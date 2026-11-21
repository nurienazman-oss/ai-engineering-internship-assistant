# Week 3 — Pipeline Decisions (V1 Data Pipeline)

## 1. Topic 2 requirement(s) supported

| Requirement ID | Requirement (from `docs/week2_requirements.md`) | Data needed | Source(s) |
|---|---|---|---|
| FR1 | Answer questions on internship eligibility, duration and credit requirements using approved documents | Official LI guideline text | S01 (primary), S02 |
| FR2 | Answer questions on application procedures, required documents, forms and deadlines | Guideline text + application form | S01, S03 |
| FR3 / RAI1 | Provide a source reference (document and section/page); citation presence 100%, source-match ≥ 95% | Source identity and page/section position on every chunk | All (identity via `source` + SHA-256; page **not yet preserved**, see §4) |
| NFR4 | Incorporate approved document updates in < 10 min without rebuilding unrelated components | Re-runnable pipeline, per-source output folders, checksums | Pipeline design (§6); update time not yet measured |

## 2. Selected sources (Pathway A — PDF)
| ID | File | Pages | Extracted characters | Purpose |
|---|---|---|---|---|
| S01 | `Final-Garis-Panduan-LI-UTM-2024-Senat.pdf` | 20 | 30,302 | UTM LI guidelines for Bachelor's programmes, 2024 (Senate version) |
| S02 | `GarisPanduanLI.pdf` | 16 | 21,715 | LI guidelines (another version; date/version not yet verified) |
| S03 | `1.-Application-of-Potential-Company-for-Industrial-Training.pdf` | 3 | 4,393 | Application form for proposing a new LI company |

All three PDFs contain extractable text (not scanned), so OCR is not required.

## 3. Part B comparison (same input, 500-character chunks)
| Source | Fixed-size (chunks) | Paragraph-aware (chunks) |
|---|---|---|
| S01 | 61 | 87 |
| S02 | 44 | 60 |
| S03 | 9 | 10 |

**Observation:** fixed-size cuts every 500 characters, so sentences and clauses (e.g. clause 10.7.1) can be split mid-way. Paragraph-aware stops at paragraph boundaries and does not cut clauses, which is why it produces more (shorter) chunks.

## 4. Chosen configuration
- Method: **paragraph-aware**, `chunk_size = 500` characters
- Cleaning: repeated spaces/tabs collapsed to one space; leading/trailing whitespace trimmed. No other content removed.
- Output: `prepared_text.jsonl` — fields `id`, `source`, `text`, `page`

**Justification (link to requirements):** the guideline documents are organised into numbered clauses; keeping clauses intact supports accurate answers (FR1, FR2) and clause-level citation (FR3).

- **Benefit:** chunks follow paragraph boundaries, so the context of a rule is better preserved.
- **Accepted limitations:** (a) `page = None` — page numbers are not preserved, so a citation can only name the document, **which falls short of FR3/RAI1 (document and section/page)**. This must be fixed in a later iteration (page-aware chunking) before the retrieval/answering stage; (b) some very short chunks exist (min ≈ 9–11 characters, e.g. headings), and tables/form fields in S03 may be extracted untidily; (c) this is not semantic chunking.

## 5. Stage contracts
| Stage | Contract / evidence | Failure response |
|---|---|---|
| Ingest | `resolve_source()` — file exists under `data/raw` | `FileNotFoundError`, stop |
| Inspect | `extract_text()` is non-empty; page and character counts recorded | `ValueError` (may need OCR), stop |
| Prepare | At least one chunk is produced | `ValueError`, stop |
| Validate | Output exists, is non-empty, SHA-256 + size recorded | Stop; manifest not written |
| Record lineage | `pipeline_manifest.json` maps source → output | Stop/report if mapping missing |
| Repeatability (Cell 9) | Second run gives the same source hash, output hash and mapping | `AssertionError` |

## 6. Architecture decisions
- **ETL vs ELT:** **ETL** — text is extracted, cleaned and chunked *before* being stored as `prepared_text.jsonl`; the raw PDFs in `data/raw` stay unchanged.
- **Batch vs streaming:** **Batch** — the guideline documents change rarely (periodic/annual updates) and are re-run manually when a new version appears; there is no real-time requirement.
- **Update path (NFR4):** a new or revised PDF is added by adding one entry to `SOURCES_A` and rerunning Cell 8A; other sources' outputs are untouched. Actual update time has not been measured yet.
- **One pipeline run per source:** each PDF runs separately with its own output folder so `prepared_text.jsonl` and the manifest do not overwrite each other.

## 7. Output locations
- `data/pipeline_v1/documents_garis_panduan_2024/`
- `data/pipeline_v1/documents_garis_panduan_lama/`
- `data/pipeline_v1/documents_borang_syarikat/`

Each folder contains `prepared_text.jsonl` and `pipeline_manifest.json`.

## 8. Provenance / access caveats
- `source_version` and `access_rights` are **"Not verified"** in the manifests.
- S01 and S02 are two different versions of the LI guidelines; **S02's date/version is not yet verified** and its content may conflict with S01 (2024). Check versions in Topic 4 before using either in system answers.
- RAI3 (privacy): the sources are guideline documents and a blank application form; confirm S03 contains no filled-in student details.
- Confirm these UTM documents may be shared before committing to a public GitHub repository; otherwise commit only non-sensitive evidence.
