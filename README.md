# MATACS-TH-2026-02

**Candidate:** Tayyab Bahadur  
**Time actually spent:** 1.5 hours (candidate-reported).

This repository describes an AI-assisted proposal triage process. No deployed application or live API is required.

## Files

- [Repository overview and AI disclosure](README.md)
- [Design and answers to the five questions](WRITEUP.md)
- [Process-flow diagram](diagram/process-flow.png)
- [Exact extraction prompts and input contract](PROMPTS.md)
- [Expected sample ranking](ranking.json)

## AI use

I used OpenAI Codex to help interpret the requirements, draft the design and extraction prompt, create the diagram, and check the scoring arithmetic and submission structure. Codex initially suggested ranking C after ignoring its embedded instruction to the reviewer. I changed that approach to flag C until its project dates are clarified, because the stated experience period does not establish how many projects fall within the five-year window.

## Review and submission

The design uses an explicit exercise reference date and proposed scoring rubric; see the assumptions in the write-up. Scores are recommendations; a human makes the award decision.

Submit this repository's public URL through the Google Form provided privately in the brief within three days of receiving the brief. Keep the repository public and unchanged until contacted or for 30 days. The brief and proposal source text are intentionally excluded.
