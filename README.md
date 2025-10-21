# youtube-agent
AI-Agent zur automatischen Erstellung strukturierter Markdown-Notizen aus YouTube-Videos (2-5 Minuten).

1.Output-Format
Die generierten Markdown-Notizen enthalten:

TL;DR (3-5 Bullet Points)
Kernaussagen (6-10 präzise Fakten)
Struktur/Outline (5-8 logische Abschnitte)
Zitate mit Zeitstempel (bis zu 4 wörtliche Zitate mit Minute:Sekunde)
Glossar (wichtige Begriffe erklärt)
Offene Fragen (weiterführende Themen)

2. Im Colab Notebook:

Klicke auf das 🔑 Secrets-Icon (links)
Füge OPENAI_API_KEY hinzu mit deinem API-Key

3. Notebook ausführen
python# Einfach die URL anpassen und ausführen:
TEST_URL = "https://www.youtube.com/watch?v=deine-video-id"
run_pipeline(TEST_URL)
4. Ergebnis herunterladen
Die Markdown-Datei wird unter output/<slug>.md gespeichert.
