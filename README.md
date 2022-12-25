# forms-dataset
Initial repo for the creation of a public forms dataset.

By crawling a CC .pdf subset of appr. 20M:

Filters:
- no URL level filtering
- timeout of request (r) set to 3 sec
- r.status_code == 200
- r.headers["Content-Length"] < 12000000   (arbitrarily set to avoid long DL)
- r.headers["Content-Type"] in ["application/pdf","stream/pdf"]

PDF-s that got through, were opened with pymupdf
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

Top .gov Sites with number of PDFs: 
```
1	dor.mo.gov	143
2	netl.doe.gov	113
7	www.irs.gov	71
8	supremecourt.nebraska.gov	71
15	www.dhs.wisconsin.gov	49
18	www.michigan.gov	44
30	www.courts.ca.gov	30
37	www.opm.gov	26
42	www.flhsmv.gov	24
44	energy.gov	24
50	epg.modot.mo.gov	22
55	www.tax.ny.gov	20
67	dmv.ny.gov	18
68	sos.iowa.gov	18
71	www.cacb.uscourts.gov	18
73	grants.nih.gov	17
74	dssmanuals.mo.gov	17
75	www.dccourts.gov	17
76	insurance.az.gov	16
77	www.dir.ca.gov	16
87	www.dol.wa.gov	15
90	www.dcjs.virginia.gov	15
91	dor.georgia.gov	15
98	www.aphis.usda.gov	14
100	humanresources.vermont.gov	14
102	www.courts.phila.gov	14
106	www.caa.gov.mk	14
108	itd.idaho.gov	13
115	www.codot.gov	13
131	www.oregon.gov	12
146	www.nj.gov	11
147	sos.ri.gov	11
154	www.in.gov	11
```

Languages:
- 66% of the forms is monolingual english
- 14% german, 4% spanish, 4% french, 2% italian, all the other languages and language pairs are much less represented
