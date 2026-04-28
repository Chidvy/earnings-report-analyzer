markdown# Earnings Report Analyzer

An LLM-driven financial document intelligence system that automates earnings report analysis — extracting structured metrics, generating analyst-grade narratives, and enabling interactive document exploration via multi-turn Q&A.

---

## Problem → Solution → Impact

**Problem:** Financial analysts spend 45–60 minutes reviewing earnings reports to extract key metrics, summarize results, and identify risks. The document is long, data is scattered, and follow-up questions require re-reading.

**Solution:** Automated extraction pipeline that reads the report once, returns structured metrics (JSON), generates analyst-style narrative, and enables multi-turn Q&A.

**Impact:** Reduces first-pass review time to under 5 minutes. Metrics are immediately usable in dashboards or further analysis.

---

## Demo
$ python earnings_analyzer.py apple_q4_2024.pdf
============================================================
EARNINGS REPORT ANALYZER
Loading PDF: apple_q4_2024.pdf
Extracted 42,891 characters from 18 pages.
[1/2] Extracting structured metrics...
[2/2] Writing analyst narrative summary...
============================================================
STRUCTURED EXTRACTION
Company: Apple Inc.
Period: Q4 FY2024
Revenue: $119.6B (+2% YoY)
EPS: $2.18 (+16% YoY)
Services Revenue: $23.1B (+11% YoY)
Gross Margin: 45.9% (+300 bps)
Key Themes: Services growth | AI integration | Emerging markets
Risks: China competition | FX headwinds
Management Tone: Positive
============================================================
ANALYST SUMMARY
Apple reported strong Q1 fiscal 2024 results with revenue of $119.6B,
up 2% year-over-year, and EPS of $2.18, up 16% versus prior year.
Services reached an all-time high of $23.1B, up 11% YoY, demonstrating
successful diversification beyond hardware...
[continues...]
============================================================
Q&A Mode — Ask anything about Apple's earnings
You: What drove the Services beat?
Analyst: Services revenue of $23.1B, up 11% YoY, was driven by growth
across the App Store, Apple Music, iCloud, and AppleCare. Management
cited 1B+ paid subscriptions globally...

---

## Setup

**Requirements:** Python 3.9+, Anthropic API key ([get one here](https://console.anthropic.com))

```bash
git clone https://github.com/Chidvy/earnings-report-analyzer.git
cd earnings-report-analyzer

pip install -r requirements.txt

export ANTHROPIC_API_KEY=your_key_here
```

---

## Usage

```bash
# Analyze a PDF (full workflow)
python earnings_analyzer.py report.pdf

# Skip interactive Q&A
python earnings_analyzer.py report.pdf --no-qa

# Save JSON output
python earnings_analyzer.py report.pdf --output results.json

# Analyze raw text
python earnings_analyzer.py --text "Revenue was $5.2B, up 12% YoY..."
```

**Where to get earnings PDFs:**
- [SEC EDGAR](https://www.sec.gov/cgi-bin/browse-edgar) — search any public company, download 10-Q/10-K filings
- Company investor relations pages (Apple, Microsoft, J&J, CVS Health)
- [Motley Fool earnings transcripts](https://www.fool.com/earnings-call-transcripts/) — copy/paste text

---

## Design Decisions

| Choice | Why It Matters |
|---|---|
| Two-pass extraction and summary | Separates factual metric extraction from narrative generation for clarity and reusability |
| JSON-first output | Enables downstream dashboards, alerts, and comparison workflows without re-parsing |
| Multi-turn Q&A with history | Allows analysts to ask follow-up questions without rereading the document or losing context |
| 80K character truncation | Controls API cost and context size while covering most earnings reports |
| LLM-based extraction | Handles varied report formats and layouts without custom parsing rules |

---

## Limitations & Future Work

**Current limitations:** Does not yet validate extracted metrics against source tables, does not perform multi-quarter trend analysis, and requires manual report selection.

**Future improvements:**
- Batch processing across multiple quarters with trend analysis and period-over-period comparison
- Page-level source citations for every extracted metric to enable verification
- Multi-company side-by-side earnings comparison
- Dashboard integration for real-time earnings monitoring
- Healthcare variant for clinical trial and hospital financial reporting

---

## Tech Stack

- Python 3.9+
- [Anthropic Python SDK](https://github.com/anthropic/anthropic-sdk-python)
- Large Language Model API (Claude / OpenAI compatible)

---

## Author

**Durga Meduri** — Business Analytics Manager | MS Business Analytics, UMass Boston

[LinkedIn](https://www.linkedin.com/in/durga-c-meduri/) | [GitHub](https://github.com/Chidvy)
