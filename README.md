# Gazetteer of Japan (地名集日本)

Japanese place name dictionary, in CSV and JSON formats.

**Interactive visualization: [Gazetteer of Japan (地名集日本) / Sorami Hisamoto | Observable](https://observablehq.com/@sorami/gazetteer-of-japan)**

Originally compiled by Geospatial Information Authority of Japan (GSI): [地名集日本（GAZETTEER OF JAPAN) | 国土地理院](https://www.gsi.go.jp/kihonjohochousa/gazetteer.html) (PDF, retrieved 2022-12-22).

This repository is not affiliated with GSI.

## License

When you use these data, please cite the source (GSI), and explicitly state that the content has been edited.

Example:

```
Data created by editing "Gazetteer of Japan" by Geospatial Information Authority of Japan.
Source: https://www.gsi.go.jp/kihonjohochousa/gazetteer.html
```

See [GSI website's Term of Use](https://www.gsi.go.jp/ENGLISH/page_e30286.html) for more details.

You do not need to cite this repository (though I would appreciate it if you do so). I would be happy to hear from you if you create some cool stuff with this data 🥳

## Data

### CSV: `gazetteer-of-japan.csv`

```csv
kanji,kana,roman,lat,lng,class
網走川,あばしりがわ,Abashiri Gawa,44.017,144.283,River
網走湖,あばしりこ,Abashiri Ko,43.967,144.183,Lake
網走市,あばしりし,Abashiri Shi,44.017,144.267,Municipality
安倍川,あべかわ,Abe Kawa,34.933,138.400,River
我孫子市,あびこし,Abiko Shi,35.867,140.033,Municipality
安平町,あびらちょう,Abira Cho,42.767,141.817,Municipality
安平川,あびらがわ,Abira Gawa,42.617,141.733,River
安房峠,あぼうとうげ,Abo Toge,36.200,137.583,Pass
阿武町,あぶちょう,Abu Cho,34.500,131.467,Municipality
...
```

### JSON: `gazetteer-of-japan.json`

```json
[
  {
    "kanji":"網走川",
    "kana":"あばしりがわ",
    "roman":"Abashiri Gawa",
    "lat":44.017,
    "lng":144.283,
    "class":"River"
  },
  ...
]
```

### Columns

- `kanji`: The official name
- `kana`: Name in [kana](https://en.wikipedia.org/wiki/Kana) format
- `roman`: Name in [romanized](https://en.wikipedia.org/wiki/Romanization_of_Japanese) format
- `lat`: Latitude (decimal degrees, 3 decimal places)
- `lng`: Longitude (decimal degrees, 3 decimal places)
- `class`: Classification of the place
  - `Municipality`: prefecture, city, town, village
  - `Populated area`: Populated area
  - `Mountain`: mountain, hill
  - `Pass`: pass (mountain pass)
  - `Cape`: cape, beach
  - `River`: river, stream, irrigation channel
  - `Lake`: lake, marsh, swamp, pond
  - `Sea Area`: sea, bay, strait, channel
  - `Undersea feature`: ridge, seamount, seamounts, plateau, trench, trough, basin, canyon, bank, terrace, gap, seachannel
  - `Island`: island, islet, rock
  - `Extensive nature feature`: mountains, plain, peninsula, upland, islands, islets

Be aware that there are different places with the same name. For example, there are 7 rows with the name `駒ヶ岳 (Komagatake)`. See `stats.ipynb` for the list of duplicate names.

### Stats

- Number of rows: 4,149
  - 4,123 rows in original PDF
  - plus 26 aliases
- Row counts per classification
  - Municipality: 1,794
  - Mountain: 593
  - Undersea feature: 439
  - River: 326
  - Island: 312
  - Cape: 182
  - Populated area: 182
  - Extensive natural feature: 115
  - Sea Area: 105
  - Lake: 51
  - Pass: 50

## Code

See `extract.ipynb` for the details of preprocess steps.

- Latitude and longitude in the source are represented in "degrees" and "minutes" (no "seconds")
  - => I have converted them to decimal degrees (rounded to 3 decimal places)
  - e.g., `44°01'` to `44.017`
- kanji as images in the original PDF
  - For some rows, kanji is represented by image instead of string, as those characters are not available on computers
  - => I have replaced them by equivalent common characters
- Aliases
  - For some rows, aliases are written together in brackets
  - e.g., `烏帽子岳（乳頭山）`, `Eboshi Dake (Nyuto Zan)`
  - => I haved splitted the string to create multiple rows
