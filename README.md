# AI-Keywords for IMatch

## 📌 Projektöversikt

Detta projekt är ett lokalt, modulärt system för automatisk generering av AI-baserade keywords för bildarkiv i IMatch.

Målet är att analysera RAW- och bildfiler med hjälp av AI-modeller (Ollama, YOLO och specialiserade vision-modeller) och generera strukturerade, kontrollerbara keywords.

IMatch ska endast hantera slutresultatet – all AI-bearbetning sker utanför IMatch.

---

## 🎯 Mål

- Automatisera bildtaggning med AI
- Identifiera objekt som:
  - Fåglar
  - Växter
  - Insekter
  - Landskap och objekt
- Generera kontrollerade keywords under `Keywords|AI`
- Undvika att störa användarens manuella keyword-struktur i IMatch
- Minimera fel genom att använda konfidensbaserade beslut

---

## 🧠 Grundprinciper

- AI får aldrig skriva direkt till manuella keyword-hierarkin
- All AI-data lagras under `Keywords|AI`
- Hellre generell klassificering än felaktig artbestämning
- Svenska namn används i slutresultat, men modeller kan arbeta med latinska namn internt
- GPS och metadata används som stöd, inte som keywords

---

## 🏗️ Systemarkitektur (planerad)

1. Förbearbetning av bild
   - Skala ner till preview (ca 768–1024 px)
   - Extrahera EXIF/XMP (GPS, tid, rating)

2. Objektidentifiering
   - YOLO används för att hitta objekt i bilden
   - Bounding boxes genereras

3. Crop & detaljanalys
   - Utskurna objekt analyseras i högre upplösning

4. AI-analys
   - Ollama/VLM-modeller används för klassificering
   - Eventuella specialmodeller för:
     - Fåglar
     - Växter
     - Insekter

5. Kunskapslager
   - Översättning (latinska → svenska namn)
   - Konfidensregler
   - Filter (GPS, kategori)

6. Output
   - JSONL som mellanformat
   - XMP/ExifTool uppdatering
   - Slutligen import till IMatch

---

## 🐦 Fåglar (speciell regel)

- Familjenivå är tillräcklig vid osäkerhet
- Artnamn används endast vid hög konfidens
- Svenska namn används i slutlig output
- Felaktiga artbestämningar ska undvikas hellre än att gå för långt i detalj

Exempel:
- `AI|Bird|Anatidae|Gräsand`
- eller bara `AI|Bird|Anatidae`

---

## 🌿 Växter och natur

- Träd och växter klassificeras grovt om osäkerhet finns
- Exempel:
  - Tree
  - Flower
  - Bamboo
  - Fern

Detaljnivå används endast vid hög konfidens

---

## 📂 Planerad projektstruktur

AI-Keywords/
│
├── README.md
├── docs/
├── scripts/
├── data/
├── prompts/
├── tests/
└── output/


---

## ⚙️ Teknologi

- WSL (Linux i Windows)
- Python
- Ollama (vision-language models)
- YOLO (object detection)
- ImageMagick / ExifTool
- Git + GitHub

---

## 🔁 Designmål

Systemet ska vara:

- modulärt
- utbytbart (nya AI-modeller ska kunna bytas in utan ombyggnad)
- deterministiskt nog för batch-körning
- säkert för stora bildarkiv (20 000+ bilder)

---

## 📌 Status

Tidigt utvecklingsstadium.

Första steg:
- Git setup klar
- Projektstruktur skapad
- Första pipeline under design

