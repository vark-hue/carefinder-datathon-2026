# CareFinder: Trust-Scored Healthcare Referrals for India

**CMU DSC Datathon 2026 · Healthcare Intelligence track** (Virtue Foundation × Databricks)

> *A patient needs service X near place Y. Where should they go, and why should we trust that answer?*

CareFinder treats every field in the Virtue Foundation's 10,088 Indian facility records as a **claim, not a fact**. It scores how well each claim is documented, ranks facilities by evidence and distance, explains every pick, and reports how sure it is. Then it tests itself against an independent outcome measure (NFHS-5) and is honest about what the score can and cannot claim.

📊 **Slides:** [`slides/CareFinder_Datathon_2026.pdf`](slides/CareFinder_Datathon_2026.pdf) · [`.pptx`](slides/CareFinder_Datathon_2026.pptx)
📓 **Notebook:** [`notebooks/CareFinder_notebook.py`](notebooks/CareFinder_notebook.py) (Databricks source format)
🎬 **Video:** 3-minute walkthrough (see the submission; script in [`docs/video_script.md`](docs/video_script.md))

---

## Key findings

| Finding | Result |
|---|---|
| Facilities analysed | **10,088** |
| Location conflicts | **1,540 (15%)** have coordinates > 50 km from their own PIN; **358** name a different state than their PIN |
| Emergency C-section claims (400 Monte Carlo weight draws) | **18** robustly Strong · **32** flip with the weights · **403** robustly not Strong (Strong count ranges 12–111) |
| NFHS-5 outside test, 581 districts | Raw claims r = 0.32 · evidence-weighted r = 0.32 (Δ −0.003, 95% CI −0.011 to 0.005) · total facility density r = 0.44 |
| Documentation deserts | **242 of 312** "covered" districts (90% range 134–282) have no Strong option within 50 km, led by Ernakulam, Palakkad and Kottayam (Kerala), whose C-section rate is not lower (21.9% vs 23.9%, p = 0.16) |
| Planted-fault test | Moved locations caught **100%**, inflated claim lists **96.7%** (a sanity check, partly circular) |
| Lucknow demo | Elite Hospital stays in the top 3 in **100%** of weight draws; the 4th option only 18% |

**What this means.** The NFHS-5 test is an association, not causation: wealth and urbanisation drive both. Our score measures **how well a claim is documented**, not whether care exists. Claims that score low *cannot be verified from public data*; that does not make them false. That is still what a referrer needs to know before sending someone, and it gives planners a worklist of records to verify first.


## How the evidence score works

| Component | Points |
|---|---|
| Direct claim in a structured field (capability, procedure, specialty) | up to 30 |
| Corroboration across independent fields | up to 20 |
| Supporting equipment or units | up to 15 |
| Description confirms it in free text | 10 |
| Record trust (sources, completeness, no conflicts) | up to 25 |
| Only a related specialty, no direct claim | capped at 45 |
| Integrity penalties: location −12, state −8, merged record −12, claim inflation −12 | subtracted |

**Labels:** Strong ≥ 65 · Moderate 45–64 · Weak < 45. Weak options are never hidden, only labelled. Ranking combines evidence with travel distance using a user-chosen trade-off.

## Tech stack

Databricks (Free Edition, Unity Catalog) · Python · pandas · NumPy · SciPy · ipywidgets. No external APIs.

Data: Virtue Foundation facilities · India Post PIN-code directory · NFHS-5 district health indicators (Databricks Marketplace).

## Repository layout

```
├── notebooks/CareFinder_notebook.py   # full pipeline, Databricks source format
├── slides/                            # deck (.pptx, .pdf) and the script that builds it
├── docs/video_script.md               # 3-minute demo script
└── docs/figures/                      # charts used in the deck
```

## Reproduce

1. Install the *Virtue Foundation dataset* from Databricks Marketplace.
2. Import `notebooks/CareFinder_notebook.py` into a Databricks workspace (File → Import).
3. If needed, set the three table names in **section 0**, then **Run all**. The widgets in section 9 drive the CareFinder view.

## Limitations

- NFHS-5 (2019–21) is ecological and cross-sectional and predates parts of the facility data; it is a consistency check, not proof of impact.
- C-section rate is not a quality measure.
- Scoring weights are judgement calls; we report their effect via 400 Monte Carlo re-weightings rather than pretend they are fixed.

---
Solo entry · CMU DSC Datathon 2026
