## Main household language in North Nigeria

Four thematic maps of household language use in northern Nigeria, from open REACH/ClearGlobal survey data. Python + QGIS.

## Main household language in northern Nigeria

Four thematic maps of language use across 131 Local Government Areas (LGAs) in six
northern Nigerian states, built from open humanitarian survey data.

Data preparation and quality checks in Python; cartography in QGIS.


## What the data measures

The underlying survey question is:

> *What is the main language your household uses at home?*

It is a **single-response** question, the unit is the **household**, and it refers
to the **main** language at home. So the mapped values are the share of households
reporting a given language as their main one — **not** the share of speakers.

The distinction matters: Hausa is widely used as a lingua franca across northern Nigeria by people who speak something else at home, so actual speakers are considerably more numerous than these maps suggest.

---

## The maps

### 1. Survey coverage

![Survey coverage](Images/LGA_with_data.png)

Where the data exists. The dataset covers 131 of the 774 LGAs, in six states.
Five LGAs in northern Borno are missing because the survey could not reach them.

### 2. Prevalent language by LGA

![Prevalent language](Images/Most_reported_language.png)

The most frequently reported main household language in each LGA. Eleven distinct
languages; Hausa prevails in 91 of the 131 LGAs.

### 3. Spread of Hausa

![Hausa](Images/Hausa.png)

Hausa appears in 130 of 131 LGAs, but is the prevailing language in only 91. The
single LGA without it — Kala/Balge, on the Cameroon border — is a genuine absence,
not a data gap: it is a Kanuri and Shuwa Arabic area.

Class breaks are user-defined. The distribution is heavily skewed — median 0.88,
third quartile 0.99 — so the top of the range is split more finely (0.75–0.95 and
0.95–1) to separate LGAs where Hausa is dominant from those where it is close to
universal. The breaks are deliberately kept round and interpretable so that maps
of different languages remain comparable.

### 4. Language composition of the north-eastern states

![North-east composition](Images/North-East_Languages_Distribution.png)

Pie charts for Adamawa, Borno and Yobe. Only the north-east is shown — see below
for why.

---

## The methodological catch

The dataset merges **two separate REACH Multi-Sector Needs Assessments**:
north-east (2021) and north-west (2022). They ask the same question but offered
very different answer options.

| | North-east 2021 | North-west 2022 |
|---|---|---|
| Households surveyed | 8,745 | 11,090 |
| Answer options in the questionnaire | 28 languages | 6 (English, Hausa, Fulfulde, Yoruba, Igbo, Other) |
| Distinct languages in the final data | 85 | 12 |

The north-west surveyed **more** households and captured **seven times fewer**
languages. This is not a sampling effect — it is the instrument. A household
speaking a minority language in Katsina or Zamfara had no way to report it, and
either chose *Other* or gave Hausa as an approximation.

So the striking visual contrast between a compact, monolingual-looking north-west
and a mosaic north-east reflects questionnaire design as much as linguistic
reality. **Comparisons between the two regions should be avoided; comparisons
within each region remain valid.**

This is also why map 4 covers only the north-east: pie charts for Katsina, Sokoto
and Zamfara would all be 95–98% Hausa, three nearly identical circles.

---

## Aggregating from LGA to state

Map 4 aggregates LGA-level proportions to state level. The denominator decides
whether the result is meaningful:

| Method | Denominator | Result |
|---|---|---|
| Wrong | only LGAs where the language appears | slices do not add up |
| Correct | all surveyed LGAs in the state | sums to exactly 100% |

The first method inflates every language in proportion to how localised it is: a
language spoken in 2 of 22 LGAs with a share of 0.8 would appear as 80% of the
state instead of 7.3%. An earlier version of this map used it, producing slices
summing to 102.5% for Zamfara and 206.3% for Borno.

Note that state averages are **unweighted by population**: every LGA counts
equally, so Maiduguri carries the same weight as a small rural LGA. This is the
only aggregation possible without population data, but it means state percentages
should not be read as population shares.

---

## Data sources

- **Language data** — ClearGlobal, *Language use in Nigeria (admin 2)*, via the
  Humanitarian Data Exchange
  <https://data.humdata.org/dataset/nigeria-languages>
- **Administrative boundaries** — OCHA, *Nigeria administrative level 0–3
  boundaries (COD-AB)*
  <https://data.humdata.org/dataset/cod-ab-nga>
- **Source surveys** — REACH / IMPACT Initiatives Multi-Sector Needs Assessments,
  north-east Nigeria (Aug–Oct 2021) and north-west Nigeria (Mar–Jul 2022)

---

## Repository contents

```
Nigerian_Languages_Notebook.ipynb         notebook: data prep, checks, exports
clearglobal_language_use_nga_admin2.csv   source dataset
output/                                   CSVs generated for the QGIS joins
Images/                                   map exports from QGIS
```

Boundary shapefiles are not included — download them from the COD-AB link above
and place `nga_admin1.*` and `nga_admin2.*` alongside the notebook.

## Reproducing

```bash
pip install pandas
jupyter lab Nigerian_Languages_Notebook.ipynb
```

Run all cells. All paths are relative to the notebook folder; the CSVs land in
`output/` and are joined to the shapefiles in QGIS on `adm2_pcode` (LGA level) or
`adm1_pcode` (state level). Each map section documents its QGIS procedure.

---

## Limitations

1. Coverage is **humanitarian, not geographic**: 131 of 774 LGAs, six of 36
   states, selected because a crisis response was active. Kano — the most
   populous northern state and the historic centre of Hausa — is absent, as is
   Kaduna.
2. Five Borno LGAs were **inaccessible** to the survey, not empty.
3. State-level figures are **unweighted by population**.
4. Language categories have **uneven granularity**: some entries are single
   languages, others are groupings of varieties.
5. The two survey rounds are nine months apart and fall in different seasons (Aug–Oct 2021 and Mar–Jul 2022).

These maps are a valid record of what these two surveys measured. They are not a
linguistic map of northern Nigeria.

---

## Licence

Source data is published under the terms given on its HDX pages. Code in this
repository is free to reuse; please cite the original data sources.

