# WorkComp Risk Radar — Cowork daily-job spec

A daily Cowork job that scans the news, distils emerging-risk signals for the
Australian **workers compensation insurance** landscape — NSW in depth, the other
jurisdictions for awareness — and writes a styled digest that a separate helper
publishes to GitHub Pages.

Same principle as the rest of the system: **the agent writes structured data
(JSON), never HTML.** Styling lives in the scaffold; a native macOS helper does the
git push. This file defines only the domain rules.

> Current context (mid-2026): NSW reform package (Amendment Act 2025 + Reform and
> Modernisation Act 2026) mid-rollout; icare premium target freeze 30 Jun 2026 →
> 30 Jun 2028; SIRA revised Guidelines effective 30 Jun / 1 Jul 2026; psychological
> injury and scheme funding ratio (~85c per $1) the dominant cost story. Interstate:
> WA bedding down its Workers Compensation and Injury Management Act 2023; Victoria's
> mental-injury and scheme-sustainability reforms a live comparator.

---

## 1. Source register (with access status)

### 1a. NSW — PRIMARY focus (cover in full depth)

| Source | Risk lens | Notes |
|---|---|---|
| **SIRA NSW** — news, guidelines, market practice | Scheme & Regulatory | The anchor regulator |
| **icare NSW** (Nominal Insurer) | Premiums, Sustainability | Premium filings, reform updates, results |
| **Personal Injury Commission (PIC)** — decisions | Legal & Case Law | Dispute precedents |
| **NSW Industrial Relations Commission** | Legal & Case Law | New psychological-injury / bullying jurisdiction |
| **SafeWork NSW** | Health & Prevention | WHS, psychosocial, prosecutions |
| **NSW Government / Treasury / Customer Service** | Political & Policy | Ministerial statements, reform releases |
| **IRO / ILARS** (Independent Review Office) | Compliance, Conduct | Worker complaints, insurer conduct |

### 1b. Other states & territories — SECONDARY (see weighting rule, §3)

| Jurisdiction | Body (regulator / insurer) | Scheme model | Disputes |
|---|---|---|---|
| **VIC** | WorkSafe Victoria | WorkSafe-managed agent model (Allianz, CGU, EML, GB, GIO, Xchanging) | Accident Compensation Conciliation Service |
| **QLD** | WorkCover Queensland (insurer); Workers' Compensation Regulator / Office of Industrial Relations | State monopoly + self-insurers | Workers' Compensation Regulator → QIRC |
| **SA** | ReturnToWorkSA | Single statutory (monopoly) insurer | SA Employment Tribunal (SAET) |
| **WA** | WorkCover WA | Privately underwritten (approved insurer list) | WorkCover WA Conciliation & Arbitration |
| **TAS** | WorkSafe Tasmania | Privately underwritten | Workers Rehabilitation & Compensation Tribunal |
| **ACT** | WorkSafe ACT / Access Canberra | Privately underwritten + default insurance fund | ACT Magistrates Court |
| **NT** | NT WorkSafe (Work Health Authority) | Privately underwritten (premiums not regulated) | NT Work Health Court |

All of the above publish news/media releases and (mostly) tribunal decisions on
their own sites — all free.

### 1c. National & cross-jurisdiction (free)

| Source | Risk lens | Notes |
|---|---|---|
| **Safe Work Australia** | Data, Benchmark, Policy | National stats; annual *Comparison of Workers' Compensation Arrangements in Australia and NZ*; model WHS |
| **Heads of Workers' Compensation Authorities (HWCA)** | Cross-scheme trends | Pre-aggregated signal of emerging issues across all schemes |
| **Comcare** | Commonwealth scheme | SRC Act scheme + national self-insurers; comparator decisions |
| **Seacare Authority** | Maritime scheme | Niche but in-scope |
| **APRA** | Capital | Prudential signals for the privately-underwritten markets (WA/TAS/NT/ACT) and licensed insurers |
| **Actuaries Institute** | Sustainability | Cross-scheme commentary |
| **Insurance News** (insurancenews.com.au) | Industry | Free, RSS — national trade |
| **Insurance Business Australia** | Industry | Strong workers-comp coverage, all jurisdictions |
| **Claims service provider bulletins** (EML, Allianz, GIO/Suncorp, DXC, Gallagher Bassett) | Operational, Claims | Operate across multiple schemes |
| **Law-firm insights** (national firms' workers-comp updates) | Legal & Case Law | High-signal on case law — paraphrase only |
| **ABC News / The Guardian Australia** | Political, Reputational | Major scheme/political stories |

### 1d. Paid — headline + public standfirst only, flagged for manual read

| Source | Risk lens | Status |
|---|---|---|
| **Australian Financial Review** | Sustainability, Political, Insurer results | **Paid — you hold access** (§2) |
| **Sydney Morning Herald** | Political, Reputational | **Paid — you hold access** (§2) |
| **The Australian** | Political | Paid — not held |
| **Specialist legal databases** (LexisNexis/Westlaw) | Case Law | Paid/optional — note most tribunal decisions are free |

---

## 2. Paywall & copyright policy (identical to the rest of the system)

- **Free sources:** fetch (RSS-first), summarise in your own words, link out.
- **Paid sources you don't hold:** public headline + standfirst only, `"paywall": true`, link out. Never bypass a paywall.
- **AFR & SMH (held):** headline + standfirst with `"paywall": true`, linked for you to read in your subscription. The agent must not log in or scrape full text. Optional manual augmentation: paste an article's text you've accessed and the agent will summarise that.
- **Always paraphrase. Never reproduce article paragraphs.** Law-firm briefings: summarise the holding/implication in your own words; don't lift.

---

## 3. Relevance filter & jurisdiction weighting

**In scope:** the Australian workers-comp insurance system, any scheme participant,
or insurer risk. Match on: workers compensation, SIRA, icare, Nominal Insurer,
Personal Injury Commission, Industrial Relations Commission, WorkSafe Victoria,
WorkCover Queensland, ReturnToWorkSA, WorkCover WA, WorkSafe Tasmania, WorkSafe ACT,
NT WorkSafe, Comcare, Seacare, Safe Work Australia, HWCA; psychological /
psychosocial injury, premium / target collection rate / premium freeze, Whole Person
Impairment / WPI, weekly payments, work injury damages, reasonable and necessary,
return to work, claims service provider / agent, self-insurer, monopoly insurer,
privately underwritten, scheme sustainability / funding ratio, enforceable
undertaking, under-insurance, excess, experience rating, commutation, exempt workers,
dust diseases / silica, journey claims.

**Jurisdiction weighting:**
- **NSW = primary.** Cover in full depth, all categories.
- **Other jurisdictions = secondary.** Include an item only when it is *materially
  significant*: a scheme reform or guideline change; a landmark tribunal/court
  decision; a scheme-wide premium, funding or sustainability shift; an
  insurer/self-insurer licensing or solvency event; or a major prosecution — **or**
  when it is likely to set a precedent other schemes (including NSW) will follow.
  Skip routine, local, or operational interstate news.
- Default non-NSW items to **`inform`** or **`watch`**; reserve **`act`** for
  developments with direct national or NSW consequence.
- For a non-NSW item, the `so_what` should note any read-across to NSW or national
  implications (e.g. "a likely template NSW stakeholders will cite").
- **Tag every item with its jurisdiction as the FIRST entry in `tags`** — one of
  `NSW`, `VIC`, `QLD`, `SA`, `WA`, `TAS`, `ACT`, `NT`, `Cth`, or `National` — then any
  topical tags (e.g. `["VIC", "Mental injury"]`).

## 4. Risk taxonomy — assign each item exactly one category

1. **Scheme & Regulatory** — guidelines, legislation, reform commencement (any scheme)
2. **Claims & Liability** — claims trends, psychological-injury volumes/costs, large claims
3. **Premiums & Pricing** — filings, freezes, affordability, experience rating, excess
4. **Legal & Case Law** — tribunal / court decisions, precedents, common law
5. **Scheme Financial Sustainability** — funding ratio, deficit, insurer results, reserves
6. **Health, Return-to-Work & Provider** — RTW outcomes, medical/allied health, treatment rules
7. **Compliance, Fraud & Conduct** — under-insurance, enforceable undertakings, insurer conduct, audits
8. **Political, Capital & Reinsurance** — political contest, APRA capital, reinsurance, macro

## 5. Severity — assign exactly one

- `"act"` — material and time-sensitive for the risk function; warrants a decision/response now.
- `"watch"` — developing; could escalate; monitor.
- `"inform"` — contextual; situational awareness only.

Reserve `act` for genuinely material, time-sensitive signals; most items are watch/inform (and most non-NSW items are inform).

## 6. Writing rules

- Paraphrase everything; never reproduce source sentences.
- `headline`: plain rewritten one-liner. `summary`: 1–2 sentences, own words.
- `so_what`: 1–2 sentences naming the risk implication (and NSW/national read-across for interstate items).
- Deduplicate across sources and against the previous 3 days' digests.
- Never fabricate; every item needs a real source name and URL. Empty day → publish empty sections and say so.

## 7. Output — same schema and mechanics as the renewable-energy digest

Write `data/digests/<TODAY>.json` (YYYY-MM-DD, Australia/Sydney):

```jsonc
{
  "date": "2026-06-29",
  "generated_at": "2026-06-29T06:02:00+10:00",
  "posture": "One-line risk posture.",
  "summary": "2–3 sentence executive overview.",
  "counts": { "act": 0, "watch": 0, "inform": 0 },
  "sections": [
    { "category": "Scheme & Regulatory",
      "items": [
        { "severity": "act", "headline": "…", "summary": "…", "so_what": "…",
          "tags": ["NSW", "Psychological injury"], "source": "SIRA NSW",
          "url": "https://…", "published": "2026-06-28", "paywall": false }
      ] }
  ]
}
```

The renderer reads the `tags` array (jurisdiction first). Then update
`data/manifest.json`: if today's date is already the top entry, refresh it in place;
otherwise prepend `{ date, file, posture, counts }` (newest first), leaving older
entries untouched. Validate both files parse. Do **not** run git; the LaunchAgent
helper publishes.
