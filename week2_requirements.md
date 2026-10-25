# Requirements Specification — Internship Information Assistant
Version: 1.0

> Items marked **[TODO]** need your real project evidence. Do not submit them unfilled.

## Section 0 — Project Framing & Application Scope Checkpoint

Flow: Problem → Evidence → Existing Approaches → Engineering Gap → Objectives → Scope → Evaluation Focus → Requirements

| Element | Content |
|---|---|
| **Problem Evidence** | Students struggle to find accurate, current internship requirements, deadlines and procedures spread across handbooks, web pages and emails. **[TODO: add 1–2 credible sources, e.g. faculty internship handbook, careers-service report, student survey or helpdesk enquiry logs, plus a short explanation.]** |
| **Existing Approaches** | **[TODO: confirm/replace with real ones]** (1) University careers portal / job board: lists opportunities but does not answer procedural questions. (2) Faculty FAQ page or email helpdesk: authoritative but slow and static. (3) General-purpose chatbots (e.g. ChatGPT): conversational but not grounded in institution-specific rules and may give invented requirements. |
| **Project / Engineering Gap** | Existing tools are not grounded in the institution's approved internship documents, give no verifiable source references, and have no scope controls to prevent inappropriate advice. |
| **Objective O1** | To design a document-grounded assistant that answers internship-related questions with verifiable source references. |
| **Objective O2** | To develop a V1 with scope and safety controls that refuse or redirect out-of-scope and high-stakes requests. |
| **Objective O3** | To evaluate correctness, citation support, refusal behaviour and latency against defined thresholds. |
| **Intended Users** | Undergraduate students seeking or preparing for internships (internship coordinators as possible later users). |
| **Supported Tasks** | Answering questions on eligibility, duration and credit requirements; application procedures, required documents and forms; deadlines; and report/assessment guidelines. |
| **Information / Knowledge Domain** | Approved institutional internship handbooks, policies, forms and published internship guidance only. |
| **Operating Context** | Web chat interface used by students on laptop or phone, during the internship planning and application period. |
| **Important Constraints** | Limited set of approved documents (PDFs); student PII must not leave the system; small project budget for model/API usage; semester time limit; no access to individual student records. |
| **Explicit Out-of-Scope Tasks** | Approving/rejecting internships or confirming an individual student's eligibility; writing applications or CVs; legal, visa/immigration or financial advice; salary negotiation; guaranteeing placement. |
| **Evaluation Focus** | Does the assistant give correct, cited answers to routine internship questions, and reliably decline what it should not answer, within acceptable latency and cost? |

> **Engineering gap ≠ automatic research gap.** The gap above is a practical/technical limitation (grounding, traceability, safety controls), not a claim of scientific novelty.

## Section 1 — Functional Requirements

| # | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
|---|---|---|
| **FR1** | Answer questions about internship eligibility, duration and credit requirements using approved documents. | Invent requirements not supported by the source documents. |
| **FR2** | Answer questions about application procedures, required documents, forms and deadlines. | Confirm or decide an individual student's eligibility or approval status. |
| **FR3** | Provide a source reference (document and section/page) for answers based on approved documents. | Present unsupported information as if it came from an approved source. |
| **FR4** | State clearly when sufficient supporting evidence cannot be found and suggest an appropriate human contact (e.g. internship coordinator). | Guess or fabricate an answer to fill the gap. |
| **FR5** | Decline queries outside the defined internship-information scope and provide an appropriate redirect. | Provide legal, immigration, financial or mental-health advice, or write applications on the student's behalf. |
| **FR6** | Present answers in clear, concise language suitable for undergraduate students. | – |

## Section 2 — Non-Functional Requirements

Pattern: Quality Attribute → Requirement → Measurement Method → Metric → Threshold

| # | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| **NFR1** | Performance | Interactive responses shall be returned within the agreed latency target. | Measure end-to-end latency on a defined test workload (e.g. 50 queries). | p90 latency | < 5,000 ms |
| **NFR2** | Correctness | Answers shall be factually consistent with approved source documents. | Score a curated evaluation set (≥ 50 questions) with a defined rubric. | Correct response rate (%) | ≥ 85% |
| **NFR3** | Cost | Inference cost shall remain within the project budget. | Record model/API usage over the evaluation workload. | Cost per 100 queries | < US$0.50 (illustrative) |
| **NFR4** | Maintainability | Approved document updates shall be incorporated without rebuilding unrelated components. | Run a controlled document-update test. | Update time | < 10 min |
| **NFR5** | Reliability | The system shall handle malformed, empty or very long queries without failing. | Run a defined robustness test set. | Graceful-handling rate | ≥ 95% |

## Section 3 — Responsible AI Requirements

Pattern: Responsible AI Risk → Requirement → Measurement Method → Metric → Threshold

| # | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| **RAI1** | Hallucination / Transparency | The system shall provide a verifiable source reference for document-grounded answers and indicate when evidence is insufficient. | Evaluate responses for citation presence and whether the cited source supports the answer. | Citation presence rate; citation-source match rate | 100%; ≥ 95% |
| **RAI2** | Safety / Scope | The system shall refuse out-of-scope queries and redirect users appropriately. | Run a scope test set of ≥ 20 out-of-scope queries. | Refusal-and-redirect success rate | ≥ 95% |
| **RAI3** | Privacy | The system shall not transmit student PII to external model APIs. | Run privacy test cases and inspect outgoing model/API payloads. | Detected PII transmissions | 0 |
| **RAI4** | Fairness | Performance shall not differ beyond tolerance across justified student groups (e.g. faculty/programme, language proficiency). | Evaluate a stratified test set and compare correctness by group. | Absolute correctness-rate gap | ≤ 10 percentage points |

## Reflection

**Which Responsible AI requirement will be the most difficult to measure or enforce technically? Why?**

Draft answer (edit to your own view): RAI1 (grounding). Checking that a citation *exists* is easy, but checking that the cited passage genuinely *supports* the claim needs human or rubric-based judgement, and a fluent answer can cite a real document while still misstating its content. RAI4 (fairness) is also hard because it needs a representative stratified test set that may not exist for a small project.

## Git

```bash
git add docs/week2_requirements.md
git commit -m 'Week 2: Requirements specification (FR, NFR, RAI)'
git push
```
