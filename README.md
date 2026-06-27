# AI-Keywords

## 📌 Projektöversikt
Detta projekt är ett lokalt, modulärt system utvecklat för att automatisera genereringen av AI-baserade keywords och metadata för stads-, rese- och turistbilder (med särskilt fokus på resor till Kina). 

Systemet är optimerat för att hantera miljöanalys, scenförståelse och avancerad textigenkänning (OCR) på skyltar, byggnader och platser, utan att störa den manuella keyword-strukturen i IMatch.

All AI-bearbetning sker helt isolerat utanför IMatch via en robust och fel-tolerant pipeline.

—

## 🎯 Mål & Grundprinciper
- **Säker struktur:** All AI-genererad data lagras strikt under `Keywords|AI|Platser` eller `Keywords|AI|Stad` för att skydda den manuella hierarkin.
- **Flerspråkig OCR:** Systemet kan identifiera komplexa geometriska former och tecken (t.ex. kinesiska Hanzi) och spara både råtext och svensk översättning.
- **Kontextbaserad taggning:** Använder vision-modeller för att identifiera landmärken, arkitektur, kulturföremål och generella miljöer (t.ex. ”Tempel”, ”Skyskrapa”, ”Bambu”).

—

## 🏗️ Pipeline-arkitektur (JSONL-baserad)

Processen körs frikopplat i olika steg för att spara VRAM och förhindra dataförlust vid batch-körningar av tusentals bilder:

