# AIUC-1 to NIST AI RMF crosswalk

This project maps AIUC-1 requirements to the NIST AI Risk Management Framework (AI RMF) so you can see where the AI RMF already covers AIUC-1, and where gaps remain.

Mappings are kept in a CSV. A small Python script turns that CSV into a coverage report.

ISO/IEC 42001 references in this project are not taken from the ISO standard. They are derived from NIST's published crosswalk from the AI RMF to ISO/IEC 42001, which NIST built against the FDIS draft. No ISO text is reproduced. The file records clause references and original summaries only.

## Scope

The three rows in `data/mapping.csv` are placeholders. Replace the ids, summaries, references, ratings, and notes with your own. Do not copy ISO/IEC 42001 text into this repository.

## Mapping file

`data/mapping.csv` has these columns:

| Column | Meaning |
| --- | --- |
| `aiuc1_id` | Identifier for the AIUC-1 requirement |
| `aiuc1_requirement_summary` | Short original summary of the requirement |
| `ai_rmf_refs` | NIST AI RMF references that relate to the requirement. Leave blank when coverage is `none`. |
| `coverage` | This project's rating: `full`, `partial`, or `none` |
| `iso42001_refs_via_nist_crosswalk` | ISO/IEC 42001 clause references derived from NIST's published AI RMF to ISO/IEC 42001 crosswalk (built against the FDIS draft). Leave blank when there is no derived reference. |
| `official_aiuc1_crosswalk_rating` | Rating from the official AIUC-1 crosswalk: `full`, `partial`, `none`, or blank if none is recorded |
| `notes` | Optional context, in your own words |

`full` means the cited AI RMF references already address the requirement. `partial` means they address only part of it. `none` means no cited AI RMF reference applies. A row marked `full` or `partial` must include at least one AI RMF reference.

## Run the report

Requires Python 3 and the standard library only. From the repository root:

```bash
python3 coverage_report.py
```

The script reads `data/mapping.csv` and writes `reports/coverage_report.md`. It checks that the required columns are present and that every `coverage` value is `full`, `partial`, or `none`. A non-blank `official_aiuc1_crosswalk_rating` must use those same values. Invalid rows are printed and left out of the totals. It also warns when `coverage` is `full` or `partial` but `ai_rmf_refs` is empty.

The report has three parts:

- a summary table with the count and percentage of requirements at each coverage level
- a gap list of every requirement marked `none` or `partial`
- a list of rows where `coverage` differs from `official_aiuc1_crosswalk_rating` (a blank official rating counts as a difference)

## ISO text

ISO/IEC 42001 is copyrighted. This project does not reproduce it. ISO/IEC 42001 references are clause identifiers derived from NIST's published AI RMF to ISO/IEC 42001 crosswalk, which was built against the FDIS draft.
