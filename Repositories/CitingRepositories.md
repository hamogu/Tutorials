# Citing Repositories in AAS Journals (AJ/ApJ)

This tutorial details how to cite repositories in your manuscript. The AAS Journals now recommend that content related to published manuscripts be archived in persistent repositories (See our parallel document, [Using Repositories](UsingRepositories.md)). This tutorial documents the acquisition of repository metadata and high level requirements for the final reference, as well as tips for constructing BibTeX and LaTeX bibliographies. Finally, it provides suggestions on how the inline citation should be constructed.

## Repository Citations

  Requirements for references are subject to change as we refine new citation types in AAS Journals, but the current reference format for digital objects in repositories is as follows:

    {author*} {year}, {title}, {version^}, {publisher|howpublished~}, {prefix}:{identifier#}

  To illustrate and document this format, we use a corresponding BibTeX entry taken and modified from a [real example](http://dx.doi.org/10.5281/zenodo.15991)). Note that all data/software BibTeX entries should be of the `@misc` type: 

    @misc{lia_corrales_2015_15991,
        author       = {Lia Corrales},
        title        = {{dust: Calculate the intensity of dust scattering halos in the X-ray}},
        month        = mar,
        year         = 2015,
        doi          = {10.5281/zenodo.15991},
        version      = {1.0},
        publisher    = {Zenodo},
        url          = {http://dx.doi.org/10.5281/zenodo.15991}
        }
  The corresponding reference entry should look like:

    Corrales, L. 2015a, dust: Calculate the intensity of dust scattering halos in the X-ray, v1.0, Zenodo, doi:10.5281/zenodo.15991
    

#### BibTeX Tips, Tricks
  
  You can quickly get a BibTeX entry for a DOI issued by any of the third party repositories listed below with this simple command (Thanks [CrossRef!](http://labs.crossref.org/resolving-citations-we-dont-need-no-stinkin-parser/)):
  
  ```Shell
  curl -LH "Accept: application/x-bibtex" http://dx.doi.org/10.5555/12345678
  ```
  
  In addition, any DataCite DOI has a human readable metadata page associated with it that is accessible through the URL `http://data.datacite.org/<doi>`, e.g., `http://data.datacite.org/10.5281/zenodo.15991`. From here you can download the reference in RIS or BibTeX formats.
  
  There are a number of points to make about the conversion of this BibTeX entry into a formal reference in an AAS Journal article. First, the older BibTeX style file, [`apj.bst`](ads.harvard.edu/pubs/BibTeX/astronat/apj/apj.bst), does not recognize all of these fields when formatting an `@misc` entry during LaTeX/BibTeX compilation. A new `aasjournal.bst` style file has been specifically modified to enable this formatting for software/data citations. You can find it at the [AAS Journals website](http://journals.aas.org/authors/aastex.html) or on [GitHub](https://github.com/AASJournals/AASTeX60).

  Second, for software/data references, you can consider the following tips or advice about these BibTeX fields and how they translate to a reference in an AAS Journal article: 

  - **{author*}** the author field should been formatted to match journal style: last name, first initial, etc. The current [`apj.bst`](http://ads.harvard.edu/pubs/bibtex/astronat/apj/apj.bst) does this correctly, as does the newest [`aasjournal.bst`](http://journals.aas.org/authors/aastex/aasjournal.bst).
  - **{version^}** The outdated `apj.bst` does not pick up the version BibTeX key, and you many have to insert it manually into your final reference. This field may or may not even exist for your data/code repository or data object. For example, there is no versioning between the Zenodo DOIs (yet), requiring you to carry version along manually.
  - **{publisher|howpublished~}** Please use the `{publisher}` key; you may have to add it manually as some repositories do not by default provide BibTeX with this key entered (e.g., Zenodo). It is not best practice to rely on information semantically encoded in the DOI string. Note you can "trick" BibTeX to use the `{howpublished}` key for the publisher and avoid manually fixing things, but this is not recommended as the new `aasjournal.bst` file will correctly parse the `{publisher}` BibTeX key. 
  - **{prefix}:{identifier#}** While in the majority of cases the "prefix" of the data/code persistent identifier will be a "doi", we reserve the generic model for edge cases, including "hdl", "arXiv", "ark", "purl", "ivoa", "abs", etc. If this were purely a "DOI" field then formal DataCite recommendations include listing the full URI with scheme (e.g., http), host (e.g., dx.doi.org) and path (e.g., /10.5281/zenodo.15991). This format may be adjusted going forward if the `\url` BibTeX key consistently reflects the full URI for all data/code repositories.

  In summary, it is important to remember that some of the fields listed above are either not provided by the archives ("publisher") or are listed in the BibTeX but incorrectly recognized and encoded by the BibTeX program using older BibTeX style files. 

## Inserting Citations

  When inserting citations into your manuscript, you should use the standard natbib, `\citet`, `\citep`, etc markup used for all other references. There are two important nuances about digital object citations. First, unlike books or journal articles that are effectively static and unchanging after publication, software and possibly data *evolve* forward, improving by fixing bugs, revising reduction algorithms, etc. Such objects may have a non-static **current** version of that research object located at a specific URL that the author wishes to alert the reader about. Second, authors may simply want to highlight the digital objects inline to the manuscript so that readers can link directly to the software or data without browsing to the bibliography. 

  We recommend a parenthetical markup to add inline URLs that point to non-static codebases or provide direct links to data:
   
  ```  
  \citet[][Codebase: \url{https://github.com/eblur/dust}]{lia_corrales_2015_15991}
  ```

  ```
  \citet[][Dataset: \url{http://doi.org/10.5281/zenodo.15991}]{lia_corrales_2015_15991}
  ```

  This parenthetical style is our current recommended way of dealing with this "dual pointer" problem. Authors may continue to use footnotes to insert non-static or direct data links into their manuscripts according to the writing style that best suites their work. 

