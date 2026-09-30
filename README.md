# AIUC-1 to NIST AI RMF crosswalk

This project builds on AIUC-1's published NIST AI RMF crosswalk. It adds coverage strength ratings, additional subcategory mappings, and ISO/IEC 42001 references derived from NIST's published crosswalk from the AI RMF to ISO/IEC 42001.

Mappings are kept in a CSV. A small Python script turns that CSV into a coverage report.

ISO/IEC 42001 references in this project are not taken from the ISO standard. They are derived from NIST's published crosswalk, which NIST built against the FDIS draft. No ISO text is reproduced. The file records clause references and original summaries only.

## Scope

Version 0.1 maps Data & Privacy requirements A001 through A007. The summaries in `data/mapping.csv` are original wording. Do not copy ISO/IEC 42001 text into this repository.

## Mapping file

`data/mapping.csv` has these columns:

| Column | Meaning |
| --- | --- |
| `aiuc1_id` | Identifier for the AIUC-1 requirement |
| `aiuc1_requirement_summary` | Short original summary of the requirement |
| `ai_rmf_refs` | NIST AI RMF subcategories chosen for this requirement, including any that go beyond AIUC-1's published crosswalk. Separate multiple references with semicolons. Leave blank when coverage is `none`. |
| `coverage` | This project's coverage strength rating: `full`, `partial`, or `none` |
| `iso42001_refs_via_nist_crosswalk` | ISO/IEC 42001 clause references derived from NIST's published AI RMF to ISO/IEC 42001 crosswalk (built against the FDIS draft). Leave blank when there is no derived reference. |
| `in_official_crosswalk` | Which of the subcategories in `ai_rmf_refs` also appear in AIUC-1's published NIST AI RMF crosswalk. Use the same semicolon-separated form. Leave blank when none of the chosen references are in that crosswalk. |
| `notes` | Optional context, in your own words |

`full` means the cited AI RMF references already address the requirement. `partial` means they address only part of it. `none` means no cited AI RMF reference applies. A row marked `full` or `partial` must include at least one AI RMF reference. Every reference in `in_official_crosswalk` must also appear in `ai_rmf_refs`.

## Run the report

Requires Python 3 and the standard library only. From the repository root:

```bash
python3 coverage_report.py
```

The script reads `data/mapping.csv` and writes `reports/coverage_report.md`. It checks that the required columns are present and that every `coverage` value is `full`, `partial`, or `none`. Invalid rows are printed and left out of the totals. It also warns when `coverage` is `full` or `partial` but `ai_rmf_refs` is empty, and it rejects an `in_official_crosswalk` entry that is not one of the chosen `ai_rmf_refs`.

The report has three parts:

- a summary table with the count and percentage of requirements at each coverage level
- a gap list of every requirement marked `none` or `partial`
- a list of AI RMF subcategories in `ai_rmf_refs` that are not listed in `in_official_crosswalk`

## ISO text

ISO/IEC 42001 is copyrighted. This project does not reproduce it. ISO/IEC 42001 references are clause identifiers derived from NIST's published AI RMF to ISO/IEC 42001 crosswalk, which was built against the FDIS draft.
