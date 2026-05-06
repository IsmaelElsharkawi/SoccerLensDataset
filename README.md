# SoccerLens Dataset

> **Note:** SoccerLens is currently under review.

SoccerLens is a soccer broadcast video dataset providing per-second bounding box annotations for on-screen graphical overlays alongside natural language commentary. It is designed to support research in object detection, explainable AI, and vision-language models applied to sports broadcast video. The dataset contains 2,209 annotated frames drawn from 200 soccer match clips, with 4,687 bounding box annotations across three categories.

---

## Overview

| Property | Value |
|---|---|
| Video clips | 200 |
| Annotated frames | 2,209 |
| Bounding box annotations | 4,687 |
| Annotation categories | 3 (Primary Cue, Secondary Cue, Common Cue) |
| Frame resolution | 1280 × 720 px |
| Annotation format | MS-COCO (object detection) |
| Seasons covered | 2014–2019 |
| License | [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) |

---

## Dataset Description

Each sample in SoccerLens consists of:
- **Video clip** — a short soccer broadcast clip sourced from [SoccerNet](https://www.soccer-net.org/).
- **Annotated frames** — keyframes extracted at one-second intervals, each labeled with axis-aligned bounding boxes for visible on-screen overlays.
- **Commentary text** — the original broadcast commentary sentence associated with the clip.
- **Anonymized commentary** — a version of the commentary where player names are replaced with `[PLAYER]` and team names with `[TEAM]`.

### Annotation Categories

| ID | Category | Description |
|---|---|---|
| 1 | `Primary Cue` | Small text overlays (e.g., score bugs, time displays) |
| 2 | `Secondary Cue` | Large text overlays (e.g., player name banners, match stats) |
| 3 | `Common Cue` | Graphical/visual indicator elements on screen |

### Event Types

Clips are labeled with one of 13 action caption types:

`corner` · `foul lead to penalty` · `foul with no card` · `free kick` · `goal` · `injury` · `lead to corner` · `penalty` · `red card` · `second yellow card` · `substitution` · `throw in` · `yellow card`

---

## Leagues & Seasons

| League | Seasons |
|---|---|
| England — Premier League | 2015–2016, 2016–2017 |
| Germany — Bundesliga | 2015–2016, 2016–2017 |
| Italy — Serie A | 2015–2016, 2016–2017 |
| Spain — La Liga | 2014–2015, 2015–2016, 2016–2017 |
| Europe — UEFA Champions League | 2014–2015, 2015–2016, 2016–2017 |

---

## Repository Structure

```
SoccerLensDataset/
├── annotations-coco.json               # COCO-format bounding box annotations (2,209 frames, 4,687 boxes)
├── selected_videos_for_annotations.json  # Metadata for the 200 annotated video clips
├── croissant_metadata.json             # ML Croissant dataset card (schema.org / mlcommons.org)
├── LICENSE                             # Dataset license
└── README.md
```

### `annotations-coco.json`

Follows the [MS-COCO object detection format](https://cocodataset.org/#format-data). Top-level keys:

| Key | Description |
|---|---|
| `info` | Dataset version and description |
| `images` | Frame metadata — `id`, `file_name`, `video_id`, `second`, `width`, `height` |
| `annotations` | Bounding boxes — `id`, `image_id`, `category_id`, `bbox` (`[x, y, w, h]`), `iscrowd` |
| `categories` | Category definitions — `id`, `name` |

Frame `id` format: `<league>/<match>/<clip>.mp4_<second>` (e.g., `germany_bundesliga_2016-2017/2016-10-01 - 19-30 Bayer Leverkusen 2 - 0 Dortmund/2_45_06.mp4_7`).

### `selected_videos_for_annotations.json`

A JSON array with one entry per clip. Each entry contains:

| Field | Description |
|---|---|
| `video` | Relative path to the source video clip |
| `caption` | Action/event label for the clip |
| `comments_text` | Original broadcast commentary sentence |
| `comments_text_anonymized` | Commentary with `[PLAYER]` and `[TEAM]` substitutions |
| `league` | League identifier string |
| `match` | Match identifier string |

---

## Intended Use Cases

SoccerLens is a benchmark for **grounded soccer video understanding**, designed to evaluate whether vision-language model (VLM) predictions are grounded in meaningful visual evidence rather than shortcut learning or spurious correlations.

---

## Limitations & Biases

- Clips are sampled from SoccerNet and may over-represent **top-tier European leagues**.
- Coverage is limited to a **single data provider** (SoccerNet) spanning seasons 2014–2019; broadcast styles may not generalize to other feeds or sports.
- The dataset does **not include audio** or temporal context beyond isolated one-second frames.
- Commentary text reflects broadcast commentator perspectives; anonymization replaces only player and team name entities and may miss other identifying references.

---

## Privacy

Original commentary sentences contain real player and team names from public broadcast sources. An anonymized version (`comments_text_anonymized`) is provided. No biometric data, faces, or individual location data are included.

---

## License

This dataset is released under the [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/) license. It is intended for **non-commercial research use only**.

---

## Citation

If you use SoccerLens in your research, please cite the associated paper (citation to be added upon publication).

---

## Acknowledgements

Video clips and commentary text are derived from the [SoccerNet](https://www.soccer-net.org/) dataset. Bounding box annotations were created by human annotators. Anonymization was performed with a named-entity replacement script.

