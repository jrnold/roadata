# Rates of Advance Data (ROADATA)

## Sources

The `docs/` directory holds three research papers by Robert L. Helmbold, US Army Concepts Analysis Agency (CAA), Bethesda, MD. All three are approved for public release.

  | File                                                 | DTIC accession | CAA report   | Title                                                                 | Date          | Pages |
  | ---------------------------------------------------- | -------------- | ------------ | --------------------------------------------------------------------- | ------------- | ----- |
  | [`docs/DTIC_ADA217891.pdf`](docs/DTIC_ADA217891.pdf) | ADA217891      | CAA-RP-90-03 | *A Survey of Past Work on Rates of Advance in Land Combat Operations* | February 1990 | 131   |
  | [`docs/DTIC_ADA220426.pdf`](docs/DTIC_ADA220426.pdf) | ADA220426      | CAA-RP-90-04 | *A Compilation of Data on Rates of Advance in Land Combat Operations* | February 1990 | 428   |
  | [`docs/DTIC_ADA225635.pdf`](docs/DTIC_ADA225635.pdf) | ADA225635      | CAA-RP-90-01 | *Rates of Advance in Historical Land Combat Operations*               | June 1990     | 160   |

## Data

All data come from CAA-RP-90-04 (`docs/DTIC_ADA220426.pdf`). Appendix A compiles 30 data bases
of historical advances; each has a short introduction followed by a data table. Appendix B
collects 26 anecdotal notes on rates of advance that do not lend themselves to tabulation.

  | File                                         | Contents                                                                                       |
  | -------------------------------------------- | ---------------------------------------------------------------------------------------------- |
  | [`data/datasets.json`](data/datasets.json)   | The Appendix A index (p A-1) and the introduction to each data base, one object per data base. |
  | [`data/tables/<ID>.csv`](data/tables/)       | The data table of each data base, one row per data item.                                       |
  | [`data/anecdotes.json`](data/anecdotes.json) | The Appendix B notes, one object per note.                                                     |

### `datasets.json`

A JSON array of 30 objects, in index order, with these fields:

  | Field                                                       | Source                                                                                                                                                          |
  | ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | `number`, `id`, `first_page`, `n_items`                     | The report's index (p A-1): number, short name (e.g. `ACSDB`), first page of the entry, and number of data items.                                               |
  | `n_rows`, `n_columns`                                       | Size of `tables/<id>.csv` (data rows, excluding the header); `null` where there is no table. `n_rows` differs from `n_items` for BAORG and ROWLAND (see below). |
  | `title`, `author`, `date`, `organization`, `available_from` | Paragraph 1 ("Data Source"), as printed. `null` where the source gives "NA".                                                                                    |
  | `numbers`                                                   | Paragraph 1e (report or contract numbers) as a list; empty where the source gives "NA".                                                                         |
  | `data_description`                                          | Paragraph 2, markdown.                                                                                                                                          |
  | `discussion_and_comments`                                   | Paragraph 3, markdown.                                                                                                                                          |
  | `data_table_notes`                                          | Paragraph 4, markdown; `null` where the source says "None".                                                                                                     |

The text is a faithful transcription with scanning errors corrected; the source's own errors
(e.g. ACSDB's "16 January 1944") are kept. In the markdown, lettered items (`a.`, `b.`) are
paragraphs, numbered sub-items (`(1)`, `(a)`) are nested bullets, and tables in the notes are
markdown tables.

### `tables/<ID>.csv`

Index items and table sizes (also in `datasets.json`):

  | No. | ID       | First page | Items (index) | Rows (CSV) | Columns |
  | --: | -------- | ---------- | ------------: | ---------: | ------: |
  |   1 | ACSDB    | A-5        |          3401 |       3401 |      10 |
  |   2 | ALEXANDE | A-65       |           124 |        124 |      17 |
  |   3 | ANDREWS  | A-74       |            55 |         55 |      17 |
  |   4 | BAORG    | A-80       |           330 |        331 |      19 |
  |   5 | CAESAR   | A-99       |            27 |         27 |      18 |
  |   6 | CDB90    | A-102      |           660 |        660 |      38 |
  |   7 | DESANTIS | A-155      |            84 |         84 |      17 |
  |   8 | EASTFRON | A-161      |           212 |        212 |      18 |
  |   9 | ENGELS   | A-173      |            19 |         19 |      17 |
  |  10 | GLANTZ   | A-176      |           114 |        114 |      18 |
  |  11 | GUSTAVUS | A-184      |             8 |          8 |      17 |
  |  12 | HANNIBAL | A-187      |             4 |          4 |      17 |
  |  13 | HULSE    | A-190      |            19 |         19 |      17 |
  |  14 | LONGMARX | A-194      |           371 |        371 |      18 |
  |  15 | MISCROAD | A-214      |           173 |        173 |      20 |
  |  16 | NAPOLEON | A-229      |            31 |         31 |      17 |
  |  17 | NORMANDY | A-232      |            50 |         50 |      19 |
  |  18 | ORALFORE | A-239      |           360 |        360 |      18 |
  |  19 | OVERHOLT | A-259      |             0 |          — |       — |
  |  20 | PARSONS  | A-261      |            33 |         33 |      18 |
  |  21 | QUICKWIN | A-265      |            30 |         30 |      18 |
  |  22 | RADZIEV  | A-270      |            40 |         40 |      18 |
  |  23 | RAND     | A-273      |             0 |          — |       — |
  |  24 | RECORD   | A-275      |            22 |         22 |      18 |
  |  25 | RMC      | A-278      |           250 |        250 |      28 |
  |  26 | ROWLAND  | A-295      |           288 |        317 |      17 |
  |  27 | SAVKIN   | A-313      |            81 |         81 |      18 |
  |  28 | SIEGFRIE | A-318      |            40 |         40 |      19 |
  |  29 | WAINSTEI | A-323      |           237 |        237 |      13 |
  |  30 | XENOPHON | A-337      |            38 |         38 |      17 |

OVERHOLT and RAND present their data only as graphs, so they have no table.

Format and conventions:

- UTF-8, comma-separated, LF line endings, one header row. The first column is the row
  number printed in the source (`no`, `seq` in ACSDB, `seqno` in CDB90); rows are in source order.
- Column names are the printed column headers in snake_case (`RATE (KM/DAY)` becomes
  `rate_km_day`). A header printed twice gets a suffix (`time_days`, `time_days_2`;
  `start_date_1`, `end_date_2`). CDB90 uses its data base code names (`seqno`, `wofa1`, ...,
  `atpcode`), which are defined in its `data_table_notes`. ACSDB adds a `section` column for
  the time period printed above each page (e.g. `15-19 DEC 44`).
- A wide table printed in several column groups ("PART n OF m") is joined back into one row
  per item on the row number.
- **Values are verbatim as printed.** Nothing is converted, recomputed or filled in. Codes are
  kept: `NA` (the source did not give the item), `NU` or `N/U` (the item is not used), `ERR`,
  sentinel values such as `999.90` in ACSDB and `-9` in CDB90, and `"` ditto marks. Dates keep
  their printed format (`17-Dec-44`, `AUG 1914`, decimal years such as `1664.5336` in CDB90).
  The source's misspellings are kept (e.g. CDB90 `SOUTH MOUTAIN`, BAORG `2 CAMERONINAS`). Empty
  cells are blank in the print. Curly quotes are normalized to straight ASCII quotes.
- The compiler converted all distances to kilometres and times to days, counted start and
  end dates inclusively, and recomputed rates as distance / elapsed time (report pp A-2 to A-3).
  Where a table also gives the source's original units (yards, miles, hours), the km and
  km/day columns follow from them.

Row counts that differ from the index (the index appears to be wrong in both cases):

- **BAORG** has 331 rows; the table numbers its rows 1-331 with no gaps, and the introduction
  says 331 engagements. The index says 330.
- **ROWLAND** has 317 rows, numbered 1-317 in the table. They include 26 subtotal rows
  ("Total" in the route column) and 4 text-only heading rows with no data (rows 266, 272, 292,
  305). Without those there are 287 advances; the index says 288.

### `anecdotes.json`

Appendix B, "Some Anecdotal Information on Rates of Advance" (pp B-1 to B-40), gives information
on cases not in Appendix A, or more detail on a few that are. The compiler calls it an
"opportunity sample". It is a JSON array of 26 objects, in the report's order (alphabetical by
short name), with these fields:

  | Field                                     | Source                                                                                                                                                                                                                              |
  | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | `number`                                  | Position in the appendix (1-26).                                                                                                                                                                                                    |
  | `id`                                      | The note's short name as printed, e.g. `ARNOLD'S EXPEDITION`, `FM 100-5`.                                                                                                                                                           |
  | `page`                                    | Printed page where the note starts, e.g. `B-3`.                                                                                                                                                                                     |
  | `title`, `author`, `date`, `organization` | Paragraph 1 ("Source"), as printed.                                                                                                                                                                                                 |
  | `notes`                                   | Paragraph 2, markdown: the quoted or summarized passages with their page cites, often with a rate worked out by the compiler. Some notes include tables (e.g. CUSTER's daily marches, ARTILLERY USAGE IN WORLD WAR II's Table B-1). |
  | `comments`                                | Paragraph 3, markdown; `null` where the source says "None".                                                                                                                                                                         |

The same transcription rules apply as for `datasets.json`.

## How the data were extracted

1. **Introductions and notes.** The text layer of the PDF (`pdftotext -layout`) was split into
   one block per data base (Appendix A) or note (Appendix B) and transcribed into `datasets.json`
   and `anecdotes.json`, checking unclear passages and the Appendix B tables against the page
   images.
2. **OCR.** The PDF's own text layer is usable on portrait pages but is noise on the landscape
   (rotated) table pages, so all table pages (PDF pp 21-356) were rendered at 300 dpi and
   re-OCR'd with Tesseract 5. Tesseract's orientation detection got about 40 pages wrong; each
   page's rotation was instead chosen by OCR confidence across the four orientations and checked
   against the page header.
3. **Tables.** Each table was parsed from the OCR using word positions, with column-specific
   re-OCR (crops at up to 600 dpi, multiple passes voted) for noisy columns. ACSDB was read cell
   by cell with a glyph classifier trained on its monospaced font. Every cell that failed a check
   or that the OCR passes disagreed on was read from the page image.
4. **Checks.** For every table: row count against the index, row numbers complete and in order,
   type and allowed-value checks on each column, and internal arithmetic where the table allows it
   (km = miles x 1.609344 or yards x 0.0009144, rate = km / days or km x 24 / hours, inclusive
   date spans, CDB90 strength and casualty totals, ACSDB time in combat + not in combat = 24).
5. **Review.** Two independent reviews compared a random sample of rows, cell by cell, with the
   page images (about 3,000 cells). Text columns that came from OCR were then checked in full
   against the images: CDB90 battle names, BAORG unit names, LONGMARX place names, and the
   ROWLAND and WAINSTEI operation, route and note columns.

The extraction scripts are not part of this repository.

## Known limitations

- **Damaged print.** A few cells are blotted or clipped in the scan and hold a best reading:
  - ACSDB seq 2730-2731 `distance_opposed_advance` (PDF p 69).
  - ORALFORE rows 40-42 `distance_km`, row 130 `weather_air`, row 304 `atk_miss_n` and row 330
    `def_cas_pct`.
  - NORMANDY row 13 yards.
  - CDB90 rows 16 `acha`, 127 and 131 `kmda`, 359 `wina`, and 569 and 580 `post1`.
  - RMC rows 51 and 139 `pers_attn_us`, row 52 `anti_armor_ger`, and row 157 `tank_attn_ger`.
  - BAORG row 3 `total_casualties`.
  - ROWLAND row 204 route ("Bir Lahfan").
- **Unverified numeric cells.** Numbers outside the reviewed sample rest on OCR agreement plus
  the arithmetic and allowed-value checks. A digit misread the same way by every OCR pass, in a
  column with no arithmetic check, would not be caught. That risk is highest in the large coded
  tables (CDB90, RMC).
- **Source inconsistencies are kept**, not corrected: for example, day counts that disagree with
  the printed dates (DESANTIS rows 28-30, HULSE row 17, MISCROAD rows 22, 66, 69, 78 and 159) and
  rates that differ slightly from distance / time because of rounding.
