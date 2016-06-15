# Inserting new traits via the API

This page provides a general description of how to insert trait data via the
(new) beta version of the BETYdb API.  For information about accessing data via
the beta BETYdb API, visit
https://pecan.gitbooks.io/betydb-data-access/content/API/beta_API.html.  For a
list of URLs of API endpoints, visit https://www.betydb.org/api/docs.

## Trait insertion endpoint.

The path to use for trait insertion is `/api/beta/traits(.EXT)` where `EXT` is
`csv`, `xml`, or `json`.  These are used to submit data in CSV, XML, and JSON
format, respectively.  If no extension is given, JSON format is assumed.

## Running the examples

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

### Using curl to upload the data samples

You can upload the data in these files using `curl`.  To try this out, start
your Rails server locally with `rails s` and then, from the `/api/lib/api/test`
directory, run the command
```sh
curl -X POST --data-binary @TEST_XML_DATA localhost:3000/api/beta/traits.xml?key=<your API key>
```
(Substitute any of the other sample file names for `TEST_XML_DATA` as desired,
changing the `.xml` extension to `.json` where appropriate.)

These API calls all generate a response (in XML format for the XML endpoint and
in JSON format for the JSON endpoints).  If the call is successful, the response
will contain a list of the ids of the new traits that were inserted.  Note that
new entities and possibly new covariates will also be inserted, but the
information about these is not (currently) contained in the response.

## Format of data files

### Schema for XML data files

XML data files must validate against the schema specified by
`app/lib/api/validation/TraitData.xsd`.  It is possible to validate files on the
command line with `xmllint`:
```sh
xmllint --schema path/to/TraitData.xsd --noout path/to/xml-data-file
```

Note that data files of other types (CSV and JSON) are converted to XML
internally and then validated using this schema.

[To do: Give a more discursive explanation of the format for XML input.]

### Schema for JSON data files

[To-do]

### Schema for CSV data files

The format to use for CSV trait data files is largely the same as that required
for the Bulk Upload wizard explained in the [previous section](bulk upload.md).
(See the templates traits.csv and traits_by_doi.csv.)  Some significant
differences from the bulk-upload case are:

1. The date of a trait measurement must be given in a column with heading
"utc-timestamp" and must conform to the following format:
`1918-11-11T10:00:00Z`.  In particular, the time must be given in UTC time
(hence the "Z") and the letter "T" must separate the date and the time portions.
Seconds must be included; optionally, fractional seconds may be included as
well.  `dateloc` and `timeloc` values will always be `5` and `1`, respectively
(exact date, time to the second).

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

1. It _is_ required, however, to specify and access level for each trait;
therefore, the CSV file _must_ have a column named `access_level`.

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

## Error feedback

As mentioned above, all trait insertion API calls generate an HTTP
response.  The response will use the same format as the format of the
file submitted except in the case of CSV files, where the response is
given in JSON format.

In the case of unsuccessful API calls, the response will contain
information about the types of errors that caused the call to be
unsuccessful.  These errors can be classified as follows:

* 

    

