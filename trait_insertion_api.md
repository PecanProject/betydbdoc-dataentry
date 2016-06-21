# Inserting New Traits Via the API

This page provides a general description of how to insert trait data via the
(new) beta version of the BETYdb API.  For information about accessing data via
the beta BETYdb API, visit
https://pecan.gitbooks.io/betydb-data-access/content/API/beta_API.html.  For a
list of URLs of API endpoints, visit https://www.betydb.org/api/docs.

## Trait Insertion Endpoint.

The path to use for trait insertion is `/api/beta/traits(.EXT)` where `EXT` is
`csv`, `xml`, or `json`.  These are used to submit data in CSV, XML, and JSON
format, respectively.  If no extension is given, JSON format is assumed.  **A
user must have _Creator_ status (page access level 3) in order to use the trait
insertion API.**

## Format of Data Files

To see some valid sample files in all three of the supported formats, see
[Running the Examples](#running-the-examples) below.

### Schema for XML Data Files

XML data files must validate against the schema specified by
`app/lib/api/validation/TraitData.xsd`.  It is possible to validate files on the
command line with `xmllint`:
```sh
xmllint --schema path/to/TraitData.xsd --noout path/to/xml-data-file
```

Note that data files of other types (CSV and JSON) are converted to XML
internally and then validated using this schema.

[To do: Give a more discursive explanation of the format for XML input.]

### Schema for JSON Data Files

[To-do]

### Schema for CSV Data Files

The format to use for CSV trait data files is largely the same as that required
for the Bulk Upload wizard explained in the [previous section](bulk upload.md).
(See the templates traits.csv and traits_by_doi.csv.)  Some significant
differences from the bulk-upload case are:

1. The date of a trait measurement must be given in a column with one of the
following headings.

    1. If the heading "utc_datetime" is used, the supplied values must conform
    to one of the following formats: `1918-11-11T10:00:00Z` or `1918-11-11Z`. In
    particular, the time must be given in UTC time (hence the "Z"), and if the
    time is specified (first format), the letter "T" must separate the date and
    the time portions.  If the time is specified, seconds must be included;
    optionally, fractional seconds may be included as well.  The resulting
    `dateloc` value will always be `5` (exact date); the `timeloc` value will be
    `1` (time to the second) if a time is given and `9` (no data) otherwise.

    1. If the heading "local_datetime" is used, the supplied values must conform
    to one of the following formats: `1918-11-11T11:00:00` or `1918-11-11`. In
    particular, if the time is specified (first format), the letter "T" must
    separate the date and the time portions.  If the time is specified, seconds
    must be included; optionally, fractional seconds may be included as well.
    The resulting `dateloc` value will always be `5` (exact date); the `timeloc`
    value will be `1` (time to the second) if a time is given and `9` (no data)
    otherwise.

    When "local_datetime" is used to specify the date-time value of a trait
    measurement, the date and time are assumed to be local (site) time if a site
    is given and if that site has a time zone value stored.  Otherwise, the
    value given is assumed to be UTC time.  (The date-time value is always
    stored in the database as UTC time.  This paragraph has to do with how the
    supplied date-time value is interpreted when read.)

  Note that only one or the other of these columns may occur in the CSV file.
  Otherwise an error results.

1. Meta-data can not be specified interactively.  Thus any associated citation,
site, species, cultivar, or treatment must be specified in each row of the CSV
file.  (This may later change so that repeated metadata specification may be
avoided.)

1. Unlike the bulk upload case, matching of metadata entries _is_ case
sensitive.  Thus, if the CSV file specifies the species as "Sorghum Bicolor" but
the database entry for the species specifies the scientificname as "Sorghum
bicolor", the upload will not be successful.

1. Unlike the bulk upload case, it is not necessary to specify an
associated citation, site, species, or treatment.  The sample file
`SIMPLE_CSV_TEST_DATA` demonstrates the case where a trait value
having no associated metadata is inserted.

1. It _is_ required, however, to specify an access level for each trait;
therefore, the CSV file _must_ have a column named `access_level`.

1. When specifying the citation in a CSV file for use with the Bulk Upload
wizard, it is necessary to have either a `citation_doi` column, or have all
three of the columns `citation_author`, `citation_year`, and `citation_title`.
When using the API, however, any combination of these may be used so long as the
values specified in each row determine a unique citation.  For example, if there
is only one citation with author "Doe", and if that is the value that occurs in
the `citation_author` column of every row of the table, then it is unnecessary
to have a `citation_year` or `citation_title` column.

1. Just as for bulk uploads, the `trait_covariate_associations` table
is consulted to determine which column names correspond to trait
variables and which ones correspond to covariate variables, and
further, which covariates correspond to which traits.  **But failing
to specify a required covariate for one or more traits will not result
in an error.** (Thus, in essence, _required_ covariates are treated
just like _optional_ covariates; they will be associated if present,
but no complaint will be made if they are not.)

1. No rounding is done of floating point values except to the extent
required to fit within PostgreSQL's 8-byte float type.  (Note that all
floating point values _may_ be specifed with an exponent; for example
3.20E-2 in place of 0.0320.)

## Error Feedback

As mentioned above, all trait insertion API calls generate an HTTP
response.  The response will use the same format as the format of the
file submitted except in the case of CSV files, where the response is
given in JSON format.

In the case of unsuccessful API calls, the response will contain
information about the types of errors that caused the call to be
unsuccessful.  These errors can be classified as follows:

### Authorization Errors

If an invalid API key is given, or if the given key is for a user who isn't
authorized to perform the given action, an authorization error is returned.  (To
do: Distinguish between authentication and authorization.)

### Lookup Errors

If a citation, site, species, or treatment is specified that doesn't match
exactly one item in the database, a lookup error occurs.  This causes the whole
data set to be returned in tree form as `annotated_post_data`.  The annotations
will be the error items next to the data item that caused the error.

### Schema Validation Errors

As mentioned above, data files in CSV and JSON format are converted to XML
format and then validated against an XML schema.  For CSV files, since the
structure of the XML document generated by the converter is generally correct,
this error usually arises only when a data value of the wrong type is given (for
example, an alphabetical string where a number is expected).  But there are
other situations that can trigger a validation error: for example, if a sample
size column (`n`) is given without including a standard error (`SE`) column, or
vice versa.[^1]

### Model Validation Errors

These errors occur when attempting to save a Trait object to the database and
may occur if a variable value is found to be out of range or if a required
attribute (e.g. `access_level`) is missing.  As in the lookup error case, this
causes the whole data set to be returned in tree form as `annotated_post_data`.

## Running the Examples

There are five sample data files in the directory `app/lib/api/test`.

`SIMPLE_XML_TEST_DATA`: A minimal XML data file consisting of a single trait.
It provides only the (currently) required values: the trait variable name, the
trait value, and an access level to specify who may view this data item.

`SIMPLE_CSV_TEST_DATA`: A minimal CSV data file consisting of a single trait.
It provides only a single variable name and value and the access level.

`TEST_XML_DATA`: A full-fledged XML data file making use of all of the
features available for XML trait data insertion: specification of
defaults for groups of traits, meta-data lookup, and complete latitude
for associating specific groups of covariates and specific sample
statistics with specific traits.

`TEST_JSON_DATA`: This JSON data file is an exact analogue to `TEST_XML_DATA`;
it should result in exactly the same trait data being inserted.

`TEST_CSV_DATA`: This CSV data file has five column headings corresponding trait
variables and two columns headings corresponding to covariate variable.  There
is a single data row, so when this file is ingested, a single new entity will be
created having 5 associated traits and each trait will have 2 associated
covariates.  Complete metadata is given for the entity (or equivalently, for the
traits it comprises).

### Using curl to Upload the Data Samples

You can upload the data in these files using `curl`.  To try this out, start
your Rails server locally with `rails s` and then, from the `/api/lib/api/test`
directory, run the command
```sh
curl -X POST --data-binary @TEST_XML_DATA localhost:3000/api/beta/traits.xml?key=<your API key>
```
(Substitute any of the other sample file names for `TEST_XML_DATA` as desired,
changing the `.xml` extension to `.json` or `.csv` where appropriate.)

These API calls all generate a response (in XML format for the XML endpoint and
in JSON format for the JSON endpoints).  If the call is successful, the response
will contain a list of the ids of the new traits that were inserted.  Note that
new entities and possibly new covariates will also be inserted, but the
information about these is not (currently) contained in the response.

## Known Bugs

1. It's too easy to make a mistake without realizing it.
 Examples:
  a. If you misspell a trait variable name in the heading, that column will simple be
 ignored; no error will occur if there exists at least one valid trait variable
 in the heading.
  b. If you include the same heading twice, the value is one column will overwrite those in the other.
1. Some error messages are obscure and seemingly unrelated to the error that
  triggered them.


[^1] These errors should really be detected during CSV file parsing before
attempting to convert to a valid XML file.