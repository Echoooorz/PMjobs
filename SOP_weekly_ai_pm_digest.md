# SOP: Weekly AI PM Hiring Digest

## Purpose

Generate a **Weekly AI PM Hiring Digest** that surfaces high-paying senior/staff/principal product manager jobs in AI, provides market statistics, identifies trending skills, and recommends how to demonstrate those skills — tailored to the user's preferences.

The digest also includes:
1. A **complete listing of all open roles** that meet the target criteria (not just summaries — every qualifying role with direct links)
2. A **personalized analysis** for an Applied AI PM (recommendation, search, ads ranking) with 3 years of PM experience post top-MBA, including competitiveness assessment and actionable advice

---

## Prerequisites

- Kiro CLI session with access to:
  - `remote_web_search` (web search tool)
  - `webFetch` (URL content fetching)
  - `fsWrite` / `fsAppend` (file creation)
- Output file: `Projects/JobPostings/weekly_ai_pm_hiring_digest.md`

---

## Target Profile

| Dimension | Criteria |
|-----------|----------|
| **Seniority** | Senior, Staff, Principal Product Manager |
| **Compensation** | Base salary ≥ $200K |
| **Location** | California (any city) OR Remote (US) |
| **Company Type 1** | Prestige companies — top talent would choose this company over other offers |
| **Company Type 2** | Startups with strong investors (Tier 1 VCs) or notable founders |
| **Company Type 3** | Companies whose PM teams include alumni from top tech companies |
| **Domain** | AI, ML, LLM, Agentic AI, GenAI, Recommendation Systems |

---

## User Profile (for Personalized Analysis)

| Dimension | Detail |
|-----------|--------|
| **Current Role** | Applied AI Product Manager |
| **Domain Expertise** | Recommendation systems, Search ranking, Ads ranking |
| **PM Experience** | 3 years post-MBA |
| **Education** | Top MBA program |
| **Typical Level** | Senior PM (L5–L6 equivalent) |
| **Target Level** | Senior / Staff PM at prestige companies; could stretch to Principal at smaller companies or startups |

### Competitiveness Baseline

This profile is used in Step 5.7 and Step 5.8 to generate personalized analysis. The assessment should account for:

- **Strengths**: Applied AI domain expertise (rec systems, search, ads) is rare and highly valued; top MBA signals structured thinking and business acumen; 3 years of shipping AI products is substantive
- **Gaps to assess each week**: How many roles require >5 years PM experience? How many require people management? How many require foundation model (LLM) experience vs traditional ML? How many are at a level above the user's current level?
- **Advice framework**: For each gap identified, provide specific, actionable advice — not generic "get more experience" platitudes

---

## Step 1 — Determine the Digest Period

### Rules

- Period = **7 calendar days** (Monday–Sunday)
- Period ends on the **most recent Sunday** (or today if Sunday)
- Period starts on the **Monday** of that same week

### Calculation

```
end_date   = most recent Sunday ≤ today
start_date = end_date − 6 days (the Monday of that week)
```

### Validation

1. Check the previous digest file for its date range
2. Confirm `start_date` = previous digest end date + 1 day
3. If there is a gap, note it in the digest header

---

## Step 2 — Gather Job Market Data

### 2.1 Search Queries

Execute the following web searches to gather current data. Adapt query terms if results are thin.

| # | Search Query | Purpose |
|---|-------------|---------|
| 1 | `senior principal product manager AI jobs California 2026 salary $200K+` | Core job listings |
| 2 | `top tech companies hiring product managers AI ML {year}` | Prestige company hiring activity |
| 3 | `AI startup hiring product manager {year} Series B C funding` | Well-funded startup roles |
| 4 | `OpenAI Anthropic Google Meta product manager jobs {month} {year}` | Foundation model company roles |
| 5 | `AI product manager skills {year} LLM agents agentic hiring trends` | Skills & trends analysis |
| 6 | `AI product manager salary compensation {year}` | Compensation benchmarks |
| 7 | `site:lever.co OR site:greenhouse.io "product manager" AI California $200K` | Direct ATS listings |
| 8 | `site:linkedin.com/jobs "senior product manager" AI recommendation search California` | LinkedIn role-specific listings |
| 9 | `{company_name} careers product manager` (for each Tier 1 company) | Direct career page scrape |
| 10 | `product manager AI ads ranking personalization jobs California remote 2026` | Applied AI PM domain-specific roles |

### 2.2 Source Priority

Prioritize data from these sources (in order):

1. **Job boards**: Indeed, LinkedIn, Built In, Levels.fyi, Glassdoor
2. **Startup trackers**: YC Work at a Startup, Funded & Hiring, Wellfound
3. **Salary data**: Levels.fyi, ideaplan.io, Glassdoor, Blind
4. **Trend analysis**: Substack newsletters (Lenny's, NeonNook), Medium, industry blogs
5. **Company career pages**: OpenAI, Anthropic, Google, Meta, Scale AI, etc.

### 2.3 Data to Collect

For each relevant job posting or data point, capture:

| Field | Description |
|-------|-------------|
| Company | Company name |
| Role Title | Exact job title |
| Level | Senior / Staff / Principal / Director |
| Base Salary | Listed base or estimated range |
| Total Comp | If available (base + bonus + equity) |
| Location | City, State or "Remote" |
| Company Type | Prestige / Well-Funded Startup / Foundation Model |
| Funding | For startups: round, amount, valuation, lead investors |
| Key Skills | Top 3–5 skills mentioned in the JD |
| URL | Link to the job posting |
| YoE Required | Years of PM experience required (extract from JD) |
| People Management | Yes / No / Not specified |
| AI Sub-Domain | LLM/GenAI, Recommendation, Search, Ads, Platform, Infra, Safety, Other |
| Fit Score | High / Medium / Low — based on match to User Profile (see Step 5.7) |

---

## Step 3 — Classify Companies

### 3.1 Prestige Company Criteria

A company qualifies as "prestige" if it meets ANY of:

| Criterion | Examples |
|-----------|---------|
| FAANG+ / Magnificent 7 | Google, Apple, Amazon, Meta, Microsoft, NVIDIA, Tesla |
| Top-tier tech | Stripe, Databricks, Snowflake, Figma, Notion, Airbnb, Uber, Netflix |
| Foundation model leaders | OpenAI, Anthropic, Google DeepMind, xAI, Mistral, Cohere |
| Market cap > $50B with strong AI investment | ServiceNow, Salesforce, Adobe, Intuit, Palantir |

### 3.2 Well-Funded Startup Criteria

A startup qualifies if it meets ANY of:

| Criterion | Threshold |
|-----------|-----------|
| Total funding | ≥ $100M |
| Valuation | ≥ $1B (unicorn) |
| Lead investors | Tier 1 VCs: Sequoia, a16z, Founders Fund, Benchmark, Lightspeed, Thrive, Accel, Index, Greylock |
| Founders | Ex-C-suite from FAANG+, notable repeat founders, or domain experts with strong track records |

### 3.3 PM Alumni Signal

Flag companies where current/recent PMs came from top companies. Check via:
- LinkedIn company page → People → Filter by "Product Manager" + past company
- Levels.fyi company profiles
- Blind company threads

---

## Step 4 — Analyze Skills & Trends

### 4.1 Skills Extraction

From the collected job postings, tally the frequency of each skill/requirement mentioned. Group into categories:

| Category | Example Skills |
|----------|---------------|
| **AI/ML Technical** | LLM product development, RAG, fine-tuning, prompt engineering, model evaluation, embeddings |
| **Agentic AI** | Multi-agent systems, agent orchestration, autonomous workflows, tool use |
| **Product Craft** | AI-native UX, probabilistic output design, trust & safety, responsible AI |
| **Data & Experimentation** | A/B testing AI features, evaluation metrics, data pipeline design, feedback loops |
| **Leadership** | Cross-functional AI leadership, research-to-production bridge, stakeholder management |
| **Technical Hands-On** | Python, prototyping, technical writing, system design |

### 4.2 Trend Identification

Read all archived digests from `Projects/JobPostings/archive/` before performing trend analysis. Compare this week's data against multiple time horizons:

- **vs last week**: New skills, roles gained/lost, comp changes
- **vs 4 weeks ago (1 month)**: Skills rising/declining in frequency, company hiring patterns
- **vs 12 weeks ago (3 months)**: Market direction (expanding/contracting), major skill shifts, fit trend for user profile
- **vs 24 weeks ago (6 months)**: Long-arc narrative, skill evolution, comp trajectory

Specific signals to track:

- New skills appearing for the first time
- Skills growing in frequency (>20% week-over-week)
- New companies entering the hiring market
- Compensation shifts
- Location/remote policy changes
- Changes in % of roles matching user's domain (rec/search/ads)
- Changes in % of roles requiring LLM vs traditional ML experience

---

## Step 5 — Build the Digest

### 5.1 Document Structure

The digest follows this fixed structure:

```
# Weekly AI PM Hiring Digest
**Week of {start MM/DD} – {end MM/DD}, {YYYY}**

## 📊 Market Snapshot              ← Key stats table
## 📋 All Open Roles               ← Complete listing of every qualifying role
## 🏢 Prestige Companies Hiring    ← Tier 1, 2, 3 company tables
## 🔥 Top Skills in Demand         ← Ranked skills table with frequency
## 📈 Trends This Week             ← 3–5 bullet trend analysis
## 📉 Historical Trends            ← 1-week, 1-month, 3-month, 6-month comparisons
## 🎯 Skills → Experience Map      ← How to demonstrate each skill
## 🧭 Applied AI PM Analysis       ← Personalized assessment for user profile
## 🔗 Job Board Quick Links        ← Curated links
```

### 5.2 Market Snapshot Table

| Metric | How to Calculate |
|--------|-----------------|
| Open PM roles globally | From job market reports (pooya.blog, Built In) |
| AI-specific PM postings growth | YoY or vs 2024 baseline |
| AI PM salary premium | Compare AI PM median vs generalist PM median |
| AI PM median total comp | From salary aggregators |
| AI PM base salary range (Senior+) | From job postings collected |
| Principal PM roles in California | From Indeed/LinkedIn count |
| YC AI startups hiring (SF Bay) | From ycombinator.com/companies |

### 5.3 Company Tables

#### Tier 1: Foundation Model / FAANG+

```
| Company | Open PM Roles | Location | Notable |
```

#### Tier 2: Top Tech & Scale-Ups

```
| Company | Open PM Roles | Location | Notable |
```

#### Tier 3: Well-Funded AI Startups

```
| Company | Funding | Valuation | Hiring For |
```

### 5.4 Skills Table

```
| Rank | Skill | Frequency | What It Means |
```

- Rank by frequency across all collected JDs
- Include top 10 skills
- "What It Means" = 1-sentence explanation of what the skill looks like in practice

### 5.5 Skills → Experience Map

```
| Skill They Want | PM Experience / Past Projects That Demonstrate It |
```

- For each of the top 10 skills, provide 2–3 sentences describing what kind of PM experience or past projects would demonstrate competency
- Be specific and actionable — not generic advice

### 5.6 Trends Section (with Historical Analysis)

Before writing trends, **read all archived digests** in `Projects/JobPostings/archive/` to build historical context.

#### 5.6.1 Weekly Trends (This Week vs Last Week)

- 3–5 numbered bullets
- Each trend = 2–3 sentences max
- Focus on what changed THIS week vs the previous week
- If this is the first digest, compare against general 2025→2026 trajectory

#### 5.6.2 Historical Trend Summary

After the weekly trends, include a **multi-horizon trend summary** that compares the current week against 1-month, 3-month, and 6-month baselines.

##### Data to Track Across Digests

For each archived digest, extract and compare these metrics:

| Metric | How to Compare |
|--------|---------------|
| Total qualifying roles found | Count trend over time |
| % of roles that are 🟢 High Fit | Is the market getting better or worse for this profile? |
| Top 3 skills by frequency | Which skills are rising, stable, or declining? |
| Median base salary (Senior AI PM) | Comp trending up, flat, or down? |
| % of roles requiring LLM/GenAI experience | How fast is the LLM shift happening? |
| % of roles requiring agentic AI | New skill — how fast is it growing? |
| % of roles that are remote-eligible | Remote trend direction |
| Top hiring companies | Who's consistently hiring vs one-time postings? |
| New companies entering the market | First-time posters this week |

##### Output Format

```
### 📉 Historical Trends

#### 1-Week Delta (vs previous week)
- Roles: {N} this week vs {N} last week ({+/-X%})
- High Fit roles: {n} vs {n} ({+/-})
- Notable: {1-sentence on biggest change}

#### 1-Month Trend (4-week rolling)
- Average roles/week: {N} (trend: ↑/↓/→)
- Skills rising: {skill1} ({X%} → {Y%}), {skill2}
- Skills declining: {skill1} ({X%} → {Y%})
- Comp trend: {direction} ({median 4 weeks ago} → {median now})

#### 3-Month Trend (12-week rolling)
- Market direction: {expanding / contracting / stable}
- Biggest shift: {1-sentence, e.g., "Agentic AI went from 30% to 78% of JDs"}
- Your fit trend: {improving / declining / stable} — {1-sentence why}
- Companies that hired consistently: {list top 3-5}

#### 6-Month Trend (24-week rolling, when available)
- Market narrative: {2-3 sentences summarizing the half-year arc}
- Skill evolution: {what was hot 6 months ago vs now}
- Comp trajectory: {base salary movement over 6 months}
- Strategic takeaway: {1-sentence advice based on the long-term trend}
```

##### Handling Missing History

| Archived Digests Available | What to Generate |
|---------------------------|-----------------|
| 0 (first edition) | Weekly trends only; note "First edition — no historical baseline" |
| 1–3 digests | Weekly delta + partial 1-month trend; note limited data |
| 4+ digests | Weekly delta + full 1-month trend |
| 12+ digests | Weekly + 1-month + 3-month trends |
| 24+ digests | All four horizons (1-week, 1-month, 3-month, 6-month) |

### 5.7 All Open Roles (Complete Listing)

This section lists **every individual role** that meets the target criteria — not aggregated by company, but one row per open position.

#### Table Format

```
| # | Company | Role Title | Level | Base Salary | Location | AI Sub-Domain | Fit Score | Link |
```

#### Column Definitions

| Column | Content |
|--------|---------|
| **#** | Sequential number |
| **Company** | Company name with company type tag: `[FM]` Foundation Model, `[F+]` FAANG+, `[T2]` Top Tech, `[SU]` Startup |
| **Role Title** | Exact job title from the posting |
| **Level** | Senior / Staff / Principal / Director |
| **Base Salary** | Listed range or estimated range (mark estimated with `*`) |
| **Location** | City, CA or "Remote US" |
| **AI Sub-Domain** | Recommendation, Search, Ads, LLM/GenAI, Agentic, Platform, Infra, Safety, General AI |
| **Fit Score** | 🟢 High / 🟡 Medium / 🔴 Low — see Fit Score rubric below |
| **Link** | Direct URL to the job posting |

#### Fit Score Rubric (based on User Profile)

| Score | Criteria |
|-------|----------|
| 🟢 **High** | Role is Senior PM level; requires 3–5 years PM experience; domain matches (rec/search/ads); no people management required; California or Remote |
| 🟡 **Medium** | Role is Staff/Senior level; requires 5–7 years OR domain is adjacent (e.g., LLM platform, personalization); may prefer but not require people management |
| 🔴 **Low** | Role is Principal/Director; requires 8+ years OR requires extensive people management; domain is distant (e.g., AI safety, robotics, hardware) |

#### Sorting

1. Sort by Fit Score (🟢 first, then 🟡, then 🔴)
2. Within each score tier, sort by base salary descending

#### Completeness Requirement

- **Do not summarize or aggregate.** Every qualifying role gets its own row.
- If a company has 3 open PM roles that qualify, list all 3 as separate rows.
- Target: capture **all roles findable** through the search queries in Step 2.1. Acknowledge if search coverage is incomplete.
- Include a count summary at the top: `**{N} roles found this week** (🟢 {n} High Fit | 🟡 {n} Medium | 🔴 {n} Low)`

### 5.8 Applied AI PM Analysis (Personalized)

This section provides a candid, personalized assessment for the user based on their profile (see User Profile section). It is the most opinionated section of the digest.

#### Structure

```
## 🧭 Applied AI PM Analysis
*For: Applied AI PM (Rec/Search/Ads) · 3 years post top-MBA · Targeting Senior/Staff roles*

### Your Market Position This Week
### Where You're Strongest
### Where You'll Face Headwinds
### Roles to Prioritize This Week
### Competitiveness Advice
```

#### 5.8.1 Your Market Position This Week

A 3–4 sentence summary answering: "Given this week's open roles, how competitive is this profile?" Include:

- What % of roles are realistic targets (🟢 High Fit)
- How the user's domain (rec/search/ads) maps to current demand
- Whether the market is trending toward or away from this profile

#### 5.8.2 Where You're Strongest

Bullet list of 3–5 specific advantages this profile has in the current market. Be concrete:

- ✅ Which specific open roles this week are a strong match and why
- ✅ Which skills from the user's domain (rec systems, search ranking, ads) are in high demand
- ✅ How the top-MBA + applied AI combo positions against other candidates

#### 5.8.3 Where You'll Face Headwinds

Bullet list of 3–5 specific challenges. Be honest and specific:

- ⚠️ Which roles require more experience than the user has (and by how much)
- ⚠️ Which roles require LLM/GenAI experience that traditional ML rec/search PMs may lack
- ⚠️ Level gaps: which roles are Staff/Principal where the user is Senior-level
- ⚠️ People management requirements the user may not yet have
- ⚠️ Domain gaps: e.g., if most roles this week are in agentic AI vs recommendation systems

#### 5.8.4 Roles to Prioritize This Week

Pick the **top 5 roles** from the All Open Roles table that are the best fit for this specific profile. For each:

```
| Priority | Company | Role | Why This One |
```

- "Why This One" = 1–2 sentences explaining why this role is a strong match for the user's specific background

#### 5.8.5 Competitiveness Advice

3–5 numbered, actionable recommendations. Each should be:

- **Specific to this week's data** — not generic career advice
- **Tied to a gap identified in 5.8.3** — each piece of advice should address a specific headwind
- **Actionable within 1–4 weeks** — not "get 5 more years of experience"

Example format:
```
1. **[Gap]: Most roles want LLM shipping experience, not just traditional ML.**
   → [Action]: Build a side project shipping a RAG-based product (e.g., internal search tool).
   Document the evaluation framework you used. This bridges the rec-systems-to-LLM gap
   that 60% of this week's roles are looking for.
```

#### Tone

- Be direct and honest, not encouraging-but-vague
- Quantify where possible ("7 of 23 roles this week require 5+ years")
- Name specific companies and roles when giving advice
- Acknowledge when the user is well-positioned — don't manufacture gaps

---

## Step 6 — Write the Output File

### 6.1 File Location

```
Projects/JobPostings/weekly_ai_pm_hiring_digest.md
```

### 6.2 Overwrite Policy

- Each week's digest **overwrites** the previous file
- Archive the previous digest before overwriting into `Projects/JobPostings/archive/`:
  ```
  Projects/JobPostings/archive/weekly_ai_pm_hiring_digest_{YYYY-MM-DD}.md
  ```
- Create the `archive/` directory if it doesn't exist
- **Do not delete archives** — they are the data source for historical trend analysis (Step 5.6.2)
- Archives older than 6 months may be summarized into a `trend_history.md` file and removed to save space

### 6.3 Footer

Always include a sources footer:

```
*Sources: {list sources used}. Content was rephrased for compliance with licensing restrictions.*
```

---

## Step 7 — Validation Checklist

Before finalizing:

- [ ] Digest period is correct and noted in the header
- [ ] All jobs listed have base salary ≥ $200K (or estimated equivalent)
- [ ] Location filter applied: California or Remote US only
- [ ] Company classification is accurate (Prestige / Startup / Foundation Model)
- [ ] Startup entries include funding details (round, amount, investors)
- [ ] **All Open Roles table is complete** — every qualifying role has its own row
- [ ] **All Open Roles count summary** matches actual row count
- [ ] **Fit Scores assigned** to every role using the rubric
- [ ] **Roles sorted** by Fit Score then salary within each tier
- [ ] Skills table has ≥ 10 entries ranked by frequency
- [ ] Skills → Experience map covers all top 10 skills
- [ ] Trends section has 3–5 bullets with specific observations
- [ ] **Historical Trends section** includes all applicable horizons based on archive depth
- [ ] **Archived digests were read** before generating trends (confirm archive count in digest)
- [ ] **Applied AI PM Analysis** includes all 5 subsections (Position, Strengths, Headwinds, Priorities, Advice)
- [ ] **Top 5 Roles to Prioritize** are selected from the All Open Roles table with specific reasoning
- [ ] **Competitiveness Advice** has 3–5 items, each tied to a specific gap and actionable within 1–4 weeks
- [ ] Job board quick links are functional URLs
- [ ] Sources footer is present
- [ ] No PII (recruiter names, personal emails) included
- [ ] Previous digest archived before overwrite

---

## Edge Cases

| Scenario | Action |
|----------|--------|
| Fewer than 5 qualifying jobs found | Expand search to include $180K+ base or add "Staff PM" queries |
| No salary listed in posting | Estimate using Levels.fyi or Glassdoor data for that company + level; note as "estimated" |
| Startup funding data unavailable | Check Crunchbase, PitchBook, or Funded & Hiring; if still unavailable, note as "undisclosed" |
| Company is borderline prestige | Include with a note explaining why (e.g., "Series D, $2B valuation, Sequoia-backed") |
| Duplicate job across multiple boards | Deduplicate by company + role title; link to the company's career page |
| Remote role restricted to specific states | Include only if California is in the allowed state list |
| Previous digest not found | Generate without trend comparison; note "First edition — no prior baseline" |
| All roles are 🔴 Low Fit | Note this explicitly in the Applied AI PM Analysis; expand advice section to focus on bridging gaps; suggest adjacent roles that could build toward target roles |
| Fewer than 5 🟢 High Fit roles | Include 🟡 Medium Fit roles in the "Roles to Prioritize" section with notes on what would need to be true for the user to be competitive |
| User's domain (rec/search/ads) has zero matching roles this week | Flag as a trend signal; advise on whether to broaden domain or wait; compare against previous weeks |
| Role requires skills the user likely has but JD doesn't name them | Note in Fit Score rationale (e.g., "JD says 'ML ranking' — your ads ranking experience directly applies") |

---

## Appendix: Reference Sources

| Source | URL | Data Type |
|--------|-----|-----------|
| Indeed (Principal PM, CA) | `indeed.com/q-principal-product-manager-l-california-jobs.html` | Job listings |
| Built In (Remote AI PM) | `builtin.com/jobs/remote/product/artificial-intelligence` | Job listings |
| YC Startups Hiring | `ycombinator.com/companies/industry/ai/san-francisco-bay-area/hiring` | Startup jobs |
| Funded & Hiring | `fundedandhiring.com` | Startup funding + hiring |
| Levels.fyi | `levels.fyi` | Compensation data |
| ideaplan.io | `ideaplan.io/product-manager-salary/ai-product-manager` | AI PM salary benchmarks |
| OpenAI Careers | `openai.com/careers/search/` | Direct listings |
| Anthropic Careers | `anthropic.com/careers/jobs` | Direct listings |
| Scale AI Careers | `scale.com/careers` | Direct listings |
| NeonNook (Skills Analysis) | `neonnook.substack.com` | Skills trend analysis |
| pooya.blog (Market Report) | `pooya.blog/blog/state-product-job-market-early-2026/` | Market statistics |

---

## Cadence

| Item | Schedule |
|------|----------|
| Digest generation | Every **Monday** |
| Data freshness | Searches executed at generation time (no caching) |
| Archive retention | Keep **all** archives (needed for 6-month trend analysis) |
| Trend comparison window | 1-week, 1-month (4 weeks), 3-month (12 weeks), 6-month (24 weeks) |
| Historical read | Before each generation, read all files in `Projects/JobPostings/archive/` |
