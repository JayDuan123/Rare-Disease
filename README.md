# Clinical decision timing — reference standard instrument

A blinded annotation instrument for the OdysseyBench clinician-gold pilot. Three
clinicians independently read 21 anonymised longitudinal case records and record, for
each contact, what they would do next — and, for each case, the window within which
escalation and referral should occur.

Specification: `notes/CLINICIAN_GOLD.md` in the analysis repository, frozen 2026-08-08
before this instrument was built.

## What it enforces

The two rules that a paper form or a spreadsheet cannot enforce, and that the study
design depends on:

1. **Pass A is prospective.** A contact is shown, answered and locked; later contacts do
   not exist in the page until the current one is locked, and a locked answer cannot be
   revised. An answer changed after seeing later evidence is not the judgement being
   measured.
2. **Pass B opens only afterwards.** The timing window is asked with the whole case
   visible, which is deliberately a hindsight judgement and is kept strictly separate
   from Pass A.

## Blinding

`data/payload.json` carries opaque labels only (`T01-S1` … `T21-S2`), ordered by a digest
so the sequence says nothing about the sources. Case text is passed through byte for byte
from the benchmark's rendered stages; PMCIDs, titles, diagnoses and outcomes are absent by
construction, and the build asserts it. The de-blinding map lives in the analysis
repository and is **not** published here.

## Running it

Static, no build step, no dependencies, no network calls. Serve the directory:

```
python3 -m http.server 8000
```

then open `http://localhost:8000`. On GitHub Pages, enable Pages for the default branch
at the repository root.

Progress is held in the rater's own browser (`localStorage`). Answers leave only when the
rater clicks download, producing a JSON file they return by hand. Nothing is transmitted
from the page.

## Files

| path | |
|---|---|
| `index.html` | the instrument |
| `data/payload.json` | 21 trajectories, 52 contacts, blinded |
