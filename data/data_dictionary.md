# Data Dictionary — Card B: FSA Food Hygiene Ratings

**What it is:** The food hygiene rating or inspection result for food businesses across England, Wales and Northern Ireland (FHRS) and Scotland (FHIS). One row per business. Updated daily.

**Source:** `https://ratings.food.gov.uk/open-data`
Full CSV: `https://safhrsprodstorage.blob.core.windows.net/opendatafileblobstorage/FHRS_All_en-GB.csv`
**Licence:** FSA open data terms and conditions.
**File you load:** `fhrs_subset.csv` (trimmed to Manchester). Full file: `fhrs_full.csv`.

## Columns (23, in order)

| # | Column | Type | Meaning |
|---|---|---|---|
| 0 | `AddressLine1` | string | Address line 1 |
| 1 | `AddressLine2` | string | Address line 2 |
| 2 | `AddressLine3` | string | Address line 3 (often the town) |
| 3 | `AddressLine4` | string | Address line 4 |
| 4 | `BusinessTypeID` | int | Code for the business type |
| 5 | `FHRSID` | string | System-unique ID for the establishment |
| 6 | `BusinessName` | string | Name of the business |
| 7 | `BusinessType` | string | e.g. `Restaurant or cafe`, `Takeaway`, `Pub`, `Supermarket`, `Mobile caterer` |
| 8 | `ConfidenceInManagement` | int / blank | Sub-score: confidence in management |
| 9 | `Hygiene` | int / blank | Sub-score: hygiene |
| 10 | `Latitude` | float / blank | Latitude (WGS84) |
| 11 | `LocalAuthorityBusinessID` | string | LA's own ID for the business |
| 12 | `LocalAuthorityCode` | string | LA code |
| 13 | `LocalAuthorityName` | string | Local authority name |
| 14 | `Longitude` | float / blank | Longitude (WGS84) |
| 15 | `NewRatingPending` | string | `True`/`False` — a new rating is in the appeals/notification period |
| 16 | `PostCode` | string | Postcode |
| 17 | `RatingDate` | date | Date of the inspection that produced the rating |
| 18 | `RatingKey` | string | Internal rating key |
| 19 | `RatingValue` | int / blank | Hygiene rating **0–5** (5 = best). Blank = not yet rated / awaiting publication |
| 20 | `RightToReply` | string | Free-text right-to-reply, usually blank |
| 21 | `SchemeType` | string | `FHRS` (Eng/Wal/NI) or `FHIS` (Scotland) |
| 22 | `Structural` | int / blank | Sub-score: structural |

## Quirks (read before you build)

- **`RatingValue` can be blank** — "Awaiting Publication" (business has appealed) or not yet rated. Handle nulls; don't treat blank as 0.
- **The sub-scores are `Hygiene`, `Structural`, `ConfidenceInManagement`** — they can be blank on a rescore. Only `RatingValue` is reliable across all rows.
- **Scotland uses FHIS** — sub-scores are **not available** for `SchemeType == "FHIS"`.
- **`NewRatingPending == "True"`** means the published rating may change — note it if you build a "live" tool.
- **Coordinates can be missing** for businesses operating from a private address — check `Latitude`/`Longitude` nulls before mapping.
- **There is no `TownCity` column** — the town is usually in `AddressLine3` (or `PostCode`). Filter by `LocalAuthorityName` for a geographic cut.
- **Volume:** full file ~614k rows. The subset is pre-trimmed to Manchester (~6,600 rows).

## Attribution (show this in your product)

> Food hygiene rating data © Food Standards Agency, used under the FSA open data terms and conditions. Data updated daily.

## Starter questions

- **Search tool:** "Find food businesses rated 4 or 5 near a given postcode / town." (Filter `RatingValue >= 4`, sort by distance if you have a centre point.)
- **Dashboard:** Distribution of ratings by `BusinessType` or `LocalAuthorityName` — which area / business type is cleanest?
- **Predictor:** Predict `RatingValue` from `BusinessType` + `LocalAuthorityName` (baseline: most common rating per business type).
