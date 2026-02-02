# YouTube AI Agent

AI agent for automatically generating structured Markdown notes from YouTube videos (2–5 minutes).

## 🎯 Use Case & USP

**Target audience:** Knowledge workers, students, content curators who need to quickly extract information from YouTube videos.

**Benefits:**
- Saves ~80% of the time spent taking notes
- Consistent, structured documentation
- Automatic timestamps for important quotes
- Reusable, searchable Markdown notes

**USP:**
- Robust transcript acquisition (multiple fallbacks)
- Intelligent quote-to-timestamp mapping
- Cleanup of UI artifacts ([Music], etc.)
- Single-shot LLM approach (efficient, no chunking complexity)

## 📋 Output Format

The generated Markdown notes include:

- **TL;DR** (3–5 bullet points)
- **Key Takeaways** (6–10 precise facts)
- **Structure / Outline** (5–8 logical sections)
- **Quotes with Timestamps** (up to 4 verbatim quotes with minute:second)
- **Glossary** (explanations of key terms)
- **Open Questions** (follow-up topics)

## 🚀 Quick Start

### 1. Google Colab öffnen

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/RumiSepantaAi/youtube-agent/blob/main/notebook.ipynb)

### 2. Set OpenAI API Key

In the Colab notebook:
- Click the 🔑 Secrets icon (left side)
- Add `OPENAI_API_KEY` with your API key

### 3. Run the Notebook
```python
# Just adapt the URL and run:
TEST_URL = "https://www.youtube.com/watch?v=your-video-id"
run_pipeline(TEST_URL)

### 4. Download the result

The Markdown file is saved under `output/<slug>.md`.

## 🏗️ Architecture

YouTube URL
    ↓
[Transcript Acquisition]
├── youtube-transcript-api (primary: manual → auto)
└── yt-dlp (fallback: subtitles → auto-captions)
    ↓
[Cleanup]
├── Remove HTML tags
├── Filter UI artifacts ([Music], (Applause), ♪)
└── Eliminate duplicates in short time windows
    ↓
[LLM Extraction] (Single-Shot JSON)
├── Summary (TL;DR)
├── Extract key takeaways
├── Generate structure/outline
├── Identify verbatim quotes
├── Generate glossary
└── Identify open questions
    ↓
[Quote Mapping]
├── Group segments into sentences (max 220 chars)
├── Token-based similarity search
└── Assign timestamps (min. 20s spacing)
    ↓
[Markdown Generation]
└── output/<slug>.md


### Technical Decisions

| Aspect                | Decision                             | Rationale                                             |
| --------------------- | ------------------------------------ | ----------------------------------------------------- |
| **Transcript source** | youtube-transcript-api + yt-dlp      | Robustness via fallback chain                         |
| **LLM approach**      | Single-shot JSON                     | Efficient for 2–5 min videos, no chunking complexity  |
| **Quote mapping**     | Token overlap + substring heuristics | Works without external NLP libs (scikit-learn, spaCy) |
| **Cleanup**           | Regex + whitelist logic              | Reliably removes ~95% of UI artifacts                 |


## 📦 Dependencies

yt-dlp>=2024.8.6
youtube-transcript-api>=0.6.2
python-slugify>=8.0.4
openai>=1.40.0
requests>=2.31.0


All dependencies are installed automatically in the notebook.

## 🧪 Example Output

See [example output](example_output.md) for a complete sample.

## ⚠️ Limitations & Constraints

### Technical Limitations
- **Video length:** Optimized for 2–5 minutes (longer videos require a chunking strategy)
- **Transcript availability:** Requires subtitles or auto-captions
- **Language:** Optimized for German/English; other languages may work but are untested
- **Quote mapping:** ~85% accuracy; similar statements may be confused

### Content Limitations
- **Technical jargon:** Highly specialized terminology may lead to incomplete glossaries
- **Visual content:** Diagrams/demos in videos are not captured
- **Context:** Irony/sarcasm may be interpreted literally
- **Multilingual videos:** Language switching can cause fragmented transcripts

### Quality Factors
- **Auto-captions:** Quality depends on YouTube’s ASR (names/technical terms often incorrect)
- **LLM variance:** Different runs may produce slightly different phrasing
- **Timestamp accuracy:** ±5 seconds due to sentence grouping


