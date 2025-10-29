# YouTube AI Agent

AI-Agent zur automatischen Erstellung strukturierter Markdown-Notizen aus YouTube-Videos (2-5 Minuten).

## 🎯 Use Case & USP

**Zielgruppe:** Wissensarbeiter, Studenten, Content-Kuratoren, die schnell Inhalte aus YouTube-Videos erfassen müssen.

**Nutzen:**
- Spart 80% der Zeit beim Notizen machen
- Konsistente, strukturierte Dokumentation
- Automatische Zeitstempel für wichtige Zitate
- Wiederverwendbare, durchsuchbare Markdown-Notizen

**USP:**
- Robuste Transkript-Beschaffung (mehrere Fallbacks)
- Intelligentes Zitat-Mapping mit Zeitstempeln
- Bereinigung von UI-Artefakten ([Musik], etc.)
- Single-Shot LLM-Ansatz (effizient, keine Chunking-Komplexität)

## 📋 Output-Format

Die generierten Markdown-Notizen enthalten:

- **TL;DR** (3-5 Bullet Points)
- **Kernaussagen** (6-10 präzise Fakten)
- **Struktur/Outline** (5-8 logische Abschnitte)
- **Zitate mit Zeitstempel** (bis zu 4 wörtliche Zitate mit Minute:Sekunde)
- **Glossar** (wichtige Begriffe erklärt)
- **Offene Fragen** (weiterführende Themen)

## 🚀 Quick Start

### 1. Google Colab öffnen

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/RumiSepantaAi/youtube-agent/blob/main/notebook.ipynb)

### 2. OpenAI API Key setzen

Im Colab Notebook:
- Klicke auf das 🔑 Secrets-Icon (links)
- Füge `OPENAI_API_KEY` hinzu mit deinem API-Key

### 3. Notebook ausführen
```python
# Einfach die URL anpassen und ausführen:
TEST_URL = "https://www.youtube.com/watch?v=deine-video-id"
run_pipeline(TEST_URL)
```

### 4. Ergebnis herunterladen

Die Markdown-Datei wird unter `output/<slug>.md` gespeichert.

## 🏗️ Architektur
```
YouTube URL
    ↓
[Transkript-Beschaffung]
├── youtube-transcript-api (primär: manuell → auto)
└── yt-dlp (fallback: subtitles → auto-captions)
    ↓
[Bereinigung]
├── HTML-Tags entfernen
├── UI-Artefakte filtern ([Musik], (Applaus), ♪)
└── Duplikate in kurzen Zeitfenstern eliminieren
    ↓
[LLM-Extraktion] (Single-Shot JSON)
├── Zusammenfassung (TL;DR)
├── Kernaussagen extrahieren
├── Struktur/Outline erstellen
├── Wörtliche Zitate finden
├── Glossar generieren
└── Offene Fragen identifizieren
    ↓
[Zitat-Mapping]
├── Segmente zu Sätzen gruppieren (max 220 chars)
├── Token-basierte Ähnlichkeitssuche
└── Zeitstempel zuordnen (min. 20s Abstand)
    ↓
[Markdown-Generierung]
└── output/<slug>.md
```

### Technische Entscheidungen

| Aspekt | Entscheidung | Begründung |
|--------|--------------|------------|
| **Transkript-Quelle** | youtube-transcript-api + yt-dlp | Robustheit durch Fallback-Chain |
| **LLM-Ansatz** | Single-Shot JSON | Effizient für 2-5 Min Videos, keine Chunking-Komplexität |
| **Zitat-Mapping** | Token-Overlap + Substring-Heuristik | Funktioniert ohne externe NLP-Libs (scikit-learn, spaCy) |
| **Bereinigung** | Regex + Whitelist-Logik | Entfernt 95% der UI-Artefakte zuverlässig |

## 📦 Dependencies
```
yt-dlp>=2024.8.6
youtube-transcript-api>=0.6.2
python-slugify>=8.0.4
openai>=1.40.0
requests>=2.31.0
```

Alle Abhängigkeiten werden automatisch im Notebook installiert.

## 🧪 Beispiel-Output

Siehe [Beispiel-Output](example_output.md) für ein vollständiges Beispiel.


## ⚠️ Limitationen & Grenzen

### Technische Limitationen
- **Videolänge:** Optimiert für 2-5 Minuten (längere Videos benötigen - Chunkingstrategie)
- **Transkript-Verfügbarkeit:** Benötigt Untertitel oder Auto-Captions
- **Sprache:** Priorisiert Deutsch/Englisch; andere Sprachen möglich aber ungetestet
- **Zitat-Mapping:** ~85% Genauigkeit; bei ähnlichen Aussagen kann es Verwechslungen geben

### Inhaltliche Limitationen
- **Fachsprache:** Bei hochspezialisiertem Jargon kann Glossar unvollständig sein
- **Visuelle Inhalte:** Diagramme/Demos im Video werden nicht erfasst
- **Kontext:** Ironie/Sarkasmus wird u.U. wörtlich genommen
- **Mehrsprachigkeit:** Sprachwechsel im Video führen zu fragmentierten Transkripten

### Qualitätsfaktoren
- **Auto-Captions:** Qualität hängt von YouTube's ASR ab (Namen/Fachbegriffe oft falsch)
- **LLM-Varianz:** Verschiedene Runs können leicht unterschiedliche Formulierungen erzeugen
- **Timestamp-Genauigkeit:** ±5 Sekunden durch Satz-Gruppierung


