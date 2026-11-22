# CareFinder: 3-minute video script

## 0:00 to 0:20 · The problem
*(Screen: notebook title cell)*
"A health worker needs to send a woman in obstructed labour for an emergency C-section. The Virtue Foundation lists 10,088 Indian facilities, but a facility *saying* it does C-sections can't always be verified from public data, and a confident wrong answer costs hours she doesn't have. CareFinder treats every field as a claim, scores how well each one is backed up, and tells you how sure it is."

## 0:20 to 1:05 · Demo
*(Screen: widgets, cell 9. Choose Emergency C-section, type Lucknow, set priority to Nearest (emergency).)*
"Pick a service and a place. Each card answers WHY: the facility's own words, with the match highlighted, how many separate fields back the claim, the source links, and, just as important, **what we could not verify**."
*(Point at the evidence label.)* "Strong, Moderate or Weak. Weak options are never hidden, but they're always labelled."

## 1:05 to 1:35 · HOW it decides
*(Screen: scoring table, cell 6)*
"Points for an explicit claim, for corroboration across separate fields, for the equipment the service needs, and for a trustworthy record. Points come off for location conflicts, merged records and inflated claim lists. The user sets the trade-off between evidence and distance."

## 1:35 to 2:30 · How sure are we? (section 13)
- *Uncertainty (13.1):* "453 facilities claim emergency C-section. Our weights are judgement calls, so we redrew them 400 times. Only 18 are robustly Strong, 32 flip depending on the weights, and 403 are robustly not Strong. The number of Strong facilities ranges from 12 to 111. CareFinder reports that uncertainty instead of hiding it."
- *Rank stability (13.4):* "Near Lucknow, the top pick, Elite Hospital, stays in the top 3 in 100% of draws. The fourth option only makes it 18% of the time, so we tell the health worker to call ahead."
- *The outside test (13.2), our most important result:* "We tested the score against NFHS-5 C-section rates in 581 districts. Raw C-section claims correlate at 0.32. Our evidence-weighted count is no better, at 0.32 (difference −0.003, 95% CI −0.011 to 0.005). The best predictor is simply how many facilities a district has at all, at 0.44. That's an association, not causation, and wealth and urbanisation drive both."
- *What that means:* "Our score measures how well a claim is **documented online**, not whether the care exists. That's still what a referrer needs to know before sending someone, but it isn't a measure of capacity."

## 2:30 to 3:00 · Impact
*(Screen: 13.3 output)*
"So we flipped the question. Of 312 districts that look covered for C-section on raw claims, 242 (90% range 134 to 282) have no Strong-evidence option within 50 km. But the top ones are Ernakulam, Palakkad and Kottayam in Kerala, which have some of India's best maternal care. Their C-section rate isn't lower (21.9% vs 23.9%, not significant). So this list isn't unmet need. It's **documentation deserts**: places where real care exists but can't be verified from public data. Fix those records first. Also 1,540 records, 15%, are internally inconsistent with their own PIN code. CareFinder doesn't just tell you where to go. It tells you how much to trust the answer, and where the data itself needs fixing."

(Sanity check: "We damaged good records on purpose. The score flagged every moved location and 94 to 97% of inflated claim lists. That check is partly circular, so the NFHS test is our main evidence.")
