# Samrat Banerjee

### Derivatives & Quantitative Finance — pricing, volatility, hedging and risk, engineered in Python and validated on real exchange data

**Target roles:** Derivatives Analyst · Options / Flow Trading · Quantitative Research · Market & Model Risk

MBA (Financial Management), University of Calcutta · BCA (Hons), Techno India University · CFA Level 1 candidate

Most student portfolios show toy models on toy data. This one is built the other way: **real NSE exchange files, real company financials, real credit data** — and every headline number below is reproduced by the code and its test suite before it is printed here. Where a model fails, the failure is the case study.

## Currently

- **Building:** Stochastic Volatility Lab — Heston and SABR models calibrated to the real NIFTY smile, fit compared slice by slice
- **Latest shipped:** Rates Lab — Treasury curve bootstrapping, swaps, swaptions and curve PCA on 710 real curves
- **Studying:** CFA Level 1 — quantitative methods and derivatives

---

## The Derivatives Stack — organised the way a desk actually works

### 1 · PRICE — [GreeksLab](https://github.com/risootooo/greeks-lab)
*What is it worth, and what are its sensitivities?*
Black-Scholes / binomial / Monte Carlo pricers (agree to ±0.25 on a 400k-path cross-check) · full Greek surface including **second-order vanna, charm, vomma** · IV solver that refuses arbitrage-violating prints · real NSE bhavcopy chain analytics: IV smile, **dealer GEX +₹12,619 crore per 1%**, gamma flip 23,872, max pain, put-call parity regression (real chain implies a forward −121 pts vs spot — documented, not hidden) · **47 tests**

### 2 · SURFACE — [VolSurface Atlas](https://github.com/risootooo/vol-surface-atlas)
*How does implied volatility actually behave?*
10,633 real IV points from **220 days of NSE bhavcopy** · SVI calibration across 69 slices (median RMSE 1.09 vol pts) · PCA of surface dynamics: **96.3% of daily change is one level shift** · real event studies — Mar 2026 crash (ATM IV 17.6% → 34.2%, term structure inverted) and the Apr 2026 vol crush (28.5% → 18.4% in one session)

### 3 · HEDGE — [Hedge Lab](https://github.com/risootooo/hedge-lab)
*Can you run the book day to day — and explain every rupee of its P&L?*
A short-vol NIFTY book held across **10 consecutive real option chains** · three hedging regimes (unhedged **−₹139,912** / daily delta hedge **+₹32,183** / tolerance band +₹23,998) · **Greeks P&L attribution that sums to actual P&L**: theta +₹93,302, gamma −₹73,102, vega −₹55,080, net delta exactly ₹0 · the worst hedged day was a *vega* day, not a spot day — delta hedging can't fix it, and the attribution proves it · **28 tests**

### 4 · STRUCTURE — [Exotics & Structured Products Lab](https://github.com/risootooo/exotics-lab)
*What does a structuring desk actually sell — and where is its margin?*
Barrier / Asian / lookback / cliquet options priced by Monte Carlo **and** an independent Crank–Nicolson PDE (max disagreement 0.026 vol points) · a 3-year NIFTY **autocallable**: fair coupon **7.11% p.a.**, P(autocall in year 1) 79.4%, and at a typical marketed 6.11% the note is worth 99.29 — the **0.71-point issuer margin**, decomposed leg by leg · barrier delta flips sign approaching the barrier (+0.10 → −0.18), measured by both engines · calibrated to the real 3 Nov 2026 chain · **29 tests**

### 5 · RATES — [Rates Lab](https://github.com/risootooo/rates-lab)
*The largest derivatives market in the world, from the official curve up*
Bootstrapping on **710 real U.S. Treasury curves** (2024–26, Treasury.gov) · par vs zero curve, key-rate DV01 ladders · interest-rate swaps, caps, and **Black-76 vs Hull-White** swaptions (ATM agreement 0.09bp; the models split −8.3% out-of-the-money, and the repo explains why) · curve PCA on real history: level 79.8% / slope 10.1% / curvature 3.6% · the hedge lesson: a DV01-neutral 2y hedge of a 10y swap leaves **~2× the gross curve risk** · **21 tests**

### 6 · VALIDATE — [EdgeGate](https://github.com/risootooo/edgegate) ⭐ flagship
*Is this backtest lying?*
Monte Carlo permutation tests · **deflated Sharpe ratio** (Bailey & López de Prado) · walk-forward consistency · bootstrap drawdowns · 1×/2×/3× cost stress · hard PASS / FAIL / UNPROVEN verdicts — a PF 1.93 curve-fit mirage **fails**, a modest 1,500-trade edge **passes**, the same edge at 600 trades is honestly **UNPROVEN**

### 7 · RISK — [VaR Engine Pro](https://github.com/risootooo/var-risk-engine)
*How much can we lose, and would Basel believe the number?*
9 VaR/ES estimators · Basel backtesting suite (Kupiec, Christoffersen, traffic-light) · GARCH filtered historical simulation · EVT/GPD tails · stressed VaR · Euler component ES · figures cross-checked against an independent library

### 8 · RESEARCH WORKFLOW — [Finance Council](https://github.com/risootooo/finance-council)
*Multi-model AI deliberation for research questions*
Independent answers → anonymised Borda peer ranking → chairman synthesis with dissent preserved on record · cost/latency accounting · offline demo, no API key · original code, concept credited to Karpathy's llm-council

**In build now:** *Stochastic Volatility Lab* (Heston and SABR calibrated to the real NIFTY smile)

---

## Verified results — real data, reproducible numbers

| Finding | Evidence |
|---|---|
| An ATM straddle lost **₹9,695/lot (−28.5%) in 5 days while spot rallied +4.9%** | Real NSE premiums, 28 Oct – 3 Nov 2026 (GreeksLab) |
| Daily delta hedging turned **−₹139,912 into +₹32,183**; theta +₹93,302 fought gamma −₹73,102 and vega −₹55,080 | Real chains, 21 Oct – 3 Nov 2026, attribution sums to actual P&L (Hedge Lab) |
| A marketed autocall coupon of 6.11% leaves the note worth **99.29** — the fair coupon is **7.11%**, and the 0.71-pt gap is the issuer's margin | Real NIFTY calibration; MC vs PDE agree to 0.026 vol pts (Exotics Lab) |
| A DV01-neutral hedge (10y swap hedged with 2y swaps only) leaves **~2× the gross curve risk** and a 1bp 2s10s twist costs 1.8× the DV01 hedged | 710 real Treasury curves, PCA + key-rate residuals (Rates Lab) |
| The market prices Infosys for **9.4% growth**; it delivered **3.4%** | Reverse DCF on real financials (Valuation Lab) |
| Yahoo's Infosys beta is **0.02** — using it fabricates +60% upside | Own 60-month regression: 0.80 (Valuation Lab) |
| A bank's default 0.50 credit cut-off **loses money**; the cost-optimal 0.196 earns **+16,248 DM** | Real UCI credit data, AUC 0.786 (Credit Scorecard Pro) |
| **96.3%** of NIFTY vol-surface movement is a single level shift | PCA over 10,633 real IV points (VolSurface Atlas) |
| A "cointegrated" pair (PEP/KO, p≈0.028) **flips its hedge ratio's sign** split-sample | Real prices 2021–26 (StatArb Lab) |
| Over 2019–26 a dual-momentum book returned **+144.6%** — and the benchmark did **+219.1%** | Printed in the headline, not buried (StatArb Lab) |

## Full project index

| Domain | Project | Core content |
|---|---|---|
| Derivatives | [GreeksLab](https://github.com/risootooo/greeks-lab) · [VolSurface Atlas](https://github.com/risootooo/vol-surface-atlas) · [Hedge Lab](https://github.com/risootooo/hedge-lab) · [Exotics Lab](https://github.com/risootooo/exotics-lab) | Pricing, Greeks, IV surfaces, GEX, SVI, PCA, delta-hedging, P&L attribution, exotics, autocallables, PDE methods |
| Trading research | [EdgeGate](https://github.com/risootooo/edgegate) · [StatArb Lab](https://github.com/risootooo/stat-arb-lab) · [Factor Lab](https://github.com/risootooo/factor-lab) | Validation statistics, pairs, Kalman hedge ratios, cross-sectional factors with IC / Fama-MacBeth / Bonferroni zoo check — verdict on Indian data: 0 of 4 textbook factors survive |
| Rates & credit | [Rates Lab](https://github.com/risootooo/rates-lab) · [VaR Engine Pro](https://github.com/risootooo/var-risk-engine) · [Credit Scorecard Pro](https://github.com/risootooo/credit-scorecard-pro) | Curve bootstrapping, swaps, swaptions, curve PCA, VaR/ES, Basel backtests, WOE scorecards, fairness audit |
| Portfolio & valuation | [Portfolio Optimizer Pro](https://github.com/risootooo/portfolio-optimizer) · [Valuation Lab](https://github.com/risootooo/valuation-lab) | HRP, risk parity, Black-Litterman, DCF, reverse DCF, comps |
| AI systems | [Finance Council](https://github.com/risootooo/finance-council) | Multi-model deliberation, evaluation, cost accounting |
| Engineering | [DSA — Python](https://github.com/risootooo/dsa-challenges-python) | 50 problems, pattern playbook, complexity notes, full test suite |

**370+ automated tests across the public repos. Every project: self-contained offline dashboard, documented assumptions, stated limitations.**

## How I work — the standards these repos are held to

- **Real data or labelled synthetic** — provenance and download date in every repo; synthetic data is watermarked as synthetic
- **No-lookahead, costs in, out-of-sample reported** — including when the honest result is "the benchmark won"
- **Cross-verification** — pricers checked against each other, risk numbers against independent implementations, vendor data audited before use (see the beta trap above)
- **Tests that can fail for the right reason** — several bugs in these repos were caught by their own suites during construction, and the READMEs say which
- **Limitations printed, not footnoted away** — survivorship, settlement-print noise, assumption sensitivity, sample sizes

## Toolkit

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?logo=scipy&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?logo=plotly&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?logo=pytest&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white)

**Derivatives:** Black-Scholes-Merton · binomial trees · Monte Carlo (antithetic, control variates) · finite-difference Greeks · second-order Greeks · SVI surfaces · implied-volatility dynamics · GEX / positioning analytics
**Quant & risk:** VaR/ES & Basel backtesting · GARCH · EVT · cointegration & Kalman filtering · deflated Sharpe / multiple-testing control · factor & PCA methods
**Finance:** DCF & reverse DCF · trading comparables · credit scorecards (WOE/IV) · portfolio construction (HRP, Black-Litterman)

## Connect

- LinkedIn: [samrat-banerjee-919a45447](https://www.linkedin.com/in/samrat-banerjee-919a45447/)
- GitHub: [github.com/risootooo](https://github.com/risootooo)

![Samrat's GitHub stats](https://github-readme-stats.vercel.app/api?username=risootooo&show_icons=true&theme=github_dark&hide_border=true)

*All projects are research and educational work — nothing here is investment advice, and no result is a promise of trading performance.*
