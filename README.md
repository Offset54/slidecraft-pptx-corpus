# SlideCraft `.pptx` round-trip corpus

Fourteen real-world PowerPoint decks, openly licensed, for SlideCraft's `.pptx` round-trip test
(`crates/engine/tests/it/pptx_roundtrip.rs` in Offset54/deckcraft, test
`an_external_corpus_survives_a_pptx_round_trip`). The test opens every deck, saves it as
`.pptx`, opens it again, and reports what was lost.

## Licences

The decks are third-party works. **Each keeps its own licence**, which is CC-BY-4.0 for all fourteen.
Authors, titles, sources and licence links are in [`ATTRIBUTION.md`](ATTRIBUTION.md), and the
licence text is in [`LICENSES/`](LICENSES). The files are unmodified, byte for byte as published
on Zenodo, and [`manifest.json`](manifest.json) records their SHA-256 values. Nothing here was
authored or published by Microsoft, Adobe, Avid or Autodesk.

## Running the test

```bash
git clone https://github.com/Offset54/slidecraft-pptx-corpus
# in a deckcraft checkout:
DECKCRAFT_PPTX_CORPUS=<corpus checkout>/decks cargo test -p deckcraft-engine --test it external_corpus -- --nocapture
```

On Windows:

```powershell
$env:DECKCRAFT_PPTX_CORPUS = "<path>\slidecraft-pptx-corpus\decks"
cargo test -p deckcraft-engine --test it external_corpus -- --nocapture
```

The decks, in `decks/`:

| File | Authoring app | Slides |
|---|---|---|
| `01-premis-tutorial-137-slides.pptx` | PowerPoint 16.0 | 137 (4:3) |
| `02-morph-smartart-nl.pptx` | PowerPoint 16.0 | 14 |
| `03-japanese-chart-4x3-ppt2010.pptx` | PowerPoint 2010 | 40 (4:3) |
| `04-arabic-morph-motion-paths.pptx` | PowerPoint 2013 | 19 |
| `05-video-smartart.pptx` | PowerPoint 16.0 | 22 |
| `06-sections-masters-epfl.pptx` | PowerPoint 16.0 | 62 |
| `07-wps-chinese-equations.pptx` | WPS Office | 22 |
| `08-google-slides-arabic.pptx` | Google Slides (inferred) | 45 |
| `09-keynote-workshop.pptx` | Apple Keynote (inferred) | 10 |
| `10-libreoffice-workshop.pptx` | LibreOffice 25.2 | 24 |
| `11-mac-audio-narration.pptx` | PowerPoint for Mac 16 | 9 |
| `12-ppt-equations-tables.pptx` | PowerPoint 16.0 | 44 |
| `13-mac-charts-notes.pptx` | PowerPoint for Mac 16 | 49 |
| `14-ppt2007-charts.pptx` | PowerPoint 2007 | 24 |

Decks 11–14 were added on 2026-11-24 to fill coverage gaps: embedded audio (11), native
PowerPoint equations in quantity (12), PowerPoint for Mac (11, 13), PowerPoint 2007 (14) and more
native charts (13, 14). The feature table below covers decks 1–10; the counts for 11–14 are in
`manifest.json`.

## Feature coverage

✓ = present in the package; the number is the count where useful.

| Feature | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| Custom masters/layouts, non-default theme | ✓ 2/22 | ✓ 2/77 | | | ✓ | ✓ 14/34 | ✓ 2/12 | ✓ | ✓ | ✓ 3/4 |
| Native charts | | | ✓ 1 | | | | | | | |
| Tables | ✓ | | ✓ 21 | | ✓ | ✓ 15 | ✓ 11 | ✓ 6 | | |
| SmartArt | | ✓ 8 | | | ✓ 2 | | | | | |
| Grouped shapes | ✓ 198 | ✓ | | | | ✓ 56 | | ✓ | | ✓ 14 |
| Cropped pictures | ✓ 79 | ✓ | | ✓ | | ✓ 73 | | ✓ | | |
| Entrance effects | ✓ 605 | ✓ 40 | ✓ 3 | ✓ 179 | ✓ 13 | ✓ 84 | | ✓ 15 | ✓ 11 | ✓ 144 |
| Emphasis effects | ✓ 77 | | | ✓ 52 | | | | | | |
| Exit effects | ✓ 118 | | | | | ✓ 4 | | | | |
| Motion paths | ✓ 7 | | | ✓ 341 | | ✓ 24 | | | ✓ 1 | |
| Transitions (with an effect) | ✓ fade | ✓ morph | | ✓ morph | | | | | | |
| **Morph** | | ✓ 7 | | ✓ 16 | | | | | | |
| Embedded video | | | | | ✓ MP4 | | | | | |
| Embedded audio | | | | | | | | | | |
| Speaker notes (non-empty) | ✓ 22 | | ✓ 37 | | | ✓ 28 | ✓ 7 | ✓ 44 | | |
| Sections | | | | | | ✓ 7 | | | | |
| Hyperlinks | ✓ | ✓ | | | ✓ | ✓ 173 | | ✓ 56 | ✓ | ✓ |
| Equations (`a14:m`) | | | | | | ✓ 1 | ✓ 56 | | | |
| Embedded fonts | ✓ 6 | | | | | | | ✓ 5 | | |
| CJK text | | | ✓ ja | | | | ✓ zh | | | |
| Right-to-left text | | | | ✓ ar | | | | ✓ ar | | |
| 4:3 | ✓ | | ✓ | | | | | | | |
| 16:9 | | ✓ | | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 100+ slides | ✓ 137 | | | | | | | | | |

### Not covered

- **Hebrew in the corpus.** Right-to-left text is covered by two Arabic decks. One Hebrew deck was
  found (Zenodo 19181796) but left out: it has 8 slides and no other feature the corpus lacks.

Gaps filled on 2026-11-24 by decks 11–14: embedded audio, native PowerPoint equations in
quantity, more than one native chart, PowerPoint for Mac and PowerPoint 2007.
