## Bulk Upload 

### Overview

There are three phases for a basic bulk upload of data:

1. Enter metadata pertaining to your data set (new sites, species, cultivars, citations, or treatments).

1. Create a CSV file of the appropriate form that contains your data.

    You may use one of the following sample headings to get started.


    --------------------------------------------------------------------------------------------------------------------------------------------
    **Heading for yield data with citation specified by author, year, and title.**

    <span id="yields.csv">citation_author,citation_year,citation_title,cultivar,species,site,treatment,date,yield,n,SE,notes,access_level</span>

    <button class="js-copy-btn" data="yields.csv">Copy to clipboard</button>
    --------------------------------------------------------------------------------------------------------------------------------------------

    If your data includes standard error and cultivar information and you do not
    plan to specify any of the required information interactively, you will be able
    to use this template “as-is”.  Otherwise, you will need to delete one or more
    columns:

    a.  If your data has no standard error information, delete both
        the `SE` and the `n` column.

    a.  If your data set has a single uniform value for the site,
        species, cultivar, treatment, access\_level, or date, then
        these values may be entered interactively through the web
        interface; in this case you should delete the
        corresponding column(s) from the template.

    a.  Note that cultivar information can’t be specified interactively unless
        the species information is as well (and vice versa); delete the
        `cultivar` column if and only if you either have no cultivar information
        or you are specifying both the species and the cultivar interactively.

    ---------------------------------------------------------------------------------------------------------------------
    **Heading for yield data with citation specified by DOI.**

    <span id="yields_by_doi.csv">citation_doi,cultivar,species,site,treatment,date,yield,n,SE,notes,access_level</span>
  
    <button class="js-copy-btn" data="yields_by_doi.csv">Copy to clipboard</button>
    ---------------------------------------------------------------------------------------------------------------------
 
    Use this template if you are uploading yield data and you wish to specify
    the citation in the file by its Digital Object Identifier (DOI).

    Again, if you do not have data for all of the columns listed in
    the template, or if you plan to specify some of the data
    interactively, you will have to delete one or more columns.

    You may also use this template if all of the data in your data
    set pertains to a single citation and you wish to specify that
    citation interactively. In this case, you must delete the
    `citation_doi` column.

    -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    **Heading for trait data with citation specified by author, year, and title.**

    <span id="traits.csv">citation_author,citation_year,citation_title,cultivar,species,site,treatment,date,entity,[trait variable 1],[trait variable 2],[trait variable n],[covariate 1],[covariate 2],[covariate n],n,SE,notes,access_level</span>

    <button class="js-copy-btn" data="traits.csv">Copy to clipboard</button>
    -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    Use this template if you are uploading trait data and you wish to specify
    the citation in the file by author, year, and title.

    **This template must be modified before it can be used.** In
    particular, the column headings `[trait variable 1]`
    …`[trait variable n]` must be replaced by actual variable names
    that *exactly* match names of variables in the database. The number
    of these trait variable columns may need to be increased or
    decreased to accomodate the data set.

    Some trait variables allow or even require corresponding covariate
    information to be included. Again, the column headings `[covariate 1]`
    …`[covariate n]` must be changed to actual covariate variable names, and the
    number of these columns may need to be increased or decreased to match the
    available information. For a list of recognized trait variable names that
    are treated as covariates, visit the trait variable/covariates list at
    [https://www.betydb.org/trait_covariate_associations](https://www.betydb.org/trait_covariate_associations){target="_blank"}
    or the corresponding page of the site to which you are uploading your data.

    As with the yield data templates, delete columns for attributes that have a
    uniform value for the data set and that you plan to specify interactively.

    Trait data files may also include an `entity` column if you wish to use
    named entities to group associated traits.  Delete this column heading from
    the template if you simply want to use anonymous automatically-created
    entities.  For more detailed information about entities, see [Optional
    data] below.

    ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    **Heading for trait data with citation specified DOI.**

    <span id="traits_by_doi.csv">citation_doi,cultivar,species,site,treatment,date,entity,[trait variable 1],[trait variable 2],[trait variable n],[covariate 1],[covariate 2],[covariate n],n,SE,notes,access_level</span>

    <button class="js-copy-btn" data="traits_by_doi.csv">Copy to clipboard</button>
    ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    As with the corresponding yield data template, use this
    template if you are uploading trait data and you wish to specify
    the citation in the file by DOI or if you plan to specify the
    citation interactively (in which case delete the
    `citation_doi` column). **Again, this template must be modified
    before it can be used.**
        
        

1.  Use the Bulk Upload Wizard in the BETYdb web interface to upload your data
    set and insert it into the database.



### Detailed CSV Data File Specifications

*In what follows, the term “field” always refers either to a column name
used in the heading of the uploaded CSV file or to an entry in that
column in some particular row of the file. On the other hand, and the
term “column” may either refer to a column of data in the uploaded CSV
file or to an attribute of a trait or yield datum in the traits or
yields table of the database.*

#### General Considerations

Although the comma-separated value (CSV) file format is not fully standardized,
here are some general guidelines:

1. The top line of the file should contain a comma-separated list of column
headings.  Any column heading not recognized as being significant (see below) will
be ignored, as will the data in subsequent rows falling under that heading.

1. Lines (or _rows_) after the first contain data.  Data items are separated by
commas, and in general there will be one data item for each column heading; the
nth data item in a row "belongs" to the nth heading in the top line.[^missing_cells]

1. There can be no extraneous blank lines, even at the end of the file.

1. Extraneous space before or after a comma or at the beginning or end of a row
is discarded.

1. To include a comma as part of a data item, the data item must be quoted with
double-quotes so that the comma is not interpreted as a data-value separator.
There should be no extraneous space between a double-quoted item and the
preceding and following commas or beginning or end of the line.

1. To include a literal double quote as part of a quoted item, use two consecutive double quotes.

#### Required data file fields

1.  For yields uploads, the only required field is a `yield` column.

1.  For trait uploads, there must be at least one column whose label exactly
    matches the variable name for the trait value being specified. (Leading and
    trailing spaces are permitted, but letter case must exactly match the name
    of the variable specified in the database.) If this trait variable has any
    required covariates, columns for these covariates must be included.  Again,
    visit
    [https://www.betydb.org/trait_covariate_associations](https://www.betydb.org/trait_covariate_associations){target="_blank"}
    (or the corresponding page for the site you are uploading to) to see which
    traits require covariates.

#### Information that is required but that *may* be specified interactively for the entire dataset.

*Attributes of data items may be specified interactively only if there is a
single uniform value that pertains to the whole data set contained in the upload
file.*

##### Information that references existing database entries {-}

As mentioned, the first step in doing a bulk upload is to ensure that there are
existing items already in the database for each attribute value of each item in
the upload set.  There are defined rules as to how to refer to these existing
attributes in your upload file.  For example, a species must be referred to by
its scientific name even though there are other attributes of the species items
stored in the species table that might uniquely identify a particular species
(the `AcceptedSymbol` attribute, for example).

In these sections, we specify, for each attribute, how to refer to the attribute
value, whether or not the attribute can be specified interactively or must be
specified in the data file, and what criteria are used to match values specified
in the data file with existing table entries in the database.

1.  Citation

    -   If the entire dataset pertains to a single citation, that citation may be
        specified interactively by choosing a citation on the citations
        page instead of including citation information in the CSV file.

    -   Otherwise, specify the citations in the CSV file, either by DOI
        or by author, year, and title.

    -   If a DOI is available for all citations in the data set, the
        citation corresponding to each row may be specified in a
        `citation_doi` column. In this case, the `citation_author`,
        `citation_year`, and `citation_title` columns must not be in the
        column heading list.[^ignoring_columns]  Each value in
        the `citation_doi` column must exactly match the `doi` attribute
        of some row in the `citations` table except that letter case and
        leading and trailing spaces are ignored.

    -   Conversely, if a DOI is not available for all citations in the data set,
        or if it is preferred to specify the citation by author, year, and
        title, then the `citation_doi` column should *not* be included and the
        columns `citation_author`, `citation_year`, and `citation_title` must
        all be present.[^ignoring_doi_column]

1.  Site

    -   If all of the data in the data set pertains to a single site,
        that site may be specified interactively.

    -   Otherwise, a `site` column is required. Each value in the column must
        match an existing `sitename` column value in the `sites` table of the
        database. (Letter case, leading and trailing spaces, and extra internal
        spaces are ignored when searching for a match.)

1.  Species

    -   If all of the data in the data set pertains to a single species,
        that species may be specified interactively.

    -   Otherwise, the `species` column is required. Each value must
        match an existing `scientificname` column value in the `species`
        table of the database. (Again, letter case, leading and trailing
        spaces, and extra internal spaces are ignored when searching for
        a match.)

1.  Treatment

    -   If a single treatment and a single citation applies to all of
        the data in the data set, the treatment may be specified
        interactively provided that the citation is specified
        interactively as well.

    -   Otherwise, a `treatment` column is required. The value must
        match an existing `name` column value in the `treatments` table
        of the database; moreover, this matching treatment must be
        consistent with the specified citation. (Again, letter case,
        leading and trailing spaces, and extra internal spaces are
        ignored when searching for a match.)

##### Other information that may be specified interactively {-}

1.  Date

    -   If a single date (with or without time of day) applies to all of the
        data in the data set, the date may be specified interactively.

    -   Otherwise, if there are multiple dates (with or without times)
        associated with the data, a `local_datetime` column is
        required.[^deprecated_date_heading]

    -   Values in the `local_datetime` column or in the `date` text box in the
        Global Values page may be in one of two forms:

        - Date values without time of day must be in the form `YYYY-MM-DD`. For
          example, July 25, 2003 must be entered as “2003-07-25”.

        - Values that include the time of day must be in the form `YYYY-MM-DD
          HH:MM:SS` or `YYYY-MM-DDTHH:MM:SS`.  (Here, `T` is simply the literal
          letter `T`.)  For example, 11 a.m. on November 11, 1918 could be
          specified either as "1918-11-11 11:00:00" or as "1918-11-11T11:00:00".
          **_Note that the yields table stores only the date and so any
          time-of-day information given in a yields data file or specified
          interactively will be ignored._**.

        Note that the date and time should always be the date and time at the
        site where the trait measurement was made.[^level-of-confidence] When
        uploading trait data, each site associated with the data file must be
        associated with a valid time zone![^specifying_a_timezone][^null_timezone]

1.  Rounding

    -   The amount of rounding for numerical data can only be
        specified interactively. Any value from 1 to 4 significant
        digits may be chosen. The amount of rounding for the standard
        error SE (if present) may be specified separately from the
        amount of rounding for yield and for trait variables and
        their covariates.

    -   By default, all numerical measurements are rounded to three
        significant digits. For example, with this default in place,
        999.1 will be rounded to 999 and 1001.1 will be rounded to 1000.

    -   Standard error values (if given) are by default rounded to two
        significant digits.

#### Numerical Data

Numerical data is *never* specified interactively since typically each
measurement will have a different numerical value so there will never be a
uniform value for all data in the data set.

##### Data for Yields {-}

1.  Yield

    Every yield data upload file must have a `yield` column. The data in
    this column must always be a parsable non-negative number and must
    never be blank. Scientific notation is not currently supported. As
    noted above, the number given in the file is subject to rounding
    before being inserted into the database.

1.  Sample Size

    An `n` column is required if and only if an `SE` column is included.
    The value must always be an integer greater than 1.

1.  Standard Error

    An `SE` column is required if and only if an `n` column is included; this
    datum will be inserted into the `stat` column of the `yields` table, and the
    `statname` column value will be set to “SE”.  As with the yield column, the
    data in this column must never be blank, and values can't be in scientific
    notation.[^se_note]

##### Data for Traits {-}

1.  Trait variable values

    -   Every trait data upload file must have at least one column whose heading
        matches the name of some recognized trait variable. A list of recognized
        trait variables is listed on the BETYdb web site. If multiple trait
        variable columns are used, each row in the CSV file will produce one row
        in the `traits` table for each trait variable column having a non-blank
        entry.[^blank_entries] (These resulting rows will be effectively
        *grouped* by assigning them a unique entity id. Said another way, there
        is a one-to-one correspondence between rows in the CSV file and
        resultant rows in the `entities` table, the table that keeps track of
        this grouping.) As with yield numbers, the data in this column must
        always be a parsable number and is subject to rounding before being
        inserted into the database. In addition, it must conform to any range
        restrictions on the value of the variable.

    -   The template for traits uploads provides dummy column headings
        `[trait variable 1]`, `[trait variable 2]`, etc., which must be
        changed to actual variable names before data can be uploaded.

1.  Covariate values

    -   If any of the included trait variables has a required covariate,
        there must be a column corresponding to that covariate.

    -   For any of the included trait variables that has an optional
        covariate, a column corresponding to that covariate *may*
        be included.

    -   As with trait variable columns, entries in a covariate variable column
        may be left blank.[^required_covariate_loophole]

    -   The template for traits uploads provides dummy column headings
        `[covariate 1]`, `[covariate 2]`, etc., which must be changed to
        actual variable names before data can be uploaded.

1.  Sample Size and Standard Error

    An `SE` column is required if and only if an `n` column is included; this
    datum will be inserted into the `stat` column of the `traits` table, and the
    `statname` column value will be set to “SE”. ***Note that if you have more
    than one trait variable column, the `n` and `SE` columns are not allowed.**
    This is because there is currently no way to use different standard error
    values for different trait variables, and it is unlikely that different
    variables would share the same value for the standard
    error.[^future_se_enhancements]

    Note that even if `n` and `SE` values _are_ specified, the `n` and `SE`
    values for any associated covariates will be set to NULL: There is currently
    no way to specify standard error values for covariates in a bulk upload
    file.

    Again, values of `n` must be at least 2, and columns for `n` and
    `SE` must both be present or both be absent.

#### Optional data

1.  Sample Size and Standard Error

    As noted above, these are both optional, but if one of these is included,
    the other must be included as well. In other words, the column heading list
    must include both of `n` and `SE` or neither. Note that if `n` and `SE` are
    not included in the uploaded CSV file, the value of the `n` column of the
    traits or yields table will default to 1 and the `stat` and `statname`
    column values will default to NULL and the empty string, respectively.

1.  Cultivar

    -   If a uniform value for the species is provided interactively
        when uploading the data set, the cultivar may be specified this
        way as well, provided that it also has a uniform value for the
        whole data set.

    -   Otherwise, to include cultivar information in the upload file, both a
        `species` and a `cultivar` column must be included. The values in the
        `cultivar` column are allowed to be blank (in which case a value of NULL
        is inserted into the `cultivar_id` column for the given row); but if
        provided, the value must match the value of the `name` column in some
        row of the `cultivars` table; moreover, this row must be a row
        associated with the species corresponding to the value given in the
        `species` column. Again, matching is case insensitive, and leading,
        trailing, and excess internal whitespace is ignored.

1.  Notes

    To include notes, use a `notes` column. There is no restriction on
    what can be included in this column, but leading and trailing space
    will be stripped before insertion into the database. Non-ascii
    characters entered in the file in UTF-8 encoding are allowed. If
    there is no `notes` column, each row inserted into the `traits` or
    `yields` table will use the empty string as the value for the
    `notes` column.

1.  Entities

    Entities are a way of grouping related traits.  For example, trait
    measurements made at the same time on the same plant group, plant, or plant
    part are intrinsically related.  To show this in the database, they may be
    given a common value for the `entity_id` attribute.

    The Bulk Upload Wizard handles entities as follows:

    a. The data file is for yields.  In this case, no entities are created, and
       all yield rows created will have NULL as their `entity_id` attribute.

    a. The data file is for traits and has no "entity" column but has at least
    two trait-variable columns.  In this case, what happens for a given row will
    depend on whether that row has any non-blank trait-variable column values.

        i. If the row has at least one non-empty trait-variable column value, a
    new, anonymous entity will be created and each trait created for the row
    will be assigned the new entity.

        i. If all trait-variable column values in the row are blank, no entities
        or traits are created for that row.

    a. The data file is for traits, has no "entity" column, and has only one
       trait-variable column.  In this case, no entities are created, and all
       trait rows created will have NULL as their `entity_id` attribute.

    a. The data file is for traits and _does_ have an "entity" column.  In this
    case, what happens for a given row will depend on whether the "entity"
    column and the trait-variable columns are blank.

        i. If the "entity" column is not blank and the name given there matches
        the name of an existing entity, the new traits created for the row will
        be assigned to that entity.

        i. If the "entity" column is not blank but does not match the name of
        any existing entity, and if at least one trait-variable column value is
        non-blank, a new entity will be created whose name is the value
        specified in the "entity" column, and new traits created for the row
        will be assigned to this new entity.

        i. If the "entity" column is not blank but all trait-variable column
        values _are_ blank, no new entity will be created whether or not the
        value in the "entity" column matches the name of an existing entity.

        i. Rows in which the "entity" column is blank are treated as in the case
        that the entity column does not exist: that is, anonymous entities are
        only created if there are at least two trait-variable columns and then
        only for rows for which at least one trait-variable column value is
        non-blank.

1. Methods

    A method _may_ be specified for each trait variable in the data file.
    Methods must be specified interactively on the Upload Options and Global
    Values page.  This means of course that for each file, each trait variable
    must be assigned uniformly to the same method; trait values in different
    rows can not be assigned different methods.


### Using the Bulk Upload Wizard

The Bulk Upload Wizard is a sequence of pages designed to guide the user through
the process of uploading a data file and having its data added to the database.
Here is a step-be-step guide to using the wizard.  This guide assumes you have
already composed a data file, and that it is accessible in the file system of
the computer you are using to access the wizard.

1. Click the Bulk Upload menu item at the top of any BETYdb page.

1. On the "New Bulk Upload" page, click the "Choose File" button.  In the file
chooser that comes up, find the file you want to upload and double-click on it.

1. Click the "Upload and validate file" button.

1. If you do not have citation information in your file and you have not chosen
a citation to use in your browser session, you will be taken to the "Choose a
Citation" page.  Otherwise, skip the next steps.

    Type into the auto-completion citation text box and choose from among the
list of citations that come up.  Note that the list of citations will be
filtered by trying to match the author, year, title, or DOI against the string
of characters you type into the box.

1. Once you have chosen a citation, click the "View Validation Results" button.

1. View the validation results.  This page will display your data file and will
highlight any errors or possible errors.  For details on potential problems, see
the [Troubleshooting] section.

1. If there are no errors to be dealt with, click the link on the upper-right to
go on to the "Specify Upload Options and Global Values page.



### Troubleshooting

Once a CSV data file has been composed

[^missing_cells]: In some cases, it is allowable for data in some columns to be
missing from some rows.  In this case, there will be two consecutive commas with
only zero or more white-space characters in between, or, in the case of the
first or last columns, there may be only whitespace before the first or after
the last comma of the row.  If items are omitted from the end of a line, the
trailing commas may be omitted as well.

[^ignoring_columns]: If such information is already included in the data set and
you want to keep such columns for purely informational purposes, the string
`-ignore` may be appended to each of these headings. (In fact, renaming the
columns to any non-recognized heading name will do.)

    One might want to do this, for example, to keep a visual record of the
author, year, and title even when it is the citation DOI that is being used to
determine how the data will associated with a citation in the database.

[^ignoring_doi_column]: Again, if some DOI information is already included and
you wish to retain it for purely informational purposes, you could append
`-ignore` to the `citation_doi` heading.

[^deprecated_date_heading]: This column can also be called `date`, but using
this as the column heading is deprecated: `local-datetime` more clearly
emphasizes that the dates or dates-and-time specified in this column are
interpreted as being the date/time in the time zone of the site where the trait
measurement was made.

[^level-of-confidence]: The `dateloc` (Date Level of Confidence) value is always
set automatically to 5 ("day").  The `timeloc` (Time Level of Confidence) value
is automatically set to 1 ("second") if the time of day is given and 9 ("no
data") otherwise.

[^specifying_a_timezone]: Currently, there is not way to specify a site timezone
via the BETYdb web application.  One must manipulate the database directly.

[^null_timezone]: The rule is slightly different for a site that is specified
interactively: If a time zone has been specified for the site, it must still be
a valid one.  But it isn't an error to specify a site whose time zone attribute
is null.  In this case, the date or date-and-time values specified will be
interpreted as being in UTC.

[^se_note]: Values _should_ be non-negative, but this isn't currently enforced.

    It is conceivable that one might have a data set in which some rows have SE
    values and some do not.  The Bulk Upload Wizard doesn't currently handle
    such a case, and such a data set would have to be separated into two files:
    one with columns for `n` and `SE`, and one without.

[^blank_entries]: Unlike yield data files, entries in trait or covariate variable
columns of a trait data file are allowed to be blank.  In this case, no trait is
inserted into the database for that variable of that row of the data file.

[^required_covariate_loophole]: There is a small loophole in the way required
covariates are enforced.  While it is true that if a column for a trait having a
required covariate is included, there must also be a column for that covariate,
it is not flagged as an error if certain rows leave that covariate column blank.

[^future_se_enhancements]: Eventually, we may enable associating differing
values of `n` and `SE` to different trait variables and covariates. In this
case, we might add columns `[trait variable 1] n` and `[trait variable 1] SE`,
etc. or `[covariate 1] n` and `[covariate 1] SE`, prefixing the usual column
heading with a variable name to indicate which variable the sample size and
standard error value is to be associated with.
    
<script>

// This code is an adapted version of code found in the section "Complex
// Example: Copy to clipboard without displaying input" in an answer to a
// StackOverflow post at
// https://stackoverflow.com/questions/400212/how-do-i-copy-to-the-clipboard-in-javascript.


function copyTextToClipboard(text) {
  var textArea = document.createElement("textarea");

  //
  // *** This styling is an extra step which is likely not required. ***
  //
  // Why is it here? To ensure:
  // 1. the element is able to have focus and selection.
  // 2. if element was to flash render it has minimal visual impact.
  // 3. less flakyness with selection and copying which **might** occur if
  //    the textarea element is not visible.
  //
  // The likelihood is the element won't even render, not even a flash,
  // so some of these are just precautions. However in IE the element
  // is visible whilst the popup box asking the user for permission for
  // the web page to copy to the clipboard.
  //

  // Place in top-left corner of screen regardless of scroll position.
  textArea.style.position = 'fixed';
  textArea.style.top = 0;
  textArea.style.left = 0;

  // Ensure it has a small width and height. Setting to 1px / 1em
  // doesn't work as this gives a negative w/h on some browsers.
  textArea.style.width = '2em';
  textArea.style.height = '2em';

  // We don't need padding, reducing the size if it does flash render.
  textArea.style.padding = 0;

  // Clean up any borders.
  textArea.style.border = 'none';
  textArea.style.outline = 'none';
  textArea.style.boxShadow = 'none';

  // Avoid flash of white box if rendered for any reason.
  textArea.style.background = 'transparent';


  textArea.value = text;

  document.body.appendChild(textArea);
  textArea.focus();
  textArea.select();

  try {
    var successful = document.execCommand('copy');
    var msg = successful ? 'successful' : 'unsuccessful';
    console.log('Copying text command was ' + msg);
  } catch (err) {
    console.log('Oops, unable to copy');
  }

  document.body.removeChild(textArea);
}


var copyBtnArray = document.querySelectorAll('.js-copy-btn');

copyBtnArray.forEach(function(button) {
    button.addEventListener('click', function(event) {
        var sourceId = event.target.getAttribute("data");
        var text = document.getElementById(sourceId).textContent;
        alert(text);
        copyTextToClipboard(text);
    });
});


</script>
