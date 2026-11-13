# NYC Marriage Index – Postman collection

Unofficial Postman collection for two free New York City marriage indexes published by **Reclaim The Records**:

1. **NYC Marriage Index 1950–2017** – <https://www.nycmarriageindex.com>. A searchable database of 4.7 million City Clerk marriage licenses. The site searches a public **Solr** endpoint, `/solrsearch/`, which returns JSON.
2. **NYC Marriage Index 1908–1929** – scanned City Clerk index books (48 microfilm rolls) on the Internet Archive, one item per borough and year (`NYC_Marriage_Index_<Borough>_<Year>`, collection `nycmarriageindex`). These are page images only, with no OCR. The collection uses the Internet Archive search and IIIF APIs to find and display pages.

No key or login is needed.

## Import

In Postman: **Import → Link** and paste the raw URL of
`NYC_Marriage_Index.postman_collection.json` from this repository.

## Requests

| Request | Endpoint | Notes |
|---|---|---|
| Solr search by surname | `GET https://www.nycmarriageindex.com/solrsearch/?q=record_surnames_spouse1:SMITH OR record_surnames_spouse2:SMITH&wt=json&rows=50` | 1950–2017; fields include GROOM_SURNAME, BRIDE_SURNAME, LICENSE_YEAR, LICENSE_BOROUGH_ID, LICENSE_SEQ |
| Solr search, groom + bride + year | `q=GROOM_SURNAME:X AND BRIDE_SURNAME:Y&fq=LICENSE_YEAR:1975` | Narrow by year or borough with `fq` |
| List 1908–1929 index volumes | `GET https://archive.org/advancedsearch.php?q=collection:nycmarriageindex&fl[]=identifier&fl[]=title&rows=300&output=json` | One item per borough-year |
| Item metadata | `GET https://archive.org/metadata/NYC_Marriage_Index_Manhattan_1914` | Files and page counts |
| IIIF manifest | `GET https://iiif.archive.org/iiif/3/NYC_Marriage_Index_Manhattan_1914/manifest.json` | `items[n]` is page n; the image service id is inside |
| IIIF page image | `GET {service}/full/1400,/0/default.jpg` or `{service}/pct:13,10,30,80/700,/0/default.jpg` | Crop to the surname and given-name columns to read them |

## How the 1908–1929 books are arranged

- Each page has **grooms on the left and brides on the right**. The two columns are separate lists, not couples.
- Pages are grouped by the **first two letters of the surname** (Ka, Ke, Ki, Kl, Kn, Ko, Kr, Ku…). They cycle through the year by date, so one two-letter group recurs about every 10 pages.
- Each line gives the surname, given name, volume, page, **license number** and date. Use the license number to order the license from the NYC Municipal Archives or to view it on Historical Vital Records.
- To find a name: find the pages for the letter group (for example "Kr"), then read every page in that group for the year. Search the groom's surname and, separately, the bride's maiden and earlier married surnames.

## Coverage

- 1908–1929: all five boroughs, page images (Internet Archive)
- 1930–1949: not in these sets. Use the City Clerk license index on Ancestry, or NYC Municipal Archives
- 1950–2017: searchable database (nycmarriageindex.com); bulk CSV, XLS and SQL downloads on the Internet Archive

Part of a personal library of genealogy and archives API collections.
