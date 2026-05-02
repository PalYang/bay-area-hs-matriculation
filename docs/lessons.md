# Methodology lessons: corrections applied during the project

A running log of estimation errors caught and the corrected approach. The point: write down what we got wrong so the same class of error doesn't recur.

## 1. The acceptance-vs-matriculation conversion error

**The bug.** When a school publishes an *acceptance* list (admits, not enrollments), early estimates converted those counts to matriculation by stacking two discount factors: a yield factor *and* a separate selection/single-choice factor. Stacking compressed the headline metric tier-by-tier in a way that broke internal consistency.

**Why it was wrong.** A T25 acceptance pool already *contains* the T15 acceptance pool. If you discount each tier independently with different multipliers, you can produce T25 matriculation < T15 matriculation — which is impossible, since T25 is a strict superset of T15.

**The case study — BASIS Independent Fremont.** The school publishes acceptance counts, not matriculations. The stacked-discount approach took 29% T15 acceptance, multiplied through two factors to land at ~16% T15 matriculation, then estimated T25 matriculation at ~22% — implying T25 < T15. Caught during BASIS Fremont review. Corrected to a single yield multiplier per tier; the new T25 estimate is ~32%.

**The correct approach — single yield per tier.**

```
TN_matriculation = TN_acceptance × yield(N)
```

One multiplier. No stacking. The yield itself can vary by tier (broader buckets have lower yield because matriculants are more diffuse), but you apply exactly one factor per tier.

## 2. The subset rule

For every school, the following monotonicity must hold on both acceptance and matriculation counts:

```
T10 ≤ T15 ≤ T25 ≤ T50 ≤ T100
```

This is definitional: T15 is a strict superset of T10, etc. Any row that violates this ordering is a methodology error, not a real-world finding. If you see it, the conversion is wrong — fix the conversion, do not publish the inversion.

## 3. Default yield factors by tier

Use these as defaults when converting school-published acceptance lists to matriculation. Yield declines as the bucket broadens because higher-tier admits cross-admit each other heavily and pick the most-selective option, while lower-tier admits are more diffusely distributed across the bucket.

| Tier | Default yield | Reasoning |
|---|---|---|
| T10 | 0.85 | Cross-admit pool concentrated; admits typically pick the single most-selective option. |
| T15 | 0.85 | Same as T10 — adding 5 more elite schools doesn't materially change yield behavior. |
| T25 | 0.80 | Bucket starts to include large publics (UCB/UCLA/UMich/UVA) where yield is lower. |
| T50 | 0.70 | Many cross-admits trade down to in-state public or merit-aid school outside T50. |
| T100 | 0.60 | Broad bucket; substantial leakage to specific-fit schools (LACs, military, conservatories, in-state). |

These are defaults. If a school publishes both acceptance and matriculation for any tier, prefer the measured ratio over the default.

## 4. Schools known to publish acceptance lists (not matriculation)

This issue is most acute at schools that publish "where students were admitted" rather than "where students enrolled." Currently known:

- **BASIS Independent Fremont** — acceptance-only profile; case study above.
- **Bay School of San Francisco** — acceptance list on profile.
- **Bentley** — acceptance list on profile.
- **Most Catholic college-prep schools** (Bellarmine, Mitty, SI, SHC, St. Francis, De La Salle, Carondelet) — acceptance-style "matriculation highlights."
- Various smaller independents that publish "Class of 20XX college acceptances."

If a school is on this list, the estimator must apply the single-yield conversion before any tier comparison.

## 5. Validation checklist

Three sanity checks to run when adding any new school estimate:

1. **Subset check.** Does T10 ≤ T15 ≤ T25 ≤ T50 hold? If not, your conversion is wrong. Fix before publishing.
2. **Yield-stacking check.** Did you apply more than one discount factor between acceptance and matriculation? If yes, collapse to a single yield per tier.
3. **Plausibility check.** Does T25 % land in the range typical for the school's peer band (see methodology.html section 1b ratio table)? If a school is showing 2× its peer band, double-check the source — likely an acceptance list being read as a matriculation list.

## 6. Yield is school-type dependent

**The bug.** Default yields (Section 3) were applied as a blanket 80% T25 multiplier across all schools. This understated T25 % at STEM-focused affluent secular schools (where almost every T25 admit enrolls — high aspiration, few non-T25 attractions, low cost sensitivity) and overstated it at mid-tier Catholic schools (where many T25 admits opt for Santa Clara / USF / USD instead).

**Why it was wrong.** Yield is a behavioral parameter of the *student population*, not a fixed property of the T25 bucket. A T25 admit at a STEM-focused affluent secular school is much more likely to enroll than a T25 admit at a mid-tier Catholic school where the local Catholic-affiliated alternatives (SCU, USF, USD, LMU) carry strong cultural pull. Treating yield as ~80% across the board systematically biased the metric.

**The corrected yield-by-type table.** Use this in place of the blanket 80% T25 yield (Section 3 still applies as a fallback when school type is unclear):

| School type | T25 yield | Reasoning |
|---|---|---|
| STEM-focused affluent secular (BASIS Fremont, BASIS SV, Quarry Lane, Pinewood, Stanford OHS) | **90%** | High aspiration, few non-T25 attractions, low cost sensitivity. |
| Elite progressive secular (Marin Academy, Urban, Lick-Wilmerding, Bay School, Branson) | **80%** | LAC alternative pulls some T25-admitted students to top LACs instead. |
| Top-tier Catholic (Bellarmine, Mitty, SI, SHC, Saint Francis) | **70%** | Notre Dame loyalty (counts in T25, fine) but Santa Clara / USF / USD pull some T25-admitted students away. |
| Mid-tier Catholic (NDB, Mercy Burlingame, De La Salle, Carondelet, Bishop O'Dowd) | **65%** | More cost sensitivity + religious-school preference; many T25 admits opt for SCU / USF / USD. |
| Top public (Gunn, Paly, MSJ, Lynbrook, etc.) | **80%** | UCB/UCLA/UCSD admits typically taken; some pull to non-T25 UC and CSU. |
| Strong suburban public | **75%** | UC focus, but more cost-driven choices. |

**The case study — BASIS Independent Fremont, second revision.**
- Original (stacked discounts): ~22% T25.
- First revision (single-yield with blanket 80% across the board): ~32% T25.
- Second revision (yield-by-type with 90% for STEM-affluent secular): **~48% T25**.

The first revision fixed the subset-rule violation. The second revision recognized that BASIS Fremont's student body is exactly the population that almost always takes a T25 admit when offered one — STEM-focused, affluent, secular, low cost sensitivity. The 50-55% T25 acceptance rate × 90% yield ≈ 48% matches the school's actual matriculation profile better than the blanket 80% (~32%).

**Sister-school implication.** BASIS Independent Silicon Valley sits in the same type bucket and was previously held at ~25% T25 in the data; the same correction lifted it to ~30% T25 (33% T25 acceptance × 90% yield). Acknowledged in the prior lessons doc but not previously revised — fixed in this pass.

**Other rows touched by this correction.** Quarry Lane (~14% → ~16%), Stanford OHS (~30% → ~32%), Notre Dame HS Belmont (~4% → ~3.5% — moved from blanket 80% to 65% mid-tier-Catholic yield). Bentley and Bay School are elite progressive secular and stayed at the 80% yield, so their T25 % did not change — only their tooltip rationale was updated.

## 7. Lessons applied

Revisions already made:

- **BASIS Independent Fremont:** T25 % corrected from ~22% to ~32% (stacked-discount fix), then to **~48%** (yield-by-type correction).
- **BASIS Independent Silicon Valley:** T25 % corrected from ~25% to **~30%** (yield-by-type correction; sister-school parity with BASIS Fremont).
- **Stanford Online HS:** ~30% → **~32%** (STEM-affluent secular yield 90%).
- **The Quarry Lane School:** ~14% → **~16%** (STEM-affluent secular yield 90%).
- **Notre Dame HS Belmont:** ~4% → **~3.5%** (mid-tier Catholic yield 65%).

Other school-by-school revisions are documented in commit history and `methodology_and_review.md`. The formal rule statement lives in `methodology.html` sections 8 and 9 — this lessons doc is the long-form case study and learning log.
