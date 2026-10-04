# Six SEC filing-text theses survive scrutiny, unevenly

Published research supports at least six investable theses for a fund that reads SEC filings with LLMs, but the evidence quality is lopsided: the best-documented effects live in short, event-like filings (8-K non-reliance and auditor-change items, Form 4 insider trades, Schedule 13D activist filings), where text adds value by sub-typing a known event, while the purely narrative theses (10-Q risk-factor updates, abnormal tone in earnings releases, SEC comment-letter severity) rest on pre-2015 samples, unpublished or summary-level effect sizes, and in two cases documented decay or failed large-cap replication. Concretely, Item 4.02 non-reliance 8-Ks produce cumulative abnormal returns of −2.6% to −5.4% across 8,006 filings 2004–2023, with revenue-recognition errors and uncertain impact language amplifying the reaction two- to three-fold (abstract-level) ([Schroeder 2025](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5118253)); opportunistic insider purchases earn 82 bp/month value-weighted ([Cohen, Malloy & Pomorski 2012](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1540-6261.2012.01740.x)); activist 13D filings earn a ~7% announcement return that the SEC's own 2011–2021 staff sample still finds at 5.7%–17.2% depending on accumulation status ([SEC Release 33-11253](https://www.sec.gov/files/rules/final/2023/33-11253.pdf)). Against that, "Lazy Prices" 10-K similarity delivers −0.92%/yr on the S&P 100 in a 2009–2026 replication ([iqueipopg/lazy-prices](https://github.com/iqueipopg/lazy-prices)), dictionary tone stopped explaining filing returns outside the original Loughran–McDonald sample window ([Frankel, Jennings & Lee 2022](https://pubsonline.informs.org/doi/10.1287/mnsc.2021.4156)), and firms demonstrably rewrite filings to game machine readers ([Cao et al. 2023](https://www.nber.org/system/files/working_papers/w27950/w27950.pdf)). The LLM's defensible edge is measurement, not oracle forecasting: segmenting items reliably, classifying footnotes and event subtypes with quote-grounded output, and compressing bloated narrative. A full annual pass over every 10-K, 10-Q, 8-K, Form 4 and 13D/13G is roughly 1.5–3.5 billion input tokens, on the order of $10k–$40k at 2026 list prices, so model cost is not the constraint; look-ahead bias, EDGAR acceptance-time alignment, small-cap capacity and the absence of any post-2020 replication for most text theses are.

## How to read this report and its sourcing caveats

Every claim below traces to the research notes compiled for this project, and those notes carry a material constraint: the research environment could read sec.gov documents in full (the SEC's 2020 Item 105 release, the 2022 10b5-1 release, the 2023 13D/13G release, Form 8-K and Form 4 instructions, the Filzen–McBrayer–Shannon 10-Q paper lodged in an SEC comment file, and the Kim–Muhn–Nikolaev 2024 working paper via a mirror), but SSRN, NBER, Wiley, Elsevier, Springer and most university hosts were blocked. Where an effect size therefore comes from a search-engine extract or an aggregator rather than the paper's tables, this report says so explicitly with "(per search extract)" or "(summary-level)". Those figures should be re-verified against the primary tables before any capital decision, and the specific tables to pull are named where the notes identified them.

The report presents six theses as a numbered list so they can be scanned, each with (1) the thesis, (2) the supporting research with authors, year, venue, sample and effect sizes plus replication, decay and contrary evidence, (3) the exact filings, sections, exhibits, timing and data-access details, and (4) a ready-to-use LLM prompt with a structured output schema. A shorter section covers the cross-cutting pipeline and evaluation issues, a bench of theses that did not make the cut, and the ranking rationale. The ranking table comes first because it is the decision-relevant summary.

## Ranking: event sub-typing beats narrative tone on both evidence and practicality

| Rank | Thesis | Evidence base | Decay / replication status | Practicality | Where the LLM earns its keep |
|---|---|---|---|---|---|
| 1 | 8-K negative-event sub-typing (Items 4.02, 4.01, 2.05/2.06, 3.01, Form NT) | Peer-reviewed (RAST 2010, AJPT 2003, Accounting Horizons 2017, Advances in Accounting 2022) plus a 2025 working paper on 8,006 Item 4.02 filings | Event reaction persists in 2004–2023 samples; post-filing drift is modest (roughly −1 to −2.5%) and the drift estimates are 2005–2006 vintage | High: filing is the first public disclosure, item tags are machine-readable, 67,651 8-Ks/yr | Sub-typing within an item (revenue-recognition vs other, quantified vs uncertain, bid-price vs equity deficiency) with quote grounding |
| 2 | Form 4 conditional insider signals with footnote denoising | Strongest peer-reviewed effect sizes in the set (JF 2012, JFE 2017, MS 2022, JFQA 2019/2022, JFR 2019) | Unconditional purchase-following has decayed and fails capacity and placebo tests in 2018–2023 data; conditional variants have 2019–2022 support; post-2023 10b5-1 evidence conflicts | High: XML, two-business-day deadline, 10 p.m. dissemination, 351,055 filings/yr | Classifying "Explanation of Responses" footnotes into mechanical vs discretionary, gift, trust, plan-adoption-date categories |
| 3 | Schedule 13D activist filings scored on Item 4 specificity | Two decades of JF/JFE/RAST evidence plus the SEC's 2011–2021 staff tables | Announcement effect intact through 2021; value-weighted long-run alpha is zero; the 2024 deadline cut compresses the pre-filing window | Medium: most of the move arrives at acceptance; ~5 prominent-activist events per month | Classifying Item 4 into boilerplate / private engagement / explicit demand, validated by one RAST 2024 paper that used an LLM |
| 4 | 10-Q risk-factor updates and 10-K/10-Q textual change | 10-Q update drift from an unpublished 2016 working paper (52,955 filings, 2006–2014); Lazy Prices in JF 2020 | Lazy Prices null on S&P 100 2009–2026; no post-2014 re-test of the 10-Q result; Item 1A informativeness declined post-2008 | High volume (17,289 10-Qs/yr) and slow drift, so no latency race; needs small/mid caps | Atomic risk-factor diffing (added/removed/reworded) and judging whether an update is vague or fundamentals-specific |
| 5 | Abnormal tone in earnings releases and MD&A tone change | TAR 2014, CAR 2012, RAST 2010 | Dictionary tone decayed outside the original sample; firms adapted language after 2011; HTZ magnitudes are 1997–2007 era and summary-level | Medium: must be timed from the press-release wire, not the 8-K | Summarisation-based ("bloat") sentiment that explains reactions better than raw text |
| 6 | SEC comment-letter severity (UPLOAD/CORRESP) | TAR 2016, RAST 2021, RFS 2020 | No post-2016 replication; samples are 2005–2012 era; letters now widely scraped | Low capacity; tradable event is public release, weeks after the exchange | Severity scoring that separates long-but-benign from short-but-severe letters |

## 1. Risk-factor updates in 10-Qs and year-over-year change in 10-K/10-Q text predict negative drift

**Thesis.** Firms that update Item 1A in a 10-Q, or that materially rewrite the risk-factor section of a 10-K, underperform over the following three to twelve months because investors under-react to qualitative bad news that arrives without a headline number; the effect is strongest for vague updates and for small, low-attention firms, and it accrues as later news confirms the risk rather than at filing.

**Supporting research.** The quarterly version is the best-specified result. Filzen, McBrayer and Shannon's 2016 working paper, read in full from the SEC's S7-06-16 comment file, covers 52,955 10-Q filings by 4,353 firms with quarters ending 2006–2014; 26.3% of filings contain a risk-factor update, the mean three-month buy-and-hold abnormal return after an update is −0.54% (median −0.89%), and a value-weighted calendar-time strategy long firms with no update in the prior three months and short updaters earns a significant 3.53% annualised alpha, rising to 5.28% when the short leg is restricted to "weak" updates in the bottom three quartiles of fundamentals-word counts; "strong" updates show near-zero post-filing drift because the filing-date reaction is more complete ([Filzen, McBrayer & Shannon 2016, sec.gov PDF](https://www.sec.gov/comments/s7-06-16/s70616-369.pdf)). Filzen's published 2015 Accounting Horizons paper shows the earnings channel: 10-Q risk updates predict significantly lower future unexpected earnings and more extreme negative earnings shocks (per search extract) ([Filzen 2015](https://publications.aaahq.org/accounting-horizons/article-abstract/29/4/887/2223/The-Information-Content-of-Risk-Factor-Disclosures)). The quarterly result is structurally cleaner than the annual one because a 10-Q need only report changes to risk factors, so an update is by construction new information, a requirement that began for fiscal years ending after December 1, 2006 ([FMS 2016](https://www.sec.gov/comments/s7-06-16/s70616-369.pdf)).

The annual version is Cohen, Malloy and Nguyen's "Lazy Prices" (Journal of Finance 75(3), 2020; NBER WP 25084), which sorts firms monthly on year-over-year similarity of their 10-K/10-Q text using cosine, Jaccard, edit-distance and simple-diff measures that all give similar answers; a portfolio long "non-changers" and short "changers" earned roughly 30–60 bp/month on the CRSP universe 1995–2014 (per a replication README summarising the paper), rising to 188 bp/month with t = 2.76 when changes are concentrated in the Risk Factors section (per search extract), with no announcement effect and returns accruing only as information is later revealed ([Wiley JF](https://onlinelibrary.wiley.com/doi/abs/10.1111/jofi.12885); [NBER w25084](https://www.nber.org/system/files/working_papers/w25084/w25084.pdf); [Quantpedia summary](https://quantpedia.com/the-positive-similarity-of-company-filings-and-the-cross-section-of-stock-returns/)). Gaulin's dissertation work supports the atomic unit the fund should track: managers time the addition of new risk factors and the removal of old ones to align with expected adverse outcomes, and information is conveyed through the evolution of individual risk factors rather than total section length (per search extract) ([Gaulin, Rice repository](https://repository.rice.edu/server/api/core/bitstreams/f00b7b25-82b8-4536-94f0-ed596a9a4050/content)). Hope, Hu and Lu (Review of Accounting Studies 2016) show that specificity, measured as proper names, locations, percentages, dollar amounts and dates in Item 1A, is positively associated with the unsigned market reaction to the 10-K (per search extract) ([Springer](https://link.springer.com/article/10.1007/s11142-016-9371-1)), which is the same direction as the FMS "weak vs strong update" split.

**Replication, decay and contrary evidence.** This thesis has the most direct evidence of decay in the set, and the report does not oversell it. An open replication of Lazy Prices on the S&P 100 (99 firms, 1,792 10-Ks FY2007–FY2025, portfolios March 2009–September 2026, long least-changed quintile / short most-changed, held 12 months, 10 bp cost per leg) returned −0.92% per year gross, a Sharpe of −0.11 with a 95% confidence interval of [−0.56, 0.38], and an FF5+momentum alpha t-statistic of −0.49; across 54 variants the best Sharpe was 0.54 but its deflated Sharpe ratio was 0.13, far below the 0.95 certification threshold. The replicator also found that cosine similarity saturates near 1.0 for large caps (median 0.996) and that 23% of filings were missing Item 7 and 8% missing Item 1A after extraction ([iqueipopg/lazy-prices](https://github.com/iqueipopg/lazy-prices)). A second S&P 500 replication (1993–2024) found the most-similar bin had the best long-run performance but no monotonic pattern ([martifigueres replication](https://github.com/martifigueres/LAZY-PRICES-REPLICATION-AND-DASHBOARD)), and a structured evidence review graded the return claim "INSUFFICIENT post-publication" ([tradepartner issue #663](https://github.com/josejuarez96/tradepartner/issues/663)). On the positive side, one practitioner backtest on a point-in-time S&P 500 universe found that "the strongest signals were coming from the 10-Q's distance-based features" with a combined sector-neutral Sharpe of about 1.5 ([calebyung/NLP-10-K-10-Q-Alpha-Research](https://github.com/calebyung/NLP-10-K-10-Q-Alpha-Research)), which is consistent with the quarterly thesis surviving where the annual one fails. Beatty, Cheng and Zhang (Contemporary Accounting Research 2019) document a decline in the relevance of risk-factor disclosure after 2008 (per search extract) ([Wiley CAR](https://onlinelibrary.wiley.com/doi/abs/10.1111/1911-3846.12444)), and a small modern test of Item 1A tone (41 large caps, FY2014–2023, FinBERT vs Loughran–McDonald) found 0 of 25 return-predictive regressions significant at 5% ([ZacharyChai/finbert-10k-sentiment](https://github.com/ZacharyChai/finbert-10k-sentiment)). Two regime breaks contaminate backtests: SEC Release 33-10825, effective November 9, 2020, forced a one-time restructuring of Item 1A (summary section if over 15 pages, "material" rather than "most significant", generic risks segregated under a "General Risk Factors" heading) ([SEC final rule](https://www.sec.gov/rules/final/2020/33-10825.pdf)), mechanically creating "changers" in FY2020–21 unrelated to fundamentals; and Cao, Jiang, Yang and Zhang (Review of Financial Studies 2023) show that firms with high expected machine readership changed their language once the Loughran–McDonald lists were published in 2011 (per search extract) ([NBER w27950](https://www.nber.org/system/files/working_papers/w27950/w27950.pdf)). No peer-reviewed re-test of the FMS 10-Q result after 2014 was found, and the paper does not appear to have been published, so the 3.5–5.3% figure is a 2006–2014 estimate that the fund must re-estimate on 2015–2025 data before trading it.

**Filings, sections, timing and access.** The primary inputs are Form 10-Q Part II Item 1A (Risk Factors) and, for the annual version, Form 10-K Item 1A compared with the prior year's; for 10-Q MD&A comparisons the correct baseline is the same quarter of the prior year because of seasonality, whereas 10-Q Item 1A updates are cumulative "changes since the last 10-K" and should be compared against both the last 10-K and the prior 10-Q. EDGAR carried 17,289 10-Qs and 6,690 10-Ks in calendar 2025, with operating-company 10-K primary documents running roughly 55k–80k words and 10-Qs 16k–54k words after HTML stripping ([SEC full-index, own computation in notes](https://www.sec.gov/Archives/edgar/full-index/)). Because there is no announcement effect, the signal is formed the month after filing and held three months (quarterly refresh) or twelve months (annual), which removes any latency race but also means holding periods under six months probably capture little of the annual drift. Item segmentation is the known failure point, and recent work on pre-trained and LLM-based 10-K item segmentation addresses exactly the 23%-missing-Item-7 problem ([arXiv 2502.08875](https://arxiv.org/pdf/2502.08875)). A filing transmitted after 5:30 p.m. ET carries the next business day's filing date, so acceptance datetime, not filing date, must anchor the event ([SEC filing-status guide](https://www.sec.gov/submit-filings/filer-support-resources/how-do-i-guides/determine-status-my-filing)). The FY2020–21 cohort should be excluded or ranked only within cohort.

**Prompt (per 10-Q, run once per filing; for the 10-K variant replace "prior 10-K" with "prior-year 10-K" and drop the no-material-changes branch).**

```text
SYSTEM
You are a forensic disclosure analyst. You will be given the Risk Factors text from a
company's current quarterly report (10-Q Part II Item 1A) together with the full list of
risk-factor headings from the company's most recent annual report (10-K Item 1A) and, if
available, the Risk Factors text from the immediately preceding 10-Q. The company has been
anonymised: do not try to identify it, do not use any knowledge of events after the filing
date, and base every judgement only on the text supplied. Output must be valid JSON matching
the schema. Every flagged change must be supported by a verbatim quote of at most 40 words
copied exactly from the current filing; if you cannot quote it, do not report it.

USER
<filing_date>{{YYYY-MM-DD}}</filing_date>
<prior_10k_risk_factor_headings>
{{numbered list of headings from the last 10-K Item 1A}}
</prior_10k_risk_factor_headings>
<prior_10q_item_1a>
{{text, or "NONE"}}
</prior_10q_item_1a>
<current_10q_item_1a>
{{text}}
</current_10q_item_1a>

Tasks:
1. Decide whether the current Item 1A contains any substantive update beyond a statement
   that there have been no material changes. Cross-references, restated boilerplate and
   wording-only edits are NOT updates.
2. For each substantive update, classify it as ADDED (a risk not among the prior headings),
   REMOVED (a prior heading explicitly withdrawn), or MODIFIED (an existing risk whose
   substance changed), and categorise it.
3. Judge specificity: does the update cite firm-specific quantities (revenue, margins, cash,
   debt, customers, contracts, products, geographies, dates, dollar amounts, percentages),
   or is it generic language that could apply to any firm?
4. Judge severity and direction for the firm's next 12 months of earnings and cash flow.
5. Report the net number of fundamentals-specific terms in the update text.

JSON SCHEMA
{
  "has_substantive_update": boolean,
  "no_material_changes_statement_present": boolean,
  "updates": [
    {
      "change_type": "ADDED" | "REMOVED" | "MODIFIED",
      "category": "demand_or_customer" | "pricing_or_margin" | "liquidity_or_covenant" |
                  "going_concern" | "litigation_or_regulatory" | "cybersecurity" |
                  "supply_chain" | "key_personnel" | "accounting_or_controls" |
                  "macro_or_fx" | "competition_or_technology" | "other",
      "summary": string,
      "specificity": "FIRM_SPECIFIC" | "SEMI_SPECIFIC" | "GENERIC",
      "fundamentals_terms_count": integer,
      "severity": 1 | 2 | 3 | 4 | 5,
      "direction_next_12m": "NEGATIVE" | "NEUTRAL" | "POSITIVE",
      "already_quantified_in_financials": boolean,
      "evidence_quote": string
    }
  ],
  "overall_update_strength": "NONE" | "WEAK" | "STRONG",
  "overall_direction": "NEGATIVE" | "NEUTRAL" | "POSITIVE",
  "confidence": number
}

Rules: "WEAK" means at least one substantive update but all updates are GENERIC or
SEMI_SPECIFIC; "STRONG" means at least one FIRM_SPECIFIC update. confidence is in [0,1].
Return only the JSON.
```

The signal construction follows FMS: short or underweight firms with `overall_update_strength = "WEAK"` and `overall_direction = "NEGATIVE"` for three months starting the month after filing, long the no-update cohort, value-weighted and sector-neutral. The annual variant uses the `updates` array to compute an added-plus-removed count per filing and ranks within the filing-month cohort.

## 2. Abnormal optimism in earnings releases and MD&A tone change predict reversal and drift

**Thesis.** Managers manage tone: when the positive language in an earnings press release (8-K Item 2.02 Exhibit 99.1) is more optimistic than the reported fundamentals justify, the stock reacts positively at announcement and then reverses over the next one to two quarters, while a change in MD&A tone relative to the prior filing adds to post-earnings drift through the next earnings announcement.

**Supporting research.** Huang, Teoh and Zhang, "Tone Management" (The Accounting Review 89(3), 2014), define abnormal tone (ABTONE) as residual positive tone after controlling for earnings, risk, complexity and other fundamentals; abnormal positive tone at the earnings release is a negative predictor of abnormal returns, with a more positive immediate reaction and "a more negative market response in one and two quarters subsequent"; a secondary summary gives the magnitudes as 2.44% over one quarter and 4.70% over two quarters, and ABTONE also predicts negative earnings and cash flows one to three years ahead, future restatements, SEOs and M&A (summary-level) ([SSRN 1960376](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1960376); [AAA Commons summary](http://commons.aaahq.org/posts/b4ad070ca9)). Davis, Piger and Sedor (Contemporary Accounting Research 29(3), 2012) scored roughly 24,000 earnings press releases 1998–2003 with DICTION and found optimistic and pessimistic language "reliably predict future firm performance" with a significant incremental same-window market response ([Wiley CAR](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1911-3846.2011.01130.x); [St. Louis Fed WP 2006-005](https://files.stlouisfed.org/files/htdocs/wp/2006/2006-005.pdf)). For the MD&A leg, Feldman, Govindaraj, Livnat and Segal (Review of Accounting Studies 15(4), 2010) show that the change in MD&A tone versus the prior period is incrementally associated with drift from two days after the SEC filing date through one day after the next quarter's preliminary earnings announcement, beyond accruals and earnings surprise (per search extract) ([ResearchGate](https://www.researchgate.net/publication/314899519_Management's_Tone_Change_Post_Earnings_Announcement_Drift_and_Accruals)). The LLM-specific support is Kim, Muhn and Nikolaev's "Bloated Disclosures" (Chicago Booth / arXiv 2306.10224, 2023): GPT summaries of MD&A and earnings-call text are shorter by more than 70% yet have amplified information content, summary-based sentiment explains announcement-window returns better than raw-text sentiment, and a "bloat" measure is associated with lower price efficiency and higher information asymmetry (summary-level) ([arXiv 2306.10224](https://arxiv.org/pdf/2306.10224v1); [BFI summary](https://bfi.uchicago.edu/insight/research-summary/bloated-disclosures-can-chatgpt-help-investors-process-information/)). Loughran and McDonald's 2011 Journal of Finance negative-word list is the baseline and does replicate: an open re-run on 50,902 firm-years 1994–2008 recovers a Fama–MacBeth t-statistic of −2.99 for proportional negative tone against the original −2.64, with R² of about 2.5% and stronger effects for MD&A than the full filing ([lm2011-replication](https://github.com/m4a1ak471994/lm2011-replication)).

**Replication, decay and contrary evidence.** Two findings should be read as decay. Frankel, Jennings and Lee (Management Science 68(7), 2022) find that machine-learning sentiment explains 10-K filing-date returns throughout, whereas dictionary measures explain them only during the original Loughran–McDonald study period (per search extract) ([INFORMS](https://pubsonline.informs.org/doi/10.1287/mnsc.2021.4156)). Cao et al. (RFS 2023) find that firms with high expected machine downloads cut Loughran–McDonald negative words after 2011 with no such change for Harvard-dictionary negatives, which is direct evidence that issuers optimise against published lexicons (per search extract) ([NBER w27950](https://www.nber.org/system/files/working_papers/w27950/w27950.pdf)). The HTZ reversal figures are 1997–2007-era estimates whose exact coefficients and holding-period alphas could not be verified against the paper, and no 2022–2026 study applies an LLM to Exhibit 99.1 and reports post-announcement drift; the bloat paper's corpus is MD&A and call transcripts, not the press release. A review in The Accounting Review (2021) notes "little evidence of mispricing induced by non-GAAP reporting" ([TAR 96(3)](https://aaahq.org/portals/0/newsroom/2021/accr-96-03-1-25.pdf?ver=2021-06-04-163501-083)), so non-GAAP emphasis should be an input to the abnormal-tone regression rather than a standalone signal. Timing confounds matter: deHaan, Shevlin and Thornock (Journal of Accounting and Economics 60(1), 2015) show managers release bad news after hours, on busy days and with less notice ([SSRN 2545966](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2545966)), so tone sorts partly load on a known after-hours bad-news effect and must control for release time. The level of raw tone is a filing-window reaction variable with R² around 2.5%, not a drift signal; only abnormal tone (HTZ) and tone change (Feldman et al.) are investable.

**Filings, sections, timing and access.** The inputs are the 8-K Item 2.02 Exhibit 99.1 press release, which the form requires to be included as an exhibit whenever a registrant publicly announces results for a completed period ([SEC Form 8-K instructions](https://www.sec.gov/files/form8-k.pdf)), and 10-K Item 7 / 10-Q Part I Item 2 MD&A for the tone-change leg. Items 2.02 and 7.01 are "furnished" rather than "filed", the press release hits the wire before or simultaneously with the 8-K, and the 8-K is therefore an archive, not an information event; the fund must timestamp from the wire release, and 8-Ks accepted after 5:30 p.m. ET carry the next business day's filing date ([Latham & Watkins on the cutoff](https://wow.lw.com/Article/Index/186)). Press-release exhibits run roughly 600–6,200 words, so the LLM cost per event is trivial. Abnormal tone is computed outside the model by regressing the LLM tone score on earnings surprise, size, book-to-market, volatility, accruals, a loss dummy and release-time dummies within each quarter; the residual's top decile is the short leg, held one to two quarters after the announcement reaction has played out. The MD&A tone-change leg enters two days after the 10-Q/10-K acceptance and exits the day after the next earnings release.

**Prompt (per Exhibit 99.1; the same prompt runs on MD&A with the input tag changed).**

```text
SYSTEM
You are an equity analyst scoring the language of an earnings press release. The issuer is
anonymised; use only the supplied text and do not draw on any knowledge of the company or
of events after the release date. First write a faithful summary that preserves every
quantitative fact and every forward-looking statement but removes repetition, promotional
language and boilerplate. Then score the ORIGINAL text and the SUMMARY separately. Output
valid JSON only.

USER
<release_date>{{YYYY-MM-DD}}</release_date>
<release_time_et>{{HH:MM or "UNKNOWN"}}</release_time_et>
<prior_period_release_summary>{{summary JSON from last quarter, or "NONE"}}</prior_period_release_summary>
<press_release_text>
{{Exhibit 99.1 text, tables included}}
</press_release_text>

JSON SCHEMA
{
  "summary": string,
  "original_word_count": integer,
  "summary_word_count": integer,
  "tone_original": number,
  "tone_summary": number,
  "tone_change_vs_prior": number | null,
  "optimism_markers": [ { "phrase": string, "backed_by_number": boolean } ],
  "hedging_markers": [ { "phrase": string } ],
  "guidance": {
    "present": boolean,
    "action": "RAISED" | "MAINTAINED" | "LOWERED" | "WITHDRAWN" | "INITIATED" | "NONE",
    "metrics": [ string ],
    "evidence_quote": string
  },
  "non_gaap": {
    "non_gaap_leads_headline": boolean,
    "gaap_to_non_gaap_gap_direction": "NON_GAAP_HIGHER" | "SIMILAR" | "GAAP_HIGHER" | "NOT_REPORTED",
    "new_adjustment_categories_vs_prior": [ string ]
  },
  "performance_claims_without_support": integer,
  "negative_facts_buried_after_paragraph_3": [ string ],
  "overall_signal": "ABNORMALLY_OPTIMISTIC" | "CONSISTENT" | "ABNORMALLY_PESSIMISTIC",
  "confidence": number
}

Scoring rules: tone_* is in [-1, 1], where +1 is uniformly optimistic and -1 uniformly
pessimistic; score the summary on substance, not adjectives. tone_change_vs_prior is
tone_summary minus the prior period's tone_summary, or null if none supplied.
"performance_claims_without_support" counts superlatives or growth claims that cite no
figure. Quotes must be verbatim and at most 40 words. Return only the JSON.
```

The field `tone_original − tone_summary` is the fund's bloat-adjusted optimism measure and the candidate for the abnormal-tone regression; `guidance.action` and `non_gaap` are controls, and `negative_facts_buried_after_paragraph_3` operationalises the information-order finding that investors respond to placement.

## 3. Negative-event 8-K items carry a text-conditioned reaction and drift, and the filing is the first public disclosure

**Thesis.** For 8-K items that are usually the first public disclosure of bad news (Item 4.02 non-reliance, Item 4.01 auditor changes with reportable events, Items 2.05/2.06 exit costs and impairments, Item 3.01 listing deficiencies, Form 12b-25 late-filing notices), the sign of the reaction is known, but the text determines its magnitude and the post-filing drift: revenue-recognition errors, impacts the company "cannot yet quantify", equity or multiple listing deficiencies, and non-accounting reasons for late filing identify the sub-populations with two to three times the reaction and the most incomplete pricing at filing.

**Supporting research.** Schroeder's 2025 working paper (SSRN, posted January 31, 2025) is the largest sample: 8,006 Item 4.02 disclosures 2004–2023 show cumulative abnormal returns of −2.6% to −5.4%, revenue-recognition errors trigger 114% more severe reactions than net-income errors, disclosures expressing uncertainty about the impact of identified errors face three times harsher responses than those with clearly stated effects, and SEC-identified issues do not amplify the reaction (abstract-level; windows and t-statistics not verified) ([SSRN 5118253](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5118253)). A vendor event study over 2007–2023 (excluding 2021) finds Item 4.02 associated with −1.1% one day after disclosure extending to −2% over 20 days ([sec-api.io](https://sec-api.io/resources/stock-price-reactions-to-item-4-02-disclosures-in-sec-form-8-k-filings)), implying roughly −0.9% of drift after day one. Lerman and Livnat (Review of Accounting Studies 15(4), 2010) is the only systematic cross-item study: Items 2.05, 2.06, 3.01 and 4.02 generate significant negative returns around both event and filing dates, and 2.05 and 2.06 "have significant negative drifts between −1.1% and −2.5%" for up to 90 days, larger when no 10-K or 10-Q intervenes ([SSRN 1126816](https://www.ssrn.com/abstract=1126816); [NYU PDF](https://pages.stern.nyu.edu/~jlivnat/f8k%20current.pdf)). For auditor changes, Whisenant, Sankaraguruswamy and Raghunandan (Auditing: A Journal of Practice & Theory 22(1), 2003) report −2.75% over three days and −5.53% over seven days around the disclosure of "reportable events", robust to controls for resignations and disagreements ([AAA abstract](https://publications.aaahq.org/ajpt/article-abstract/22/1/181/5535/Market-Reactions-to-Disclosure-of-Reportable)). Guragai (Advances in Accounting 59, 2022) covers 3,425 Nasdaq deficiency notices to 1,018 companies 2004–2015: Item 3.01 filings draw negative reactions that are less negative with more institutional ownership and analyst following, and "equity and multiple deficiency notice filings elicit more negative reactions and are also more likely to result in actual delisting compared to bid price deficiency notice filings" ([ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0882611022000359)). For late filings, Bartov and Konchitchki (Accounting Horizons 31(4), 2017; 2,115 firms over nine years) find prices drop as soon as Form NT is filed, with five-day drops for NT 10-Qs of −5.48% (multiple issues), −2.87% (corporate events) and −2.83% (accounting reasons), and abnormal returns "continue to drift downward during the post-filing months" with the drift less pronounced when accounting reasons underlie the delay; average delays are 41 days for accounting reasons versus 13 for corporate events ([Accounting Horizons PDF](https://faculty.haas.berkeley.edu/yaniv/files/Papers_Publications/SEC-Filings-Regulatory-Deadlines-Capital-Market-Consequences_Bartov-Konchitchki_AH.pdf)). Two timing overlays are documented: Niessner's working paper finds managers 6% more likely to disclose negative news after Friday's close and a roughly 50 bp under-reaction persisting about three weeks (summary-level, unpublished) ([SSRN 2439040](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2439040)), and Cohen, Jackson and Mitts document insiders earning 42 bp per trade on average, and 163 bp on open-market purchases, inside the four-business-day gap between event and 8-K across 15,419 filings ([SSRN 2657877](https://ssrn.com/abstract=2657877)). The LLM tooling now exists: Dolphin et al. (arXiv 2607.08346, 2026) tag 292,984 8-Ks from 2022–2026 into a 119-type taxonomy with fuzzy quote validation and a quality score under which precision rises monotonically from 12% to 96%, retaining 34% of tags at 96% precision ([arXiv](https://arxiv.org/abs/2607.08346)), with a public reproduction that tests economic significance via standardised abnormal returns ([GitHub](https://github.com/chirindaopensource/grounded_event_extraction_from_SEC_8K_filings)).

**Replication, decay and contrary evidence.** The event-day reaction is the robust part, spanning 2003–2023 across multiple samples; the drift estimates are weaker. Lerman–Livnat's drift is 2005–2006 vintage and the per-item CARs and t-statistics could not be read; Schroeder's CAR range may mix windows; post-filing drift beyond 20 days for Item 4.02 was not quantified in any retrievable source. Item 2.06 carries a selection caveat: Sanseverino and Suh (Journal of Accounting, Auditing & Finance, online December 2024) find an Item 2.06 8-K is filed in only 9.84% of firm-quarters with 10-K/Q impairments, more often in quarters with option grants and insider purchases ([SSRN 5074799](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5074799)), so some 2.06 filings may be timed to depress the price before grants and reverse rather than drift. Ben-Rephael, Da, Easton and Israelsen (The Accounting Review 97(5), 2022) show media-driven retail pressure on the filing day that institutions exploit by providing liquidity ([AAA](https://publications.aaahq.org/accounting-review/article/97/5/59/336/Who-Pays-Attention-to-SEC-Form-8-K)), implying filing-day moves in heavily covered names partly reverse. For Item 5.02 departures, the form only requires the fact and date for officer departures ([Form 8-K](https://www.sec.gov/files/form8-k.pdf)), the only recent paper finds negative reactions to pre-restatement CFO turnovers but insignificant reactions to CEO turnovers ([Advances in Accounting 2025](https://www.sciencedirect.com/science/article/abs/pii/S0882611025000276)), and no paper quantifies returns conditional on the stated reason text, so the "vague-reason CFO departure" screen is an untested composite. No peer-reviewed 2022–2026 paper reports a long-short alpha from LLM-classified 8-K text with explicit holding windows.

**Filings, sections, timing and access.** Items are tagged in the EDGAR filing header and queryable by item number through full-text search and commercial APIs ([sec-api Item 4.02 API](https://sec-api.io/api-reference/form-8k-item-4-02)). The text to read is the item body plus the exhibits: Item 4.02(a) must give the date of the non-reliance conclusion, the periods affected, a brief description of the facts, and whether the audit committee discussed it with the auditor; Item 4.01 must carry the Regulation S-K Item 304(a)(1) disclosures with the auditor's agreement letter as Exhibit 16; Item 5.02(a) director disagreements must attach the director's correspondence as Exhibit 17 ([Form 8-K instructions](https://www.sec.gov/files/form8-k.pdf)). Most items are due within four business days of the event, so the pipeline should record the stated event date to measure the gap. Form 12b-25 is due one business day after the periodic-report deadline and requires a narrative reason, which is a representation with liability ([Unfolding Values explainer](https://www.unfoldingvalues.com/learn/form-nt-12b25/)). Negative-news 8-Ks are frequently accepted after 5:30 p.m. ET, so the day-0 reaction appears at the next session; the pipeline should key on (filer CIK, acceptance datetime, item list, exhibit types) and align returns to the next open when acceptance is after 4:00 p.m. There were 67,651 8-Ks in 2025 ([EDGAR full-index](https://www.sec.gov/Archives/edgar/full-index/)); the relevant negative items are a small fraction, so a cheap first-pass filter on the header's item list keeps frontier-model calls to a few thousand per year.

**Prompt (per 8-K whose header lists any of Items 2.04, 2.05, 2.06, 3.01, 4.01, 4.02, 5.02, or any Form NT 10-K / NT 10-Q).**

```text
SYSTEM
You are a forensic accountant extracting events from an SEC Form 8-K or Form 12b-25. The
issuer is anonymised. Use only the supplied text. For every event you report, copy a
verbatim quote of at most 50 words from the filing that establishes it; an event without a
quote is invalid. If the filing contains a press release exhibit, treat exhibit text as part
of the filing. Output valid JSON only.

USER
<form_type>{{8-K | 8-K/A | NT 10-K | NT 10-Q}}</form_type>
<items_declared>{{e.g. ["4.02", "9.01"]}}</items_declared>
<acceptance_datetime_et>{{YYYY-MM-DD HH:MM:SS}}</acceptance_datetime_et>
<filing_text>
{{item bodies}}
</filing_text>
<exhibits>
{{EX-16, EX-17, EX-99.x text if present}}
</exhibits>

JSON SCHEMA
{
  "events": [
    {
      "item": string,
      "event_type": "NON_RELIANCE_RESTATEMENT" | "AUDITOR_RESIGNED" | "AUDITOR_DISMISSED" |
                    "REPORTABLE_EVENT_DISCLOSED" | "IMPAIRMENT" | "EXIT_OR_RESTRUCTURING" |
                    "COVENANT_DEFAULT_OR_ACCELERATION" | "LISTING_DEFICIENCY" |
                    "OFFICER_DEPARTURE" | "DIRECTOR_DEPARTURE" | "LATE_FILING" | "OTHER",
      "event_date": string | null,
      "first_public_disclosure": boolean,
      "accounting_area": "REVENUE_RECOGNITION" | "LEASES" | "TAX" | "INVENTORY" |
                         "GOODWILL_OR_INTANGIBLES" | "DEBT_CLASSIFICATION" | "EQUITY_OR_WARRANTS" |
                         "INTERNAL_CONTROLS" | "OTHER" | "NOT_APPLICABLE",
      "periods_affected_count": integer | null,
      "impact_quantified": "QUANTIFIED" | "RANGE_GIVEN" | "NOT_YET_DETERMINED" | "STATED_IMMATERIAL",
      "impact_direction": "NEGATIVE" | "POSITIVE" | "MIXED" | "UNKNOWN",
      "impact_magnitude_usd": number | null,
      "sec_identified": boolean,
      "auditor_change": {
        "reportable_event_cited": boolean,
        "disagreement_cited": boolean,
        "going_concern_in_prior_opinion": boolean,
        "ex16_letter_agrees": "AGREES" | "DISAGREES" | "PARTIAL" | "NOT_INCLUDED"
      } | null,
      "listing_deficiency": {
        "deficiency_type": "BID_PRICE" | "STOCKHOLDERS_EQUITY" | "MARKET_VALUE" |
                           "LATE_PERIODIC_REPORT" | "MULTIPLE" | "OTHER",
        "cure_period_days": integer | null
      } | null,
      "departure": {
        "role": "CEO" | "CFO" | "CAO" | "COO" | "OTHER_OFFICER" | "DIRECTOR",
        "successor_named": boolean,
        "effective_immediately": boolean,
        "stated_reason": "PURSUE_OTHER_OPPORTUNITIES" | "PERSONAL" | "RETIREMENT" |
                         "TERMINATED" | "DISAGREEMENT" | "NONE_GIVEN" | "OTHER",
        "no_disagreement_statement_present": boolean
      } | null,
      "late_filing_reason": "ACCOUNTING" | "CORPORATE_EVENT" | "MULTIPLE" | "OTHER" | null,
      "evidence_quote": string,
      "quality_score": 1 | 2 | 3 | 4 | 5
    }
  ],
  "overall_severity": 1 | 2 | 3 | 4 | 5,
  "confidence": number
}

quality_score is your own assessment of how directly the quote supports the event
(5 = the quote states it verbatim, 1 = inferred). confidence is in [0,1]. Return only the JSON.
```

The trading rule follows the literature: short Item 4.02 filers at the next open for about 20 trading days, overweighting `accounting_area = "REVENUE_RECOGNITION"` and `impact_quantified = "NOT_YET_DETERMINED"`; short Item 4.01 filers with `reportable_event_cited = true` for about seven days; short 2.05/2.06 for 60–90 days when the next periodic filing is more than 90 days away; short Form NT filers with `late_filing_reason` other than `"ACCOUNTING"` for one to three months; and filter everything on `quality_score ≥ 4`, mirroring the Dolphin et al. precision curve.

## 4. Conditional Form 4 insider signals survive where unconditional ones have decayed, and footnotes are the denoising layer

**Thesis.** Open-market insider purchases predict returns only when the trade is opportunistic rather than routine, clustered across insiders, made through indirect accounts, or made by a CFO; insider gifts and insider silence are negative signals; 10b5-1 plan sales timed to the 90–120-day post-adoption window remain informative after the 2023 reform. The Form 4 "Explanation of Responses" footnotes are what separate discretionary trades from tax withholding, sell-to-cover, plan sales and transfers, so an LLM footnote classifier is the enabling step rather than the alpha source.

**Supporting research.** Cohen, Malloy and Pomorski, "Decoding Inside Information" (Journal of Finance 67(3), 2012), classify insiders as routine if they traded in the same calendar month in prior years and find a value-weighted long-short portfolio on opportunistic traders earns 82 bp/month while routine traders earn essentially zero; opportunistic trades predict future firm-specific news and the most informed are local, non-executive insiders at geographically concentrated, poorly governed firms ([Wiley](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1540-6261.2012.01740.x); [NBER Digest](https://www.nber.org/digest/apr11/decoding-inside-information)). Ali and Hirshleifer (Journal of Financial Economics 126(3), 2017) identify opportunistic insiders from the profitability of pre-earnings-announcement trades and report four-factor alphas above 1% monthly on those insiders' subsequent trades ([ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0304405X17302349)). Alldredge and Blank (Journal of Financial Research 2019) find ~23% of purchases occur on the same day as another insider's and that purchases within two days of another insider's purchase are followed by ~2.1% abnormal return the next month, 0.9 points more than solitary purchases ([Wiley](https://onlinelibrary.wiley.com/doi/abs/10.1111/jfir.12172)). "Indirect Insider Trading" (JFQA 2022/2023) shows a hedge portfolio of large indirect trades through family, trust, retirement and foundation accounts earns 0.90% the following month, 50 bp more than direct trades, accumulating 6.34% over two years without reversal ([Cambridge PDF](https://www.cambridge.org/core/services/aop-cambridge-core/content/view/7933F3093D5055F73128AF294FFF0945/S0022109022001119a.pdf/indirect-insider-trading.pdf)). Wang, Shin and Francis (JFQA 47(4), 2012) find CFO purchases earn 12-month excess returns 5 percentage points higher than CEO purchases ([Cambridge](https://www.cambridge.org/core/journals/journal-of-financial-and-quantitative-analysis/article/abs/are-cfos-trades-more-informative-than-ceos-trades/B7DD71285F1326E694CC860193C87710)). On the negative side, Avci, Schipani, Seyhun and Verstein (Duke Law Journal 71, 2021) find insider gifts are "suspiciously well-timed", with prices rising ~6% in the year before and falling ~4% in the year after ([SSRN](https://ssrn.com/abstract=3795537)), and Yermack (JFE 94, 2009) documents an inverted-V price path peaking exactly on the gift date for CEO gifts to family foundations ([NYU PDF](https://web-docs.stern.nyu.edu/glucksman/docs/Gifts_20081231.pdf)). Gao, Ma, Ng and Wu, "The Sound of Silence" (Management Science 2022), show the insider-silence portfolio's buy-and-hold abnormal return is a significant −7.3% and a silence-based strategy yields about 7.36%/year, wider at firms with worse information environments ([INFORMS](https://pubsonline.informs.org/doi/10.1287/mnsc.2021.4113)), while Hong and Li (JFQA 2019) show sudden silence after a routine selling schedule predicts positive returns, with a long-short strategy earning 6–10% annually ([Cambridge](https://www.cambridge.org/core/journals/journal-of-financial-and-quantitative-analysis/article/abs/information-content-of-sudden-insider-silence/32C501CD9FB2FE914771EB9C5DB2EB73)). For plan sales, Larcker et al.'s Stanford Closer Look (January 2021) built from Form 144 adoption dates for 20,595 plans by 10,123 executives 2016–2020 found ~14% of plans commence trading within 30 days of adoption, that trades within 30 days are ~50% larger, and that sales under red-flag plans (short cooling-off, single-trade, adopted just before earnings) foreshadow declines well in excess of peers ([SSRN 3769567](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3769567)); Jagolinzer (Management Science 55(2), 2009) found plan adoption associated with adverse news an average 72.2 days later, as restated in the SEC's own rule release ([SEC Release 33-11138](https://www.sec.gov/files/rules/final/2022/33-11138.pdf)).

**Replication, decay and contrary evidence.** The unconditional signal has decayed and the report says so plainly: a Finance Research Letters 2024 study of 58,732 Form 4 filings from November 2018 to November 2023 finds positive but lower short-horizon abnormal returns than earlier studies, returns that vanish or turn negative once the tradable dollar amount per signal is capped, and placebo events shifted six months forward showing abnormal returns of the same size and sign ([ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1544612324015435)); McLean and Pontiff's cross-anomaly norm is a ~50% post-publication decline ([HEC PDF](https://www.hec.ca/finance/Fichier/McLean.pdf)). No post-2020 out-of-sample replication of CMP, Ali–Hirshleifer or the indirect-trade result was found. The 10b5-1 evidence after the 2023 reform conflicts: a Journal of Accounting and Economics 2026 paper finds plan sales within 90 days of adoption fell from 31.1% to 1.7% and that post-reform plan sales are followed by flat or slightly positive abnormal returns ([CLS Blue Sky summary](https://clsbluesky.law.columbia.edu/2025/07/31/insider-trading-after-the-2022-rule-10b5-1-amendment/)), whereas a Bergen/CEPR study of 158,000 executive sales 2016–2025 finds abnormal profits did not fall, that the 90–120-day window's share rose from ~11% to nearly 30%, and that annual abnormal gains rose from ~$23M to ~$89M ([CEPR DP21199](https://cepr.org/publications/dp21199); [Verity summary](https://verityplatform.com/resources/study-insider-sales-10b5-1/)). Vendors report cluster-buy alpha "reduced but still measurable" and front-loaded in the first 21–60 trading days (practitioner, no sample stated) ([Form4API](https://www.form4api.com/guides/cluster-buy-signals)). Critically, no retrieved study shows a text-mined footnote feature adding alpha beyond the category labels; the footnote classifier reproduces vendor cleansing and enables the conditional theses, and its incremental value is a proprietary test, not a published result. Hvide and Nielsen's below-top-executive result (68–101 bp over one month) is Norwegian register data, not US Form 4 ([ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0304405X2600053X)).

**Filings, sections, timing and access.** Form 4 must be filed before the end of the second business day after the transaction, and EDGAR serves it as XML with `nonDerivativeTable` (Table I) and `derivativeTable` (Table II), transaction codes (P, S, A, F, M, G, J and others), a direct/indirect flag with a nature-of-ownership text, and footnotes linked by `footnoteId` IDREFs ([Form 4 instructions](https://www.sec.gov/files/form4.pdf); [EDGAR ownership XML spec](https://www.sec.gov/info/edgar/ownershipxmltechspec-v4_d.htm)). Since April 1, 2023, Form 4 carries a mandatory 10b5-1 checkbox with the plan adoption date in the Explanation of Responses, gifts must be reported within two business days, and Item 408(a) of Regulation S-K requires quarterly 10-Q/10-K disclosure of plan adoptions and terminations with name, date, duration and share count ([SEC Release 33-11138](https://www.sec.gov/files/rules/final/2022/33-11138.pdf)). Form 144 has been electronic and machine-readable since April 13, 2023 and leads the Form 4 by up to several days ([SEC compliance notice](https://www.sec.gov/oit/announcement/form-144-electronic-filing-compliance-date)). Section 16 forms transmitted between 5:30 and 10:00 p.m. ET keep that day's filing date and are disseminated until 10:00 p.m., unlike 10-Ks and 8-Ks ([SEC filing-status guide](https://www.sec.gov/submit-filings/filer-support-resources/how-do-i-guides/determine-status-my-filing)). Volume is high but cheap: 351,055 Form 4s, 68,810 Form 144s and 25,923 Form 3s in 2025, at only 89–187 words of text per Form 4 ([EDGAR full-index, own computation](https://www.sec.gov/Archives/edgar/full-index/)). The signal date is EDGAR acceptance, entry is the next open, holding is one to three months for purchase signals and twelve months for gift and silence signals; the opportunistic flag, pre-earnings profitability score, seven-day cluster count and silence state are computed from the structured history outside the model.

**Prompt (per Form 4, after XML parsing; the model sees only rows and footnotes).**

```text
SYSTEM
You classify transactions reported on SEC Form 4 using the structured rows and the
"Explanation of Responses" footnotes. The issuer and reporting person are anonymised. Use
only the supplied content. Your job is to decide, for each non-derivative row, whether the
transaction reflects a discretionary decision by the insider, and to extract the facts the
footnotes add. Output valid JSON only.

USER
<filing_acceptance_et>{{YYYY-MM-DD HH:MM:SS}}</filing_acceptance_et>
<reporting_owner_relationship>{{Director / Officer (title) / 10% Owner / Other}}</reporting_owner_relationship>
<officer_title>{{text or ""}}</officer_title>
<rule_10b5_1_checkbox>{{true | false}}</rule_10b5_1_checkbox>
<rows>
{{for each Table I row: row_id, transaction_date, code, acquired_or_disposed, shares,
  price, post_transaction_shares, ownership_form (D/I), nature_of_ownership, footnote_ids}}
</rows>
<footnotes>
{{F1: text, F2: text, ...}}
</footnotes>

JSON SCHEMA
{
  "rows": [
    {
      "row_id": string,
      "discretionary": boolean,
      "category": "OPEN_MARKET_PURCHASE" | "OPEN_MARKET_SALE" | "PRIVATE_TRANSACTION" |
                  "TAX_WITHHOLDING" | "SELL_TO_COVER_EXERCISE" | "OPTION_EXERCISE" |
                  "GRANT_OR_AWARD" | "VESTING" | "RULE_10B5_1_PLAN_SALE" | "RULE_10B5_1_PLAN_PURCHASE" |
                  "GIFT_TO_CHARITY" | "GIFT_TO_FAMILY_OR_FOUNDATION" | "TRANSFER_NO_PECUNIARY_CHANGE" |
                  "ESTATE_OR_DIVORCE" | "DISTRIBUTION_IN_KIND" | "FORFEITURE" | "PLEDGE_OR_MARGIN" |
                  "ISSUER_REPURCHASE" | "OTHER",
      "plan_adoption_date": string | null,
      "plan_is_single_trade": boolean | null,
      "indirect_owner_type": "SPOUSE" | "CHILD_OR_FAMILY" | "FAMILY_TRUST" | "RETIREMENT_ACCOUNT" |
                             "FOUNDATION" | "LLC_OR_PARTNERSHIP" | "OTHER" | null,
      "gift_recipient_type": "CHARITY" | "FAMILY_FOUNDATION" | "FAMILY_MEMBER" | "TRUST" | "OTHER" | null,
      "price_is_weighted_average": boolean,
      "price_range_low": number | null,
      "price_range_high": number | null,
      "pledged_shares_mentioned": boolean,
      "margin_call_or_forced_sale_mentioned": boolean,
      "amendment_reason": string | null,
      "evidence_footnote_ids": [ string ],
      "confidence": number
    }
  ],
  "filing_level": {
    "voluntary_early_report_code_v": boolean,
    "late_filing_explanation_present": boolean,
    "any_discretionary_purchase": boolean,
    "any_discretionary_sale": boolean,
    "any_gift": boolean
  }
}

Rules: a row is discretionary only if the insider chose the timing and amount; tax
withholding (code F), sell-to-cover language, grants (A), vesting, forfeitures, transfers
between accounts of the same person, and sales under a 10b5-1 plan are NOT discretionary.
A code S row with no footnote and the checkbox unchecked is OPEN_MARKET_SALE and
discretionary. Dates in ISO format. confidence in [0,1]. Return only the JSON.
```

Downstream, the fund keeps rows with `discretionary = true`, applies the CMP routine/opportunistic rule and the Ali–Hirshleifer profitability score from history, counts distinct discretionary purchasers within seven days for clusters, flags `indirect_owner_type` trades and `GIFT_TO_FAMILY_OR_FOUNDATION`, and computes `transaction_date − plan_adoption_date` to isolate the 90–120-day window and single-trade plans.

## 5. Schedule 13D announcement returns are real and durable, and Item 4 text sorts the large reactions from the boilerplate

**Thesis.** A Schedule 13D by an activist is followed by a positive abnormal return that does not reverse, concentrated in small caps and in filers still accumulating; the text of Item 4 (purpose of transaction) separates boilerplate "investment purposes" filings from explicit demands, and explicit board-seat or sale demands earn the largest reactions and the highest win rates.

**Supporting research.** Brav, Jiang, Partnoy and Thomas (Journal of Finance 63(4), 2008; 1,059 hedge-fund activism events 2001–2006) report ~7% abnormal return around announcement with no reversal in the subsequent year, which the SEC's 2023 rule release restates as "an abnormal short-term return of 7% over the window before and after a Schedule 13D filing" ([Wiley](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1540-6261.2008.01373.x); [SEC Release 33-11253, fn. 563](https://www.sec.gov/files/rules/final/2023/33-11253.pdf)). Bebchuk, Brav and Jiang (Columbia Law Review 115, 2015) find ~6% announcement returns 1994–2007 with no reversal over five years, again restated by the SEC ([SSRN 2291577](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2291577)). The SEC's own staff analysis of initial 13Ds 2011–2021 is the most recent large sample and the strongest citation because it was read in full: among 3,067 "non-corporate-action" filings with tabular trade histories, the average CAR(−20,+20) is 5.7% where the filer had completed its stake by the new five-business-day deadline, 8.1% where still accumulating, 17.2% where under 90% accumulated and 14.4% where under 75%; filers that used the full ten days earned roughly 3% from day seven to the day after filing; only 22 "Prominent Activists" filed 60 initial 13Ds in 2022 with a median 6.6% stake ([SEC Release 33-11253, Tables 1–6](https://www.sec.gov/files/rules/final/2023/33-11253.pdf)). Albuquerque, Fos and Schroth (Journal of Financial Economics 2022) estimate a 6.34% return after a 13D versus 0.59% for passive 13G filings, attributing 74.8% of the 13D return to activism rather than stock-picking (per search extract) ([ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0304405X21003950)). On text specifically, Aiken and Lee (Journal of Corporate Finance 2020) use Item 4 language about prior negotiations to show that nearly a quarter of campaigns begin as "open activism" with demands stated in the 13D and that the market responds positively anticipating operational improvements (per search extract) ([ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0929119920300377)); McDonough, Nagar and Schoenfeld (Review of Accounting Studies 29(3), 2024) hand-collected activist disclosure texts, generated topics with a large language model, and found disclosures demanding a board seat have the highest announcement returns and that disclosers win proxy contests and directorships more often (per search extract) ([Springer](https://link.springer.com/article/10.1007/s11142-024-09836-6)); Bebchuk, Brav, Jiang and Keusch (JFE 137(1), 2020) show settlement agreements, filed as 13D/A exhibits, are accompanied by positive reactions and followed by CEO turnover and higher payouts ([ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0304405X20300180)). Greenwood and Schor (JFE 92(3), 2009) show the long-run returns are concentrated in targets subsequently acquired ([HBS PDF](https://www.hbs.edu/ris/download.aspx?name=Investor+Activism+and+Takeovers.pdf)), and Fos (Management Science 63(3), 2017) finds proxy contests earn ~6.5% with gains concentrated in business-strategy and undervaluation contests rather than capital-structure or governance ones ([INFORMS](https://pubsonline.informs.org/doi/10.1287/mnsc.2015.2340)). Collin-Dufresne and Fos use the Item 5(c) trade tables to show filers' trades are 26.3% of daily turnover in the 60-day pre-filing window and a replicating portfolio earns 0.09% daily four-factor alpha ([NBER w18452](https://www.nber.org/system/files/working_papers/w18452/w18452.pdf)).

**Replication, decay and contrary evidence.** The announcement effect has not decayed: the SEC's 2011–2021 figure of 5.7% for completed-stake filers sits beside Brav et al.'s 1994–2018 ~5% and the 9% smallest-tercile versus 2–3% largest-tercile split (SEC fn. 827–829). But deHaan, Larcker and McClure (Review of Accounting Studies 2019) show equal-weighted long-run returns are driven by the smallest 20% of targets (average market cap $22 million), that the larger 80% have insignificant negative long-run returns, that value-weighted pre-to-post returns are indistinguishable from zero, and that apparent operating improvements reflect pre-activism trends (per search extract; the SEC confirms the "smallest 20%" result) ([Springer](https://link.springer.com/article/10.1007/s11142-019-9480-8)). Capacity is therefore the constraint: the SEC's estimated value creation per campaign is $36M–$222M, initial 13D counts halved from ~2,800/year in 1997–2010 to ~1,400 in 2011–2022, and 80% of the 15,724 initial 13Ds in 2011–2021 were "corporate action" filings with no campaign at all ([SEC Release 33-11253](https://www.sec.gov/files/rules/final/2023/33-11253.pdf)). No study scores Item 4 tone or hostility with NLP and reports a return spread, the per-category announcement returns in McDonough et al., Aiken–Lee and Brav 2008 (Table IV/V) were not retrievable and should be pulled, and no post-February-2024 study measures whether the deadline cut changed the CAR. The 13G-to-13D switch has only practitioner claims behind it ([13finsight](https://13finsight.com/learn/13d-vs-13g-filings-active-vs-passive-intent-explainer)).

**Filings, sections, timing and access.** Since February 5, 2024, an initial 13D is due within five business days of crossing 5% (previously ten calendar days), 13D amendments within two business days (previously "promptly"), passive-investor 13Gs within five business days, and the 13D/13G cut-off moved from 5:30 p.m. to 10 p.m. ET; XML filing via EDGAR Online Forms has been mandatory since December 18, 2024, with only exhibits remaining unstructured ([SEC Release 33-11253](https://www.sec.gov/files/rules/final/2023/33-11253.pdf); [SEC press release 2023-219](https://www.sec.gov/newsroom/press-releases/2023-219); [EDGAR Filer Manual Vol. II v72](https://www.sec.gov/files/edgar/filermanual/archive/efmvol2-v72.pdf)). The fields to read are the cover page (type of reporting person: IA/PN/HC for funds; percent of class), Item 3 (source of funds: "working capital" indicates open-market accumulation), Item 4 (purpose), Item 5(c) (all transactions in the past 60 days, which gives the 5%-crossing date), Item 6 (contracts, now including all derivatives) and Item 7 exhibits (letters, cooperation agreements), with the header separating SUBJECT COMPANY from FILED BY and listing GROUP MEMBERS ([example 13D/A](https://www.sec.gov/Archives/edgar/data/1031316/000090266424006808/p24-3453sc13da.htm)). EDGAR carried 11,274 "SCHEDULE 13D" and 49,060 "SCHEDULE 13G" submissions in 2025 ([full-index](https://www.sec.gov/Archives/edgar/full-index/)). Because most of the move arrives within a day of acceptance and filings can land as late as 10 p.m., execution at acceptance time or the next open matters more here than for any other thesis; the pipeline polls the submissions API at sub-minute cadence, joins the filer CIK to a curated activist list (the SEC used Insightia's Activist Top Ten and FactSet's SharkWatch 50) and to 13F filer CIKs, and timestamps the event at acceptance.

**Prompt (per initial Schedule 13D or 13D/A; the model sees Items 3–7 and exhibits).**

```text
SYSTEM
You are an M&A and activism analyst reading a Schedule 13D. The subject company and filer
are anonymised. Use only the supplied text. Classify the filer's stated purpose, extract
every explicit demand, and judge how specific and how adversarial the filing is. Every demand
must be supported by a verbatim quote of at most 40 words. Output valid JSON only.

USER
<submission_type>{{SCHEDULE 13D | SCHEDULE 13D/A}}</submission_type>
<amendment_number>{{integer or 0}}</amendment_number>
<acceptance_datetime_et>{{YYYY-MM-DD HH:MM:SS}}</acceptance_datetime_et>
<cover_page>{{type of reporting person codes, percent of class, group members count}}</cover_page>
<item_3_source_of_funds>{{text}}</item_3_source_of_funds>
<item_4_purpose>{{text}}</item_4_purpose>
<item_5c_transactions>{{table or text}}</item_5c_transactions>
<item_6_contracts>{{text}}</item_6_contracts>
<exhibits>{{EX-99 letters, agreements, press releases}}</exhibits>

JSON SCHEMA
{
  "engagement_type": "BOILERPLATE_INVESTMENT_PURPOSE" | "PRIVATE_ENGAGEMENT_MENTIONED" |
                     "OPEN_DEMANDS" | "SETTLEMENT_OR_COOPERATION" | "EXIT_OR_GROUP_DISSOLUTION" |
                     "CORPORATE_ACTION_ONLY",
  "demands": [
    {
      "type": "BOARD_SEATS" | "SALE_OF_COMPANY" | "STRATEGIC_ALTERNATIVES" | "DIVESTITURE_OR_SPIN" |
              "CAPITAL_RETURN" | "CAPITAL_STRUCTURE" | "OPERATIONAL_CHANGE" | "CEO_CHANGE" |
              "GOVERNANCE_CHANGE" | "OPPOSE_TRANSACTION" | "OTHER",
      "specificity": "NAMED_AND_QUANTIFIED" | "NAMED" | "VAGUE",
      "number_of_seats": integer | null,
      "evidence_quote": string
    }
  ],
  "prior_private_contact_with_management": boolean,
  "hostility": 0 | 1 | 2 | 3 | 4,
  "threatens_proxy_contest_or_litigation": boolean,
  "nomination_deadline_mentioned": string | null,
  "accumulation": {
    "open_market_purchases_in_item_5c": boolean,
    "share_of_60_day_purchases_in_last_10_days": number | null,
    "still_accumulating_language": boolean,
    "derivatives_or_swaps_disclosed": boolean
  },
  "group": {
    "multiple_unaffiliated_funds": boolean,
    "wolf_pack_indicators": [ string ]
  },
  "settlement": {
    "present": boolean,
    "board_seats_granted": integer | null,
    "standstill_expiry": string | null,
    "ownership_cap_pct": number | null
  },
  "source_of_funds": "WORKING_CAPITAL_OF_FUNDS" | "BORROWED" | "SHARES_FROM_TRANSACTION" | "OTHER",
  "confidence": number
}

hostility: 0 = cooperative, 4 = litigation or public attack on named directors. confidence
in [0,1]. Return only the JSON.
```

The rule: enter at acceptance for `engagement_type = "OPEN_DEMANDS"` with `source_of_funds = "WORKING_CAPITAL_OF_FUNDS"` and `open_market_purchases_in_item_5c = true`, size up when `still_accumulating_language = true` or the last-10-day purchase share is high, weight toward `BOARD_SEATS` and `SALE_OF_COMPANY` demands, treat boilerplate filings like 13Gs, and run a separate long on 13D/A filings where `settlement.present = true` with the standstill expiry stored as a re-escalation date.

## 6. SEC comment-letter severity predicts a multi-week negative drift that investors ignore

**Thesis.** When the SEC's correspondence with a registrant becomes public, letters about revenue recognition and other core accounting issues are followed by a small negative return and a 1–5% negative drift over roughly 50 trading days, because few investors download the letters; an LLM severity score should separate the letters that predict restatements from the long-but-benign ones that only retail investors react to.

**Supporting research.** Dechow, Lawrence and Ryans (The Accounting Review 91(2), 2016) find insider selling significantly above normal before public disclosure of revenue-recognition comment letters and triple its normal level at firms with high short interest, a small negative return at release, a negative drift of 1–5% over the following 50 days that is stronger where pre-disclosure insider sales were greater, and that comment letters are downloaded infrequently from EDGAR after release (per search extract) ([SSRN 2336812](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2336812); [CFO.com coverage](https://www.cfo.com/news/sec-comment-letters-lead-insiders-to-dump-shares/665054/)). Ryans (Review of Accounting Studies 26(1), 2021) shows naive-Bayes classification of letter text identifies letters associated with future restatements and write-downs, that disclosure-event abnormal returns, revenue-recognition comments and the number of letters in a conversation are useful importance metrics, and that innocuous letters are associated with improved earnings credibility (per search extract) ([Springer](https://link.springer.com/article/10.1007/s11142-020-09565-6); [LBS working paper](https://lbsresearch.london.edu/id/eprint/1268/1/comment_letter_text_20191102.pdf)). Lowry, Michaely and Volkova (Review of Financial Studies 33(12), 2020) apply LDA and KL divergence to pre-IPO comment letters and find revenue recognition is the dominant SEC concern, is not independently discovered by investors, and is associated with lower post-IPO returns and higher withdrawal probability (per search extract) ([RePEc](https://ideas.repec.org/a/oup/rfinst/v33y2020i12p5510-5554..html)). Cassell, Dreher and Myers (The Accounting Review 2013) show that weak internal controls, complex operations, smaller auditors and weak governance predict longer response times, more rounds and a higher probability of restatement ([ResearchGate](https://www.researchgate.net/publication/228273971_Reviewing_the_SEC's_Review_Process_10-K_Comment_Letters_and_the_Cost_of_Remediation)), and Johnston and Petacchi (Contemporary Accounting Research 34, 2017) show adverse selection in spreads falls and earnings response coefficients rise after resolution ([Semantic Scholar](https://www.semanticscholar.org/paper/Regulatory-Oversight-of-Financial-Reporting:-and-Johnston-Petacchi/684371cd9ff1acdc29f6e7c2ca13d49ab7c9a9ea)), which supports a mirror-image long around the first earnings announcement after the "no further comments" letter. A conference paper on Robinhood investors finds retail holders reduce positions in firms receiving longer letters with more issues, while the number of rounds and duration do not move retail trade, and notes that fewer than 10% of letters lead to an amended filing and under 3% to a restatement ([conference PDF](https://s3.amazonaws.com/amz.xcdsystem.com/DE52A724-B7F9-5299-52604A3263D5412C_abstract_File17073/851_ViewPaper_1201105708.pdf?nocache=230511130407)).

**Replication, decay and contrary evidence.** This is the thinnest thesis on decay evidence precisely because no one has re-tested it: the Dechow et al. sample is 2005–2012 era, its t-statistics and sub-period robustness were not verifiable, no post-2016 replication exists, and comment letters are now covered by Audit Analytics and news aggregators, which should have eroded the inattention mechanism. Ryans 2021 does not appear to report a tradable return test, so whether severity predicts returns rather than restatements is unknown. No 2022–2026 LLM study of comment-letter text was located. The base rate matters for sizing: with under 3% of letters ending in restatement, the signal is a probability tilt, and the Robinhood evidence that retail reacts to length rather than severity suggests a two-sided trade (long after retail overreaction to long-but-benign letters, short after short-but-severe ones) that is entirely untested.

**Filings, sections, timing and access.** The inputs are EDGAR form types UPLOAD (the SEC staff's letter) and CORRESP (the registrant's response), released publicly only after the review closes, so the tradable event is the EDGAR acceptance of the public release, not the date on the letter. Both are short free-text documents, trivially cheap to score. The pipeline ingests UPLOAD/CORRESP daily, groups them by registrant CIK into conversations, counts rounds, scores each SEC letter for topic and severity, joins Form 4 sales in the window before release (the Dechow et al. amplifier) and short interest, and shorts or underweights flagged firms for about 50 trading days from release.

**Prompt (per UPLOAD letter, with the matching CORRESP response if available).**

```text
SYSTEM
You are a technical accounting reviewer reading an SEC Division of Corporation Finance
comment letter and, if supplied, the registrant's response. The registrant is anonymised.
Use only the supplied text. Classify each numbered comment, assess how severe it is for
the reliability of reported revenue and earnings, and judge from the response whether the
registrant conceded, resisted, or promised future changes. Every severity-4 or severity-5
comment must carry a verbatim quote of at most 40 words from the SEC letter. Output valid
JSON only.

USER
<public_release_datetime_et>{{YYYY-MM-DD HH:MM:SS}}</public_release_datetime_et>
<letter_date>{{YYYY-MM-DD}}</letter_date>
<round_number_in_conversation>{{integer}}</round_number_in_conversation>
<filing_reviewed>{{10-K FY.. | 10-Q Q.. | S-1 | 8-K | other}}</filing_reviewed>
<sec_letter_text>
{{UPLOAD text}}
</sec_letter_text>
<registrant_response_text>
{{CORRESP text or "NONE"}}
</registrant_response_text>

JSON SCHEMA
{
  "is_closing_letter": boolean,
  "comments": [
    {
      "comment_number": integer,
      "topic": "REVENUE_RECOGNITION" | "IMPAIRMENT_OR_FAIR_VALUE" | "SEGMENTS" | "NON_GAAP" |
               "GOING_CONCERN_OR_LIQUIDITY" | "INTERNAL_CONTROLS" | "RELATED_PARTY" | "TAX" |
               "LEASES_OR_DEBT" | "MD_A_DISCLOSURE" | "RISK_FACTORS" | "EXECUTIVE_COMPENSATION" |
               "LEGAL_OR_CONTINGENCIES" | "XBRL_OR_FORMAT" | "OTHER",
      "nature": "REQUEST_EXPLANATION" | "REQUEST_EXPANDED_DISCLOSURE" | "CHALLENGE_ACCOUNTING_TREATMENT" |
                "REQUEST_RESTATEMENT_OR_AMENDMENT" | "REQUEST_SUPPORTING_ANALYSIS",
      "affects_reported_revenue_or_earnings": boolean,
      "severity": 1 | 2 | 3 | 4 | 5,
      "registrant_response": "CONCEDED" | "WILL_REVISE_PROSPECTIVELY" | "DEFENDED" | "PARTIAL" | "NO_RESPONSE_SUPPLIED",
      "evidence_quote": string | null
    }
  ],
  "core_accounting_issue_count": integer,
  "max_severity": integer,
  "letter_length_words": integer,
  "benign_but_long": boolean,
  "restatement_risk": "LOW" | "MODERATE" | "HIGH",
  "confidence": number
}

Severity guide: 5 = staff challenges the accounting for revenue or asks for restatement;
4 = staff challenges a judgement that moves earnings or going-concern; 3 = substantive
disclosure gap; 2 = clarification; 1 = formatting or XBRL. benign_but_long is true when
letter_length_words exceeds 1500 and max_severity is at most 2. confidence in [0,1].
Return only the JSON.
```

The trade shorts firms with `restatement_risk = "HIGH"` or any `REVENUE_RECOGNITION` comment at severity 4–5 for about 50 trading days from public release, with extra weight where Form 4 shows discretionary sales in the preceding weeks; the contrarian long on `benign_but_long = true` is a hypothesis to test, not a documented effect.

## Cross-cutting pipeline and evaluation issues decide whether any thesis survives contact

Look-ahead bias is the central methodological risk for any LLM backtest and the literature now offers four defences. Sarkar and Vafa show that models trained on unrestricted internet corpora "inevitably embed information from the future" ([Semantic Scholar](https://www.semanticscholar.org/paper/Lookahead-Bias-in-Pretrained-Language-Models-Sarkar-Vafa/e5097ccd4477c454e0df52945cef4ba74d255b91)). Glasserman and Lin (Journal of Financial Data Science 6(1), 2024) separate look-ahead from "distraction", the interference of general firm knowledge with sentiment measurement, and find anonymised headlines outperformed non-anonymised ones in-sample, so anonymisation is useful live as well as in backtests ([arXiv 2309.17322](https://arxiv.org/pdf/2309.17322)). Kim, Muhn and Nikolaev's 2024 statement-analysis paper, read in full, demonstrates the audit: asked to guess the firm from anonymised statements, GPT-4 was right 0.07% of the time and almost always guessed Tesla, Facebook or Amazon, year guesses were 2.95% correct, and an out-of-training-window FY2022→FY2023 test gave 58.96% accuracy against 60.3% in-sample ([BFI WP 2024-65](https://readwise-assets.s3.amazonaws.com/media/wisereads/articles/financial-statement-analysis-w/BFI_WP_2024-65.pdf)). Gao, Jiang and Yan's "Lookahead Propensity" uses a date-only recall query to estimate the probability the model has internalised the realised outcome and finds it "collapses essentially to zero right after the training-data cutoff" ([arXiv 2512.23847](https://arxiv.org/pdf/2512.23847)), and chronologically consistent models such as ChronoBERT/ChronoGPT eliminate leakage by construction at the cost of lagging unconstrained models ([arXiv 2502.21206](https://arxiv.org/pdf/2502.21206)). The defensible protocol is therefore: anonymise issuer names and absolute dates in every backtest prompt (every prompt above already does), run the LAP probe by year on the backtest universe and haircut contaminated years, report results separately for the post-cutoff window of whichever model is used, and keep temperature at 0 while still sampling several times or across models, because Chon, Kim and Kim (Finance Research Letters 2025) find repeated identical queries change 42–79% of selected stocks in open-ended recommendation tasks ([ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S1544612325021762)), and GPT-4 and Gemini 1.5 Pro disagreed on about 6% of earnings-direction calls in KMN. The prompts above return quote-grounded evidence and a confidence field for the same reason Dolphin et al. built a quality score: precision is a filter the fund can tune.

Filing timestamps are the second trap. Submissions beginning transmission at or before 5:30 p.m. ET get that day's filing date; after 5:30 p.m. they receive the next business day's filing date and are not disseminated until the next business day, with an explicit exception for Forms 3, 4, 5 and 144 and their amendments, which keep the same-day date and are disseminated until 10:00 p.m. ([SEC filing-status guide](https://www.sec.gov/submit-filings/filer-support-resources/how-do-i-guides/determine-status-my-filing)); 13D and 13G moved to a 10 p.m. cut-off in 2024 ([SEC Release 33-11253](https://www.sec.gov/files/rules/final/2023/33-11253.pdf)). Backtests keyed on filing date will mis-align after-hours 10-Ks and 8-Ks by a day, and because bad news clusters after hours and on Fridays, the mis-alignment is correlated with the signal. The `acceptanceDateTime` field in the submissions API and the bulk `submissions.zip` is the correct anchor, with trades allowed only at the next tradable print after dissemination ([EDGAR APIs](https://www.sec.gov/search-filings/edgar-application-programming-interfaces)). Filings typically appear on sec.gov within one to three minutes of the EDGAR timestamp, with the submissions API processing in under a second ([SEC Developer FAQ](https://www.sec.gov/os/webmaster-faq)). The full-index files from 1994Q3 onward give a survivorship-free filing universe ([Accessing EDGAR Data](https://www.sec.gov/search-filings/edgar-search-assistance/accessing-edgar-data)), which matters because the S&P 100 Lazy Prices replication found every quintile showing 2–8% annual alpha from survivorship alone.

EDGAR access and cost are not the constraints. The SEC allows at most 10 requests per second with a declared User-Agent of the form "Company Name contact@domain.com" and blocks undeclared tools ([Accessing EDGAR Data](https://www.sec.gov/search-filings/edgar-search-assistance/accessing-edgar-data)); full-text search covers all filings since 2001 with phrase, boolean, proximity and form-type filters and can query XML element content ([EFTS FAQ](https://www.sec.gov/edgar/search/efts-faq.html)). Calendar 2025 held 6,690 10-Ks, 17,289 10-Qs, 67,651 8-Ks, 351,055 Form 4s, 68,810 Form 144s, 11,274 Schedule 13Ds and 49,060 Schedule 13Gs ([EDGAR full-index, own computation](https://www.sec.gov/Archives/edgar/full-index/)). The notes' own token estimate, using an unsourced 1.3–1.5 tokens-per-word rule of thumb on sampled 2025-Q4 documents, puts a full annual pass at roughly 1.5–3.5 billion input tokens plus 0.5–1 billion output tokens, which at the Anthropic list prices cached in the session's Claude API skill (Sonnet-class at $2/$10 per million input/output tokens, Opus-class at $4/$20, batch at half price) implies about $8k–$17k per year on a Sonnet-class model and $16k–$34k on an Opus-class model before batch discounts, tripled if every document is sampled three times; these prices come from a skill cache rather than a public page and should be checked. Form 4 dominates count but is under 10% of tokens; 10-Qs dominate tokens; a tiered design that triages 8-K, Form 4 and 13G with a cheap model and reserves the frontier model for 10-K/10-Q sections, 13D narrative and comment letters keeps the bill in the low tens of thousands. The engineering effort is in sub-minute polling during 6 a.m.–10 p.m. ET, stripping inline-XBRL wrappers (one rendition was 277k "words" of tags), and item segmentation.

Transaction costs and capacity bind where the effects are. Every thesis in this report is strongest in small caps: Lakonishok–Lee and CMP for insiders, deHaan et al. for 13Ds, the Lazy Prices saturation for large-cap text, and the FRL 2024 result that Form 4 returns vanish under dollar caps. KMN's equal-weighted Sharpe of 3.36 falls to 2.84 with 10 bp one-way costs, but the value-weighted figure falls from 1.47 to 0.95, which the notes treat as the realistic ceiling for a capacity-constrained strategy ([BFI WP 2024-65](https://readwise-assets.s3.amazonaws.com/media/wisereads/articles/financial-statement-analysis-w/BFI_WP_2024-65.pdf)); a 10 bp assumption is optimistic for the micro-caps where 13D and insider effects concentrate. Finally, no vendor or fund publicly reports Sharpe or alpha for an LLM-on-filings signal; AlphaSense, Fintool, Hudson Labs, Brightwave and Man Group's AlphaGPT publish coverage, latency and workflow claims, not return attribution ([Marvin Labs comparison](https://www.marvin-labs.com/blog/ai-tools-for-equity-research-complete-platform-comparison/); [Bloomberg on Man Group](https://www.bloomberg.com/news/articles/2025-07-10/man-group-says-agentic-ai-is-now-devising-quant-trading-signals)), so the academic results above are the only quantified evidence the founder has.

## Theses that did not make the cut, and why

Four candidates have real evidence but fail the "investable text signal" test as stated. MD&A going-concern language plus tone has significant explanatory power for bankruptcy up to three years ahead, incremental to ratios and the auditor's opinion, in Mayew, Sethuraman and Venkatachalam (The Accounting Review 90(4), 2015) ([citing paper](https://doi.org/10.1111/1911-3838.12150)), and Donovan, Jennings, Koharki and Lee (Review of Accounting Studies 2021) improve out-of-sample prediction of bankruptcies, spreads and downgrades from MD&A and call text ([Springer](https://link.springer.com/article/10.1007/s11142-020-09575-4)); this is a credit and short screen with no published equity-alpha test, best used as an overlay on Theses 1 and 3. S-1/424B4 language is the best-documented "other form": a one-standard-deviation increase in uncertain or negative language raises first-day returns by roughly 3% and 4% in Loughran and McDonald (JFE 109(2), 2013) ([ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0304405X13000603)) and standard versus informative content moves underpricing by about +4% and −8% per standard deviation in Hanley and Hoberg (RFS 23(7), 2010) ([JSTOR](https://www.jstor.org/stable/40782968)), but the tradable expression is IPO allocation, not secondary-market alpha, and a recent measurement study found the surviving text effect disappeared after controlling for deal terms ([GitHub summary](https://github.com/leeyawnnn/ipo_underpricing_model)). Hoberg and Phillips' text-based industry momentum from Item 1 product descriptions generates "economically large" momentum profits exceeding own-firm momentum, strongest where SIC and TNIC peers disagree (JFQA 2018) ([Tuck PDF](https://faculty.tuck.dartmouth.edu/images/uploads/faculty/gordon-phillips/hoberg_phillips_TNICmomJFQA_FinV1.pdf)), but the monthly spreads could not be verified and no post-2018 replication exists; the data library is public, so the fund can buy rather than build it. EX-10 credit agreements are the richest exhibit for an LLM, with 32% containing explicit capex restrictions and new restrictions followed by higher market value in Nini, Smith and Sufi (JFE 2009) ([SSRN](https://www.ssrn.com/abstract=928688)), but no paper reports a covenant-text long-short alpha and extraction accuracy degrades mid-document ([covenant-extraction-eval](https://github.com/stendeze/covenant-extraction-eval)). Readability and file size predict volatility and forecast dispersion rather than direction ([Loughran & McDonald 2014](https://onlinelibrary.wiley.com/doi/abs/10.1111/jofi.12162)), Critical Audit Matters produce a volatility and dispersion response that the authors frame as possible misinterpretation ([Bucknell record](https://digitalcommons.bucknell.edu/fac_journ/1966/)), and 13F best-ideas cloning earns 2.8–4.5% per year ([HBS WP 21-004](https://www.hbs.edu/ris/download.aspx?name=21-004.pdf)) but contains no narrative text at all.

## Conclusion

The honest reading of this evidence is that an LLM-on-filings fund is a measurement business wearing an alpha business's clothes. The theses with the strongest and most recent support are the ones where the LLM converts a semi-structured event into a typed, quote-grounded record (which accounting area, how uncertain, which demand, which footnote category) and a conventional event-study portfolio does the rest; the theses where the LLM is asked to read tone or novelty from long narrative are precisely the ones with documented decay, failed large-cap replication and issuer adaptation. That asymmetry also points to the fund's durable edge: issuers can and do rewrite prose to game lexicons, but they cannot rewrite the fact that a restatement is about revenue, that a sale was a gift to a family foundation, or that an activist named a number of board seats.

The practical implication is a staged build. The first six months should re-estimate Theses 3, 4 and 5 on 2020–2026 data using acceptance timestamps, anonymised prompts and a post-cutoff holdout, because those are the theses whose event-day effects have held through 2021–2023 samples and whose text sub-types have at least one published return result each. Theses 1, 2 and 6 should be run in parallel as research rather than capital, with the explicit goal of producing the post-2014 10-Q update test, the LLM-summarised abnormal-tone test and the post-2016 comment-letter re-test that the literature lacks; if they fail, the fund will have learned so for a few thousand dollars of tokens, and if they succeed, the fund will own the only modern evidence. The founder's real question is therefore not whether the signals exist but whether a capacity-limited, small-cap, event-driven book can support the fund's cost base, and that is a question the research cannot answer for them.
