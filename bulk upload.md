BETYdb: Bulk Data Upload 
========================

Overview
--------

There are three phases for a basic bulk upload of data:

1.  Use the web interface

    -   to enter metadata pertaining to your data set (new sites,
        species, cultivars, citations, or treatments);

    -   to obtain a template appropriate for your data set.

2.  Fill in the template with your data. There are four templates to
    choose from:

    -   [yields.csv](https://docs.google.com/spreadsheets/d/1maK1uKr6i9KERaYdU5zSiXcBndQoiG4Vgn2DTnqdfbA/export?format=csv&gid=0)
        — Use this template if you are uploading yield data and you wish
        to specify the citation in the file by author, year, and title.

        If your data includes standard error and cultivar information
        and you do not plan to specify any of the required information
        interactively, you will be able to use this template “as-is”.
        Otherwise, you will need to delete one or more columns:

        1.  If your data has no standard error information, delete both
            the `SE` and the `n` column.

        2.  If your data set has a single uniform value for the site,
            species, cultivar, treatment, access\_level, or date, then
            these values may be entered interactively through the web
            interface; in this case you should delete the
            corresponding column(s) from the template.

        3.  Note that cultivar information can’t be specified
            interactively unless species information is as well; delete
            the `cultivar` column if and only if you either have no
            cultivar information or you are specifying both the species
            and the cultivar interactively.

    -   [yields\_by\_doi.csv](https://docs.google.com/spreadsheets/d/1ExLosMvX05jHWO9UYVE4Dxcl2ZbUgPc0KYoUPruaOtM/export?format=csv&gid=0)
        — Use this template if you are uploading yield data and you wish
        to specify the citation in the file by doi.

        Again, if you do not have data for all of the columns listed in
        the template, or if you plan to specify some of the data
        interactively, you will have to delete one or more columns.

        You may also use this template if all of the data in your data
        set pertains to a single citation and you wish to specify that
        citation interactively. In this case, you must delete the
        `citation_doi` column.

    -   [traits.csv](https://docs.google.com/spreadsheets/d/1TK-u-m4SG1KupYCVDUIye1C3zX8b1xgaYIG1fHNkYjs/export?format=csv&gid=0)
        — Use this template if you are uploading trait data and you wish
        to specify the citation in the file by author, year, and title.

        **This template must be modified before it can be used.** In
        particular, the column headings `[trait variable 1]`
        …`[trait variable n]` must be replaced by actual variable names
        that *exactly* match names of variables in the database that
        have been marked to be recognized as trait variables. The number
        of these trait variable columns may need to be increased or
        decreased to accomodate the data set.

        Some trait variables allow or even require corresponding
        covariate information to be included. Again, the column headings
        `[covariate 1]` …`[covariate n]` must be changed to actual
        covariate variable names, and the number of these columns may
        need to be increased or decreased to match the
        available information. As with the yield data templates, some
        columns may also need to be deleted. For a list of recognized
        trait variable names and their corresponding required and
        optional covariates, visit the trait variable/covariates list
        at www.betydb.org. \[TO-DO: Make this Web page.\]

    -   [traits\_by\_doi.csv](https://docs.google.com/spreadsheets/d/1Bv4dAPKU6YDJ6yB0DC4bAmHoGxSLgKybMpTR7qBvCu0/export?format=csv&gid=0)
        — As with the corresponding yield data template, use this
        template if you are uploading trait data and you wish to specify
        the citation in the file by doi or if you plan to specify the
        citation interactively (in which case delete the
        `citation_doi` column). **Again, this template must be modified
        before it can be used.**

3.  Use the web interface to upload your data set and insert it into
    the database.

*In what follows, the term “field” always refers either to a column name
used in the heading of the uploaded CSV file or to an entry in that
column in some particular row of the file. On the other hand, and the
term “column” may either refer to a column of data in the uploaded CSV
file or to an attribute of a trait or yield datum in the traits or
yields table of the database.*

Detailed CSV Data File Specifications
-------------------------------------

### Required fields

1.  For yields uploads, the only required field is a `yield` column.

2.  For trait uploads, there must be at least one column whose label
    exactly matches the variable name for the trait value
    being specified. (Leading and trailing spaces are permitted, but
    letter case must exactly match the name of the variable specified in
    the database.) If this trait variable has any required covariates,
    columns for these covariates must be included.

### Information that is required but that *may* be specified interactively for the entire dataset.

*Data values may be specified interactively only if there is a single
value that pertains to the whole data set.*

***Information that references existing database entries***

1.  Citation

    -   If only one citation for the entire dataset exists, it may be
        specified interactively by choosing a citation on the citations
        page instead of including citation information in the CSV file.

    -   Otherwise, specify the citation in the CSV file, either by doi
        or by author, year, and title.

    -   If a DOI is available for all citations in the data set, the
        citation corresponding to each row may be specified in a
        `citation_doi` column. In this case, the `citation_author`,
        `citation_year`, and `citation_title` columns must not be in the
        column heading list. (If such information is already included in
        the data set, to keep such columns for purely informational
        purposes, the string `-ignore` may be appended to each of
        these headings. One might want to do this, for example, to keep
        a visual record of the author, year, and title even when it is
        the citation doi that is being used to determine how the data
        will associated with a citation in the database.) Each value in
        the `citation_doi` column must exactly match the `doi` attribute
        of some row in the `citations` table except that letter case and
        leading and trailing spaces are ignored.

    -   Conversely, if a DOI is not available for all citations in the
        data set, or if it is preferred to specify the citation by
        author, year, and title, then the `citation_doi` column should
        *not* be included and the columns `citation_author`,
        `citation_year`, and `citation_title` must all be present.
        (Again, if some DOI information is already included and you wish
        to retain it for purely informational purposes, simply give the
        column some descriptive name other than `citation_doi` and it
        will be ignored by the upload code.)

2.  Site

    -   If all of the data in the data set pertains to a single site,
        that site may be specified interactively.

    -   Otherwise, a `site` column is required. The value must match an
        existing `sitename` column value in the `sites` table of
        the database. (Letter case, leading and trailing spaces, and
        extra internal spaces are ignored when searching for a match.)

3.  Species

    -   If all of the data in the data set pertains to a single species,
        that species may be specified interactively.

    -   Otherwise, the `species` column is required. The value must
        match an existing `scientificname` column value in the `species`
        table of the database. (Again, letter case, leading and trailing
        spaces, and extra internal spaces are ignored when searching for
        a match.)

4.  Treatment

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

***Other information that may be specified interactively***

1.  Date

    -   If a single date applies to all of the data in the data set, the
        date may be specified interactively.

    -   Otherwise, a `date` column is required.

    -   Date values must be in the form YYYY-MM-DD. For example, July
        25, 2003 must be entered as “2003-07-25”. (Eventually, month and
        day may become optional, in which case any of the forms
        “2003-07-25”, “2003-07”, and “2003” would represent dates of
        varying degrees of specificity. Note that uploading dateloc,
        time, and timeloc information is not supported.)

2.  Rounding

    -   The amount of rounding for numerical data can only be
        specified interactively. Any value from 1 to 4 significant
        digits may be chosen. The amount of rounding for the standard
        error SE (if present) may be specified separately from the
        amount of rounding for yield and for trait variables and
        their covariates.

    -   By default, all numerical data is rounded to three
        significant digits. For example, with this default in place,
        999.1 will be rounded to 999 and 1001.1 will be rounded to 1000.

### Numerical Data (This is *never* specified interactively.)

***Data for Yields***

1.  Yield

    Every yield data upload file must have a `yield` column. The data in
    this column must always be a parsable non-negative number and must
    never be blank. Scientific notation is not currently supported. As
    noted above, the number given in the file is subject to rounding
    before being inserted into the database.

2.  Sample Size

    An `n` column is required if and only if an `SE` column is included.
    The value must always be an integer greater than 1.

3.  Standard Error

    An `SE` column is required if and only if an `n` column is included;
    this datum will be inserted into the `stat` column of the `yields`
    table, and the `statname` column value will be set to “SE”.

***Data for Traits***

1.  Trait variable values

    -   Every trait data upload file must have at least one column whose
        heading matches the name of some recognized trait variable. A
        list of recognized trait variables is listed on the BetyDB
        web site. If multiple trait variable columns are used, each row
        in the CSV file will produce one row in the `traits` table for
        each trait variable column. (These resulting rows will be
        effectively *grouped* by assigning them a unique entity id. Said
        another way, there is a one-to-one correspondence between rows
        in the CSV file and resultant rows in the `entities` table, the
        table that keeps track of this grouping.) As with yield numbers,
        the data in this column must always be a parsable number and is
        subject to rounding before being inserted into the database. In
        addition, it must conform to any range restrictions on the value
        of the variable.

    -   The template for traits uploads provides dummy column headings
        `[trait variable 1]`, `[trait variable 2]`, etc., which must be
        changed to actual variable names before data can be uploaded.

2.  Covariate values

    -   If any of the included trait variables has a required covariate,
        there must be a column corresponding to that covariate.

    -   For any of the included trait variables that has an optional
        covariate, a column corresponding to that covariate *may*
        be included.

    -   The template for traits uploads provides dummy column headings
        `[covariate 1]`, `[covariate 2]`, etc., which must be changed to
        actual variable names before data can be uploaded.

3.  Sample Size and Standard Error

    An `SE` column is required if and only if an `n` column is included;
    this datum will be inserted into the `stat` column of the `traits`
    table, and the `statname` column value will be set to “SE”. ***Note
    that if you have more than one trait variable column, each trait
    will get the same values of `n` and `SE`. There is currently no way
    to use different sample size and standard error values for different
    trait variables. Also, the `n` and `SE` values for any associated
    covariates will be set to NULL.*** (Eventually, we may enable
    associating differing values of `n` and `SE` to different trait
    variables and covariates. In this case, we might add columns
    `[trait variable 1] n` and `[trait variable 1] SE`, etc. or
    `[covariate 1] n` and `[covariate 1] SE`, prefixing the usual column
    heading with a variable name to indicate which variable the sample
    size and standard error value is to be associated with.)

    Again, values of `n` must be at least 2, and columns for `n` and
    `SE` must both be present or both be absent.

### Optional data

1.  Sample Size and Standard Error

    As noted above, these are both optional, but if one of these is
    included, the other must be included as well. In other words, the
    column heading list must include both of `n` and `SE` (or, in the
    case of traits, `[trait or covariate variable k] n` and
    `[trait or covariate variable k] SE`) or neither. Note that if `n`
    and `SE` are not given fields of the uploaded CSV file, the value of
    the `n` column of the traits or yields table will default to 1 and
    the `stat` and `statname` column values will default to NULL.

2.  Cultivar

    -   If a uniform value for the species is provided interactively
        when uploading the data set, the cultivar may be specified this
        way as well, provided that it also has a uniform value for the
        whole data set.

    -   Otherwise, to include cultivar information in the upload file,
        both a `species` and a `cultivar` column must be included. The
        values in the `cultivar` column are allowed to be blank (in
        which case a value of NULL is inserted into the `cultivar_id`
        column for the given row); but if provided, the value must match
        the value of the `name` column in some row of the `cultivars`
        table, and moreover, this row must be a row associated with the
        species corresponding to the value given in the
        `species` column. Again, matching is case insensitive, and
        leading, trailing, and excess internal whitespace is ignored.

3.  Notes

    To include notes, use a `notes` column. There is no restriction on
    what can be included in this column, but leading and trailing space
    will be stripped before insertion into the database. Non-ascii
    characters entered in the file in UTF-8 encoding are allowed. If
    there is no `notes` column, each row inserted into the `traits` or
    `yields` table will use the empty string as the value for the
    `notes` column.

