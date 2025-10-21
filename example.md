# KI Agenten für Beginner: Alle Grundlagen in 9 Min Einfach Erklärt

- Quelle: https://www.youtube.com/watch?v=yN2iYWbwFFs

## TL;DR (3–5 Bullet Points)
- Drei-Level-Erklärung: LM → KI-Workflows → KI-Agenten.
- LMs generieren Text, sind aber tool-los, nicht reproduzierbar und passiv.
- Workflows verbinden LMs mit Tools über feste Steuerlogik für vorhersagbare Ergebnisse.
- KI-Agenten übernehmen Planung und Toolnutzung selbstständig und iterieren als Blackbox.
- Praxisbeispiele: Recherche-Workflow (Sheets→Perplexity→Docs→Gemini) und Claud Code baut Wetter-App.

## Kernaussagen
- Large Language Models wie GPT, Clode oder Gemini generieren auf Basis eines Prompts Texte und beantworten Fragen.
- LMs haben drei grundlegende Probleme: kein Zugriff auf Tools, nicht reproduzierbare Ergebnisse und sie sind passiv.
- KI-Workflows kombinieren LMs mit Tools (z.B. Kalender, Outlook, Notion) und folgen einer vorher definierten Steuerlogik; ohne passendes Modul scheitern zusätzliche Aufgaben (z.B. Wetter).
- Vom LM zum Workflow: von chaotischem Output zu vorhersagbarem Output – gute Workflows sind in der Praxis schwer und erfordern extrem gutes Prompt Engineering.
- Praxis-Workflow: Artikel in Google Sheets → an Perplexity zur Zusammenfassung → Speicherung in Google Docs → an Gemini für Blogpost; Qualität erfordert manuelle Prompt-Anpassung.
- Vom Workflow zum KI-Agenten: Der Mensch wird durch ein LM beim Planen und beim Benutzen/Verbinden von Tools ersetzt; der Agent erstellt intern den besten Workflow – Blackbox statt voller Kontrolle.
- Zentrale Technik: Iteration; ein Kritiker LM kann den Output prüfen, wodurch ein zwei Agentensystem (Kritiker LM + Antwort LLM) entsteht.
- Beispiel Claud Code: plant (To-Do-Liste), sucht im Hintergrund, iteriert über Code und liefert eine Wetter-App für Potzam Brandenburg – Ergebnis in 2 Minuten für 10 Cent.

## Struktur / Outline
1. Einführung, Zielgruppe und Dreistufen-Ansatz
2. Level 1: LMs – Funktionsweise, Prompt→Output, Grenzen
3. Level 2: KI-Workflows – Tools, Steuerlogik, Modul-Beispiel (Wetter)
4. Praxis-Workflow: Recherche (Sheets→Perplexity→Docs→Gemini) und Prompt-Iteration
5. Vom Workflow zum KI-Agenten: Ersetzen von Planung/Toolnutzung, Blackbox, Iteration, Kritiker LM, zwei Agentensystem
6. Praxis-Agent: Claud Code Wetter-App, Abschluss und Zusammenfassung

## Zitate mit Zeitstempel
- **[00:00]** KI-Agenten sind die Zukunft von künstlicher Intelligenz. Aber was bedeutet das für dich konkret? Ich habe mich die letzten Jahre intensiv mit LMS auseinandergesetzt und bereits auch schon dazu unterrichtet. Wenn du jetzt
- **[02:55]** auch als Steuerlogik bezeichnet. Ein KI Workflow folgt also immer der vorher definierten Steuerlogik. Alles klar?
- **[06:30]** Punkt in diesem ganzen Video. Um aus einem KI Workflow einen KI Agenten zu machen, muss ich durch ein LM ersetzt werden. Das heißt sowohl das Planen als auch das Tools benutzen wird jetzt der Agent erledigen. Das heißt, anstatt

## Glossar
- **Large Language Model (LM)**: ein einfaches Sprachmodell, das für einen Input eine Ausgabe generiert.
- **Prompt**: Du als Mensch gibst dem LM Eingabe, nämlich den Prompt und das LM gibt dir dann auf Basis vom Prompt eine Ausgabe.
- **KI Workflow**: Mit diesen Workflows kannst du jetzt nämlich dein LM Tools wie z.B. deinen Kalender, Outlook oder Notion kombinieren.
- **Steuerlogik**: Ein KI Workflow folgt also immer der vorher definierten Steuerlogik.
- **KI Agent**: Das heißt sowohl das Planen als auch das Tools benutzen wird jetzt der Agent erledigen.
- **Iteration**: Das heißt, wenn der KI Agent feststellt, dass der Output nicht zufriedenstellend war, kann es zurückgehen und die Aufgabe noch mal komplett neu angehen.
- **Kritiker LM**: Ein KI Agent könnte jetzt mich durch ein Kritiker LM ersetzen, das dann für mich überprüft, ob der Output zufriedenstellend ist.
- **zwei Agentensystem**: Und in diesem Fall, wo es ein Kritiker LM und ein Antwort LLM gibt, die gegenseitig interagieren, spricht man auch von einem sogenannten zwei Agentensystem.
- **Blackbox**: Das heißt, aus diesem kontrollierten Workflow, wo du alles überwachen konntest, wird jetzt eine Blackbox.

## Offene Fragen
- Aber was bedeutet das für dich konkret?
- wie könnte ich dieses Problem am besten angehen?
- Speichere ich die Artikel als Links oder als PDF?
- Welches LM nehme ich am besten, um die Texte zusammenzufassen?
- Soll ich zurückgehen und den Prompt ändern oder sollte ich versuchen, ein anderes LM zu nehmen?
