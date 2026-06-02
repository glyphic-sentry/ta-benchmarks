# Credibility Criteria for Recruiting Benchmark Reports

When Claude discovers a new report during Phase 1c (discovery) or the weekly
automated update, use these criteria to decide whether it belongs in the
knowledge base. The goal is a high-quality, trustworthy library — not an
exhaustive one.

---

## Required Criteria (all must be met)

**1. Clear publisher with industry standing**
The report must come from a named organization with a plausible reason to
collect this data: an ATS or recruiting platform, a professional association
(SHRM, ATAP, REC), a research firm (Gartner, Forrester, McKinsey), a
staffing firm (Korn Ferry, Spencer Stuart), or a credible media outlet
(Harvard Business Review with data, Bloomberg with original survey).

Not credible: anonymous blog posts, single-person newsletters presenting "data",
consulting firms with no disclosed methodology, vendor content with no sourced
stats.

**2. Quantitative data, not just opinion**
The report must contain actual numbers — percentages, medians, averages, rates,
counts — not just expert opinions or trend narratives without data behind them.

**3. Disclosed sample**
The report must state or strongly imply how data was collected (survey, ATS
aggregate, job posting analysis) and at minimum hint at scale (e.g., "hundreds
of companies", "50,000 job postings"). Reports that present numbers with
absolutely no methodology context should be treated with caution and noted as
such.

**4. Published within the last 3 years**
Recruiting benchmarks shift quickly. Reports older than 3 years should not be
added unless they are foundational (e.g., a methodology paper) or explicitly
requested by the user. Exception: if the user wants to build a YoY trend going
back further, older reports from the same publisher may be added.

**5. Relevant to TA and recruiting**
The report must be meaningfully about talent acquisition, recruiting, sourcing,
candidate experience, or workforce planning. Adjacent HR topics (benefits,
L&D, performance management) are acceptable if they contain TA-relevant data.
General business reports with only passing mentions of hiring do not qualify.

---

## Quality Signals (nice to have, not required)

- **Sample size stated explicitly** (e.g., "1,200 recruiters across 14 countries")
- **Data segmented by company size, industry, or role level**
- **Published on a recurring annual basis** (signals the publisher takes it seriously)
- **Cited by other credible sources** (e.g., if three other reports cite this one)
- **Peer-reviewed or produced with an academic partner**

---

## Disqualifying Signals

Exclude any report that:
- Is clearly a marketing piece with cherry-picked stats and no methodology
- Presents a sample of < 50 (too small to generalize)
- Is from a vendor with an obvious financial interest in the specific stat
  (e.g., a sourcing tool reporting that "sourcing is the #1 channel") and no
  third-party validation
- Cannot be fetched or accessed even at the summary level
- Is a press release, not a report

---

## Borderline Cases

When a report meets some but not all criteria, add it with a clear caveat in
the markdown file:

```markdown
## ⚠️ Credibility Note
This report does not disclose its sample size methodology. Stats should be
treated as directional indicators rather than authoritative benchmarks.
```

Always tell the user when a borderline report is added and why you decided
to include it.

---

## Examples

| Report | Include? | Reason |
|--------|----------|--------|
| Ashby Talent Trends 2024 | ✅ Yes | Known ATS, large sample, annual, full methodology |
| Recruiter on LinkedIn shared "5 stats I noticed" | ❌ No | No methodology, no publisher standing |
| Gartner HR Survey 2023 (3 years old) | ⚠️ Borderline | Credible publisher but approaching age limit — include with year caveat |
| HireRight Background Check Survey | ✅ Yes | Named publisher, quantitative, TA-adjacent |
| McKinsey "Future of Work" report | ⚠️ Borderline | Credible but broad — include only if it has TA-specific stats |
| Random SaaS company blog: "We analyzed 1M job postings" | ⚠️ Borderline | Depends on methodology disclosure — add with caveat if data is interesting |
