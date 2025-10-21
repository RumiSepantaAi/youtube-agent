# youtube-agent
AI-Agent zur automatischen Erstellung strukturierter Markdown-Notizen aus YouTube-Videos (2-5 Minuten).
🎯 Use Case & USP
Zielgruppe: Wissensarbeiter, Studenten, Content-Kuratoren, die schnell Inhalte aus YouTube-Videos erfassen müssen.
Nutzen:

Spart 80% der Zeit beim Notizen machen
Konsistente, strukturierte Dokumentation
Automatische Zeitstempel für wichtige Zitate
Wiederverwendbare, durchsuchbare Markdown-Notizen

USP:

Robuste Transkript-Beschaffung (mehrere Fallbacks)
Intelligentes Zitat-Mapping mit Zeitstempeln
Bereinigung von UI-Artefakten ([Musik], etc.)
Single-Shot LLM-Ansatz (effizient, keine Chunking-Komplexität)

📋 Output-Format
Die generierten Markdown-Notizen enthalten:

TL;DR (3-5 Bullet Points)
Kernaussagen (6-10 präzise Fakten)
Struktur/Outline (5-8 logische Abschnitte)
Zitate mit Zeitstempel (bis zu 4 wörtliche Zitate mit Minute:Sekunde)
Glossar (wichtige Begriffe erklärt)
Offene Fragen (weiterführende Themen)

🚀 Quick Start
1. Google Colab öffnen
Bild anzeigen

Hinweis: Ersetze DEIN-USERNAME mit deinem GitHub-Benutzernamen im Link oben.

2. OpenAI API Key setzen
Im Colab Notebook:

Klicke auf das 🔑 Secrets-Icon (links)
Füge OPENAI_API_KEY hinzu mit deinem API-Key

3. Notebook ausführen
python# Einfach die URL anpassen und ausführen:
TEST_URL = "https://www.youtube.com/watch?v=deine-video-id"
run_pipeline(TEST_URL)
4. Ergebnis herunterladen
Die Markdown-Datei wird unter output/<slug>.md gespeichert.
🏗️ Architektur
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
