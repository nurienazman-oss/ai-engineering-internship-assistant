# Evaluation Criteria — Internship Information Assistant

Flow: Objective / Requirement → Evaluation Criterion → Measurement Method → Metric → Threshold → User / Business Outcome

Objectives: **O1** design grounded assistant · **O2** develop scope/safety controls · **O3** evaluate correctness, citations, refusal, latency.

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold | User / Business Outcome |
|---|---|---|---|---|---|---|
| O3 / FR1, FR2 / NFR2 | Answer Correctness | Domain-specific capability | Evaluate ≥ 50 supported internship questions against approved documents using a rubric (correct / partially correct / incorrect). | Correct response rate | ≥ 85% | Students receive reliable answers on eligibility, procedures and deadlines, reducing helpdesk load. |
| O1 / FR3, FR4 / RAI1 | Source Citation and Support | Instruction-following capability | Inspect document-grounded responses for citation presence, and check whether the cited passage supports the answer. | Citation presence rate; citation-source match rate | 100%; ≥ 95% | Students can verify information against approved documents before acting. |
| O2 / FR5 / RAI2 | Out-of-Scope Refusal | Instruction-following capability | Test with ≥ 20 out-of-scope queries (legal, visa, application writing, approval requests). | Refusal-and-redirect success rate | ≥ 95% | Prevents inappropriate advice and directs students to the right human contact. |
| O3 / NFR1 | Response Latency | Cost and latency | Measure end-to-end response time across a defined workload (e.g. 50 queries). | p90 latency | < 5 s | Interaction feels responsive enough for routine use. |
| O1 / FR6 | Response Clarity | Generation capability | Rate responses using a simple 3-point rubric (clear wording, answers the question, actionable next step). | Mean clarity rubric score | ≥ 2.5 / 3 | Students understand the information without needing to re-ask. |
| O3 / NFR3 | Inference Cost | Cost and latency | Record API usage across the evaluation workload. | Cost per 100 queries | < US$0.50 (illustrative) | Keeps the system affordable to run for a student cohort. |

**Optional clarity rubric:** 1 = confusing or incomplete · 2 = understandable but missing detail/next step · 3 = clear, complete and actionable.

**Notes**
- Not every requirement is evaluated here; these are the most important and testable.
- Not all four capability buckets need be used; here Domain-specific, Generation, Instruction-following and Cost/latency are all relevant.
- Thresholds are initial targets and may be revised once baseline results exist.

## Reflection

**Which evaluation criterion is most important for determining whether the application will be useful to its intended users? Why?**

Draft answer (edit to your own view): Answer correctness, because an assistant that is fast and well-worded but gives a wrong deadline or eligibility rule can cause a student to miss an application or breach requirements. Citation support is the close second, since it lets students verify correctness themselves.

## Git

```bash
git add docs/week2_evaluation_criteria.md
git commit -m 'Week 2: Define evaluation criteria'
git push
```
