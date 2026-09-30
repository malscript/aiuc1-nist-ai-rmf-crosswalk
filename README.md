# AIUC-1 to ISO/IEC 42001 crosswalk

This project maps AIUC-1 requirements to ISO/IEC 42001:2023 so you can see where an organization certified to ISO/IEC 42001 already covers AIUC-1, and where gaps remain.

Mappings are kept in a CSV. A small Python script turns that CSV into a coverage report.

## Scope

Version 0.1 covers one AIUC-1 domain: **Data & Privacy**. Other domains are out of scope for this version.

The three rows in `data/mapping.csv` are placeholders. Replace the ids, summaries, clause references, coverage values, and notes with your own. Do not copy text from the ISO standard into this repository.

## Mapping file

`data/mapping.csv` has these columns:

| Column | Meaning |
| --- | --- |
| `aiuc1_id` | Identifier for the AIUC-1 requirement |
| `aiuc1_domain` | Domain name |
| `aiuc1_requirement_summary` | Short original summary of the requirement |
| `iso42001_refs` | ISO/IEC 42001 clause references that relate to the requirement. Leave blank when coverage is `none`. |
| `coverage` | `full`, `partial`, or `none` |
| `notes` | Optional context, in your own words |

`full` means the cited clauses already address the requirement. `partial` means they address only part of it. `none` means no cited clause applies. A row marked `full` or `partial` must include at least one clause reference.

## Run the report

Requires Python 3 and the standard library only. From the repository root:

```bash
python3 coverage_report.py
```

The script reads `data/mapping.csv` and writes `reports/coverage_report.md`. It checks that the required columns are present and that every `coverage` value is `full`, `partial`, or `none`. Invalid rows are printed and left out of the totals. It also warns when `coverage` is `full` or `partial` but `iso42001_refs` is empty.

The report has two parts:

- a summary table with the count and percentage of requirements at each coverage level
- a gap list of every requirement marked `none` or `partial`

## Copyright

ISO/IEC 42001:2023 is copyrighted. This project does not reproduce the text of the standard. It records clause references and original summaries only.
