# Findings

Analysis of 1,000 healthcare claims, comparing three independent status-tracking fields and
quantifying revenue impact by denial reason.

---

## 1. The three status fields do not agree with each other

**Observed.** Every claim carries three separate status indicators — Claim Status, Outcome,
and AR Status — each presumably maintained to answer "was this claim denied?" 435 of 1,000
claims (43.5%) show Claim Status and Outcome in direct disagreement: one field says "Denied,"
the other does not.

**Shape of the disagreement.**

| Field | Denial rate | Categories used |
|---|---:|---:|
| Claim Status | 32.8% | 3 |
| Outcome | 33.1% | 3 |
| AR Status | 15.7% | 6 |

Claim Status and Outcome land close to each other by coincidence of scale — both split claims
across three roughly equal buckets. AR Status uses six categories, so "Denied" competes against
five other buckets instead of two, which mechanically halves its apparent share. The three
fields are not measuring disagreement at random; they are built on incompatible category
schemes.

**Interpretation.** This is the signature of disconnected systems: a denial-management system,
a claims-adjudication system, and an accounts-receivable system, each recording its own view of
the same claim without reconciling against the others. None of the three fields is "wrong" in
isolation — each is internally consistent — but none of them alone answers "what is our denial
rate" in a way a second system would confirm.

**Conclusion.** Any report built from a single status field will misstate the organisation's
true denial rate, and the direction of the error is not predictable without checking the other
two fields.

---

## 2. The costliest denial reason is not simply the most common one

**Observed.** "Incorrect billing information" is the leading denial reason on every measure
that was checked — 52 claims (the highest count), ₹16,740 in denied revenue (17.4% of all
denied revenue), and the highest average claim value of any denial reason at ₹321.92.

| Reason | Denied claims | Denied revenue | Avg. claim value |
|---|---:|---:|---:|
| Incorrect billing information | 52 | ₹16,740 | ₹321.92 |
| Lack of medical necessity | 38 | ₹12,157 | ₹319.92 |
| Service not covered | 43 | ₹12,093 | ₹281.23 |
| Patient eligibility issues | 45 | ₹11,672 | ₹259.38 |
| Duplicate claim | 41 | ₹11,631 | ₹283.68 |
| Pre-existing condition | 42 | ₹11,456 | ₹272.76 |
| Missing documentation | 37 | ₹11,353 | ₹306.84 |
| Authorization not obtained | 33 | ₹9,055 | ₹274.39 |

**Interpretation.** Volume and dollar impact don't always point the same direction — a reason
could be common but cheap, or rare but expensive. Here they compound: "Incorrect billing
information" is both the most frequent and the most expensive per incident, which is what
makes it the largest single contributor to denied revenue rather than a tie between several
reasons.

**Why it matters.** Unlike "Lack of medical necessity" or "Pre-existing condition" — which stem
from clinical or coverage disputes outside a billing team's direct control — "Incorrect billing
information" is an administrative error. It is, in principle, the most fixable driver of
denied revenue on this list.

**Conclusion.** Prioritising denial-reduction effort by claim count alone would still surface
this reason, but prioritising by revenue impact confirms it, and adds that each individual
error here is also disproportionately costly — a second, independent reason to address it
first.

---

## Summary

| Finding | Type | Action |
|---|---|---|
| Claim Status / Outcome disagree on 43.5% of claims | Data governance | Reconcile the two fields before trusting either for reporting |
| AR Status denial rate diverges structurally (15.7% vs ~33%) | Measurement defect | Normalise category schemes across systems before comparing |
| "Incorrect billing information" leads on both count and revenue | Diagnostic | Highest-priority denial reason to address |
| It also carries the highest average claim value | Diagnostic | Confirms priority independent of volume |

**The most useful number here was not the denial rate.** 32.8%, 33.1%, or 15.7% — three
answers to what should be one question — is what exposed the real problem: the systems don't
agree, and no single-field report would have surfaced that on its own.
