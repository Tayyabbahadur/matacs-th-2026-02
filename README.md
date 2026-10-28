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

I used OpenAI Codex to help draft the design, extraction prompt and flow diagram, and to check the scores and required file structure. I disagreed with its initial suggestion to rank Proposal C and chose to flag it until the project dates are clarified. This avoids assuming that all of C's projects fall within the required five-year period.

## Design notes

The design uses an explicit exercise reference date and proposed scoring rubric; see the assumptions in the write-up. Scores are recommendations; a human makes the award decision.
