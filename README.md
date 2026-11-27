
# 2026 US Senate: Polls vs Prediction Markets

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/steevesolomon-eng/senate-polls-vs-markets/blob/main/senate_project.ipynb)

Code and data for an observational study comparing published polling averages with Polymarket prices across the 2026 US Senate elections. The full write-up is in the accompanying paper, *Polls & Prediction Markets* 

The study asks five questions:

1. **Co-movement:** how closely did polls and market prices move together?
2. **Disagreement:** where and when did they point to different outcomes?
3. **Poll releases:** did prices move when a poll was published?
4. **Forecast evaluation:** how well did each call the winners, and how well calibrated were the probabilities?
5. **Method sensitivity:** do the findings change with other ways of averaging the polls?

## Sample at a glance

- 34 Polymarket statewide races; 16 analysis states with enough polling and a clear Democratic-Republican matchup, 12 of them competitive.
- 15 head-to-head races are scored for both polls and markets (Montana's three-way race is scored for the market only).
- Polls: 2,189 rows and 783 polls (Polling Desk export plus a later supplement).
- Prices: 49,273 Polymarket observations (Democratic YES price, 3-hour buckets).
- Results: civicAPI snapshot of Nov 11, 2026 (09:03 UTC). **These counts are unofficial until certified.**

## Headline results

- On Nov 1, polls and markets ranked the 15 states almost identically (Spearman 0.96); week-to-week changes showed no reliable relationship.
- On the final day, polls and markets each named 13 of the 15 head-to-head winners, missing the same two close races (Iowa and South Carolina).
- Both shared one large miss: the Democrats beat the final poll average in all 15 races, by 4.52 points on average.
- Poll-implied probabilities scored lower Brier scores than market prices under an assumed forecast error. This depends on that assumption and on one election.

All findings are descriptive and do not show causation. See the paper for the limits.

## How to run

**Option A: Colab, nothing to download (default).**
1. Click the Colab badge above and sign in to Google (needed only to run).
2. Run the notebook from top to bottom. The setup cell clones this repository and reads the data from `data/`.
3. **First run only:** the raw Polymarket price file is not in the repository (see *Data and credits*). Set `REFRESH = True` in the setup cell, run the setup cell and Section 9 (the only part that downloads Polymarket data), set `REFRESH = False`, then run from the top.

**Option B: use your own Google Drive.**
1. Upload this repository's `data` folder to your Drive and name it `senate_project`.
2. Set `USE_DRIVE = True` in the setup cell and run from the top. Drive asks for permission once per session.
3. Do the same first-run Polymarket step as above.

Notes:
- A new Polymarket pull includes prices after Nov 2, 2026. The analysis cuts them off at Nov 2, so results are unaffected, but the row count will differ from 49,273.
- If `deepsyte_candidates_2026.csv` is missing, the notebook downloads it from DeepSyte's open-data page (used for party labels only).
- A Colab Secret named `GOV_DATA_API_KEY` is needed only if the FEC cache file is missing. It is included here, so you normally will not need it.
- Anything written during a run lives in that Colab session and disappears when it disconnects; download what you want to keep.
- To re-pull FEC data you need your own free key from api.data.gov, stored as a Colab Secret named `GOV_DATA_API_KEY`

## What is in this repository

```
senate_project.ipynb      the full analysis (Sections 1-10, with saved outputs)
data/
  inputs                  polling_desk_merged.csv, polling_desk_original.csv,
                          polling_desk_update.csv, polling_desk_added_polls.csv,
                          polymarket_senate_market_register.csv,
                          polymarket_historical_coverage.csv,
                          fec_senate_2026_candidates_RAW.csv,
                          civicapi_race_87528_20261111_0903UTC.json,
                          all_35_us_senate_state_results.csv
  derived tables          final_25_state_sample.csv, poll_classification.csv,
                          polls_25_with_party.csv, matchups_general_clean.csv,
                          margin_series_reference.csv,
                          disagreement_weekly_competitive.csv,
                          analysis3_events.csv, results_by_state.csv,
                          external_aggregators.csv
  figures                 fig_*.png (nine figures used in the paper)
```

The notebook sections follow the paper: Analysis 1 (Section 3), Analysis 2 (Section 4), Analysis 3 (Section 5), Analysis 4 (Section 6), Analysis 5 (Section 7), saving figures (Section 8), Polymarket refresh (Section 9) and the polling-file rebuild (Section 10).

## Data and credits

- **Polls:** Polling Desk (polling-desk.com), with poll data from VoteHub and The New York Times, licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The data were filtered, merged and reformatted for this study.
- **Election results:** civicAPI (https://civicapi.org). Counts are unofficial until certified.
- **Candidates and parties:** OpenFEC API (api.open.fec.gov) and DeepSyte (deepsyte.app).
- **Market prices:** Polymarket (Gamma API for market discovery, Data API v2 `prices-history` for prices). The raw price history is **not redistributed** here; regenerate it with Section 9 of the notebook. Derived tables built from it are included.
- **Outside poll averages:** Decision Desk HQ and PollCheck figures are hand-entered with their source and retrieval date, and cited with attribution (see `external_aggregators.csv` and the paper's Appendix E).

Each provider's own terms apply to its data. Check them before reusing anything beyond this study.

## Limitations in brief

One election, 12 to 16 states with correlated errors; provisional vote counts; equal-weighted polls with no house-effect adjustment; Brier scores for polls rest on an assumed forecast-error SD; several tests were added after earlier results were seen and are labelled exploratory. Full list in the paper.

## Licence and citation

- Code: [MIT](LICENSE) (add a `LICENSE` file; see GitHub's "Add file > Create new file > LICENSE" template picker).
- Data: under the original providers' terms, as above.
- Please cite as: *Steeve Solomon. Polls & Prediction Markets: the 2026 US Senate elections.*

## Contact

Steeve Solomon/stevejr162@gmail.com
