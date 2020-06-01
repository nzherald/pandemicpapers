# Pandemic Papers: Covid-19 Proactive Release Document Dump Text

_Pandemic Papers_ makes the New Zealand Governments proactively released [Covid-19 document
dump](https://covid19.govt.nz/resources/key-documents-and-legislation/proactive-release/) available as
searchable plain text.

The document dump consists of 325 pdf files. Some of these contain searchable text and some do not.
The goal of this project is to extract the the text from these documents and make it to search.

The text is made available as an R package, [csv](inst/extdata/covid_docs.csv), and
[Excel](inst/extdata/covid_docs.xlsx) files.

Although the primary usecase _Pandemic Papers_ supports is further software based exploration you can
get a long way by just opening the excel file and using the search functionality. At a minimum this
allows you to see if keywords of interest are in a certain documents and if they are what pages they
are on.

To use the document dump in R

```r
library(devtools)
install_github("nzherald/pandemicpapers")
data("covid_docs", package = "pandemicpapers")
```

This will pull the full set of pdf documents and hide them in R cache somewhere so a better approach
may be to clone this repository and then use `devtools::install_local`

If you have any questions or issues please reach out on [Twitter](https://twitter.com/vizowl) or
email [Chris Knox](mailto:chris.knox@nzherald.co.nz)

## Articles

If you want to get a sense of what is contained in these documents [Matt Nippert](https://twitter.com/MattNippert) has written 3 excellent _Pandemic Papers_
(paywalled) pieces.

- [No time for a trial run](https://www.nzherald.co.nz/nz/news/article.cfm?c_id=1&objectid=12332156)
- [Days from disaster](https://www.nzherald.co.nz/nz/news/article.cfm?c_id=1&objectid=12333986)
- [Eye of the storm](https://www.nzherald.co.nz/business/news/article.cfm?c_id=3&objectid=12335374)

## Fields

The spreadsheet, csv file, and data frame all conatin one row per document page with the following
columns:

- **release**: Date of release (Currently only May 8 - but hopefully there will be more)
- **category**: Cateogory document was released under see https://covid19.govt.nz/resources/key-documents-and-legislation/proactive-release/
- **title**: Document title
- **link**: URL to download the document from directly
- **doc_date**: The date the document was published (not the release date)
- **doc_type**: Briefing/Memo/Minute etc
- **page**: page of the document text is from
- **text**: text from the page
- **ocr**: text from the page that was embedded in images

The page **text** is the text that you would get if you selected the entire page in a pdf viewer and
copied it. The page **ocr** is the text extracted from images that were embedded in the page.
Extraction of text from images is not always accurate. Many pages will have only **text** or **ocr**
fields as the page was either all text or a single image.

## Additional Content

The `documents/originals` directory contains a copy of all the of released documents and the
`documents/extracts` has a text file for each image that has had text extracted from it.

## Copyright

### Documents and extracted text - Crown Copyright [CC-BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/legalcode)

The original pdf files, and the text extracted from them are owned by the Crown and are released under a Creative 
Commons 4.0 Attribution Non-Commercial International Public Licence.

The text extracted from the images in the documents is in `documents/text` - the extracted images
themselves have not been included in the repository as they are very large. This text as also
subject to Crown Copyright under the same CC-BY-NC 4.0 license.


### Code

The New Zealand Herald has released the code used to extract the text from the documents under an
MIT license. It is not required, but if you make use of this code and package we would appreciate it
if you acknowledged the New Zealand Herald.

## Requirements

If you are running R on a Mac or Linux computer you should be able to run the code used to extract
the text. It is `data-raw/extract_document_dump_text.Rmd` and you will require:

- tidyverse
- pdftools
- tesseract
- rvest


If you wish to run the OCR yourself you should delete the `documents/extracts` directory first.

The R package itself was created using [DataPackageR](https://github.com/ropensci/DataPackageR)

