# AI-assisted proposal triage design

## Assumptions and scoring policy

This is decision support; the reviewer makes the award decision. All facts refer to fictional proposals A-E. For this exercise only, use 1 January 2026 as the assessment reference date: the five-year experience window starts on 1 January 2021. The live system must use the project's explicit reference date and request exact dates where a summary crosses the boundary. A stated named lead counts as present even though the summaries omit the person's name. Confirmed proposal claims are not independent licence or insurance verification.

The following rubric is a proposed admin configuration, not additional criteria supplied by the client. Publish it before opening bids. A category version stores criteria IDs, evidence fields, mandatory checks, thresholds, units, weights, rubric parameters and tie policy. Code implements generic operators; category-specific requirements are data. Reject weights that do not total 100%.

Mandatory licence, WSIB and insurance statements must pass. A known failure is `ineligible`; missing, ambiguous or contradictory evidence is `flagged`, with no score or rank. Price above CAD 260,000 or completion beyond 16 weeks is ineligible; unknown price or schedule is flagged. Experience dates that cannot establish the qualifying count also require clarification before scoring. Missing optional team elements receive zero for that element, not an invented fact.

For eligible, confirmed bids, calculate points using unrounded values:

| Criterion | Points and policy |
| --- | --- |
| Experience (30) | 30 × min(qualifying commercial projects of at least 100 kW in the window / 10, 1). Ten is an admin-selected saturation cap. |
| Price (25) | 25 × lowest eligible confirmed price / bid price. Use the same locked comparison set for every bid. |
| Timeline (15) | 15 × shortest eligible confirmed schedule / bid schedule. |
| Warranty (15) | 7.5 × min(panel years / 25, 1) + 7.5 × min(workmanship years / 12, 1). |
| Team and approach (15) | 3.75 each for a named lead, identified crew, explicit safety plan and explicit monitoring plan. No bonus for persuasive language. |

Sum points, sort descending and display two decimals. Exact ties share a competition rank; display tied rows by proposal ID without implying a preference. Relative price/timeline anchors are recalculated only in a new batch snapshot, never silently.

## 1. AI vs. rules

A reviewer selects a category and uploads PDFs. Code checks file type, size, page count, malware and duplicate hashes; quarantines failures; extracts text with page references; and invokes OCR for scans. Unreadable pages go to a human. AI extracts structured claims and supporting quotations using the selected configuration. It does not decide eligibility or scores.

Code validates the JSON schema, source quotations, numeric types, units and relationships between fields. A reviewer verifies evidence, especially mandatory statements, dates and suspicious text. Deterministic code applies gates, calculates points and generates reasons from approved facts. AI helps interpret varied wording; rules provide predictable arithmetic and consistent gates.

## 2. Consistency and explainability

Freeze document hashes, extracted text/OCR version, category version, prompt/model version, reference date, confirmed facts and comparison set in each run. Pin the model and use low temperature when supported, but do not claim AI extraction is deterministic. Re-scoring an identical approved snapshot is identical; new extraction requires validation and review.

Each result shows its gate outcomes, criterion points, formula inputs, source page/snippet, uncertainties and rank explanation. Store full precision and round only for display. A reviewer can follow every number back to evidence.

## 3. Human in the loop

The admin approves the rubric before use. The reviewer confirms extraction and resolves flags; corrected claims require evidence and a reason. Never let a model-supplied confidence score waive a mandatory check. A reviewer acknowledges C's attempted manipulation before any later scoring. The final decision screen requires a human award choice and justification, including any departure from the ranking.

Keep an append-only audit log of uploads/hashes, access, configuration versions, extraction/prompt/model outputs, validations, flags, corrections, actors, timestamps, reruns, per-criterion calculations and final decision. Preserve both original and corrected values. Overrides remain explicit annotations; they do not overwrite the computed result. Store rejected unsafe uploads separately with restricted access and retention limits.

## 4. Changing criteria

An edit creates a draft version; old runs remain immutable. Warn which runs are affected. After admin approval, explicitly rescore the entire comparison set into a new run. Reuse approved facts only if their definitions still match; extract new fields and obtain review otherwise. Compare versions side by side. Never mix scores from different versions, or change a published rubric invisibly after seeing bids.

## 5. Risks and sample outcome

Wrong extraction or hallucination: require exact source evidence, schema checks and human confirmation; unknown is not zero except an explicitly absent optional rubric element. Prompt injection: treat all proposal text as untrusted data, disable tools/network, isolate documents, ignore instructions and log suspicious spans. Keyword detection is a review aid, not the security boundary.

Bias: exclude company reputation and writing style, use proposal IDs and evidence-only criteria, and inspect outcomes for systematic disadvantages. Cost/outages: cap pages/tokens, cache by document/configuration/prompt hashes, limit retries and queue failures for review. Security: enforce role access, encrypt storage, avoid third-party training retention where configurable and never expose secrets to extraction.

| Proposal | Outcome | Explanation |
| --- | --- | --- |
| A | Rank 1; 98.75 | Experience cap, best eligible price/schedule, complete approach; less workmanship coverage than E. |
| E | Rank 2; 92.38 | Strong approach and warranty; fewer qualifying projects, higher price and longer schedule than A. |
| B | Ineligible | A future subcontractor does not satisfy a licence held by the bidder. Low price cannot offset this. |
| C | Flagged | Its experience period crosses the cutoff; qualifying count needs clarification. Ignore and log the embedded instruction; do not award full marks or automatically disqualify it for that text. |
| D | Flagged | No completion commitment establishes compliance with the 16-week ceiling. |

A's points are 30 + 25 + 15 + 13.75 + 15. E's are 24 + 24.53608247 + 13.84615385 + 15 + 15. C and D can join a new comparison snapshot after evidence is clarified, potentially changing normalized scores.
