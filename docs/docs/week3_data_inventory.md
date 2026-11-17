# Week 3 Data Inventory

## Requirement mapping
| Req ID | Data needed | Source(s) |
|---|---|---|
| FR1 | Eligibility, duration, credit rules | S01 (primary), S02 (reference) |
| FR2 | Application procedure, forms, supporting documents | S03, S01 (Seksyen 2 & 5) |
| FR3 | Document name + page + section for citation | S01–S03, stored per chunk |
| RAI2 | Answers must be traceable to an approved source version | week3_manifest.json + version/status fields | Two guideline versions exist (2014 vs 2024); checksum and status prove which one was used |

## Sources
| Source ID | Filename | Type and purpose | Version / date / owner | Access / rights | Inspection evidence |
|---|---|---|---|---|---|
| S01 | Final-Garis-Panduan-LI-UTM-2024-Senat.pdf | PDF, guideline; eligibility, duration, credit, assessment (FR1, FR3) | 2024 (Senat); PDF created 2024-06-11; owner: UTM Sekolah Pengajian Prasiswazah | Disahkan awam atau tidak? | 20 pages, 29,373 chars, text readable, 0 empty pages, almost no line breaks so clause-based splitting is needed |
| S02 | GarisPanduanLI.pdf | PDF, older guideline; reference (FR1) | 2014 (PDF created 2014-02-24); owner: UTM ; status: possibly superseded by S01 | 16 pages, 21,700 chars, text readable, 0 empty pages, normal line breaks, headings like "6.0 Skop LI" |
| S03 | 1.-Application-of-Potential-Company-for-Industrial-Training.pdf | PDF, form; application procedure (FR2) | 2023 (PDF created 2023-04-16); owner: Sekretariat Unit Pembangunan dan Kerjaya LI, UTM; status  | 3 pages, 4,391 chars, text readable, 0 empty pages, form layout with blanks, tick lists, signature lines |

## Observed limitations
- No fixed application deadline found in the documents; they refer to dates "ditentukan oleh Fakulti/Sekolah".
- S01 and S02 are two versions of the guideline and may conflict; S01 is treated as current.
- PDF page number differs from printed page number in S01 (PDF page 2 is printed "1").
- S03 is a form, so blanks and tick boxes appear as noise in extracted text.
- Documents are in Malay; some form labels are bilingual.
- Tables (e.g. assessment weights) may extract poorly.
- Not yet tested for scanned pages: none found, so OCR is not needed.

## Checkpoint A
FR1/FR2 are served by S01 and S03; FR3 needs page and section, which are preserved at chunk level in Part B.
