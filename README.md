# forms-dataset
Initial repo for the creation of a public forms dataset.

By crawling a CC .pdf subset of appr. 20M:

Filters:
- no URL level filtering
- timeout of request (r) set to 3 sec
- r.status_code == 200
- r.headers["Content-Length"] < 12000000   (arbitrarily set to avoid long DL)
- r.headers["Content-Type"] in ["application/pdf","stream/pdf"]

PDF-s that got thorugh, were opened with pymupdf
- doc = fitz.open(stream=r.content, filetype="pdf")

Data collected:
- size (as in content-length)
- len(doc) - length of document
- doc.is_form_pdf (0 if no form element, positive int if any, showing the number of form elements)


URL-s parsed: 20 888 505
PDFs available online: 7 169 385
PDFs with exactly 1 form element:  152164
PDFs with more than 1 form element:  66046 
Documents with 5+ Form elements and one page: 19824

Insights:
- 2.5% of all (live) links are from .gov sites
- only 10% of all PDF with form elements come from url's containing ".gov"
- 40% of the crawled urls **containing forms** have only 1 pdf on them, 50% on the other hand more than 5 pdf's with the same base url
- while only 2% of ALL (live) links contained the word "form", 10% of all the documents that had at least one form element had the word "form" in the url
