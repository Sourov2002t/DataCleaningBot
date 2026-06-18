# 🤖 DataCleaningBot

> AI-powered data cleaning web app built with React + Vite and Groq LLM. Upload any CSV, auto-clean it, get AI-generated insights, and download the polished result — all in the browser with zero backend.

---

## ✨ Features

### 📂 Smart CSV Upload
- Drag & drop or click-to-browse file upload
- Instant preview of raw data on load
- Supports any `.csv` file structure

### 🧹 Automatic Data Cleaning Engine
Runs entirely in the browser with no server needed:

| Step | What It Does |
|------|-------------|
| Empty Row Removal | Drops fully empty rows |
| Deduplication | Removes exact duplicate rows |
| Column Drop | Drops columns with >60% missing values |
| Type Detection | Auto-classifies each column as numeric, string, boolean, or datetime |
| Numeric Imputation | Fills missing numbers with the column median |
| String Fill | Fills missing text fields with `"Unknown"` |
| Boolean Normalisation | Casts yes/no/true/false/1/0 to proper booleans |
| Whitespace Normalise | Trims and collapses extra spaces in string cells |

### 🤖 AI Analysis via Groq
Powered by `openai/gpt-oss-120b` through the Groq API, the bot generates a structured markdown report covering:

- **Key Observations** — specific findings using real column names and values
- **Data Quality Assessment** — rated Excellent / Good / Fair / Poor with evidence
- **Patterns & Anomalies** — distributions, relationships, and outliers
- **Why Columns Are Missing** — real-world explanation per column with nulls
- **Improvement Suggestions** — 4 concrete, actionable next steps
- **Recommended Analyses** — best follow-up visualisations and queries

### 📊 Visual Dashboard
Interactive charts and stats built with Recharts:
- Before vs. After cleaning comparison (rows, nulls, duplicates)
- Column type distribution pie chart
- Missing values bar chart per column
- Numeric statistics table (min, max, mean, median, std dev)

### 📥 Export
- Download cleaned data as a UTF-8 CSV (`cleaned_<filename>.csv`)
- Generate and download a full HTML report with embedded charts

### 🔐 Admin API Key Panel
- Admin-only panel (password protected) to configure the Groq API key
- Key stored in `localStorage` — never sent anywhere except directly to Groq
- All users on the same browser share the configured key automatically

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | React 18 |
| Build Tool | Vite 5 |
| AI / LLM | Groq API (`openai/gpt-oss-120b`) |
| CSV Parsing | PapaParse 5 |
| Charts | Recharts 2 |
| Styling | Inline CSS (zero dependencies) |
| Storage | Browser `localStorage` (API key only) |

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ installed
- A free Groq API key from [console.groq.com](https://console.groq.com)

### Installation

```bash
# 1. Clone the repo
git clone https://github.com/your-username/DataCleaningBot.git
cd DataCleaningBot/datacleaning-app

# 2. Install dependencies
npm install

# 3. Start the dev server
npm run dev
```

Then open **http://localhost:5173** in your browser.

---

## 🔑 Setting Up Your Groq API Key

1. Go to [console.groq.com](https://console.groq.com) and create a free account
2. Navigate to **API Keys** → **Create Key** → copy your key (starts with `gsk_`)
3. In the app, click the **🔐 Admin** button (top right)
4. Enter the admin password and paste your API key
5. The key is saved in your browser — AI analysis is now active for all users

> The API key is stored only in your browser's `localStorage` and sent directly to Groq. It is never logged or stored on any server.

---

## 📁 Project Structure

```
datacleaning-app/
├── index.html                  ← App entry point
├── package.json                ← Dependencies & scripts
├── vite.config.js              ← Vite configuration
└── src/
    ├── main.jsx                ← React DOM mount
    └── DataCleaningBot.jsx     ← Entire app (single component)
        ├── detectColType()     ← Column type inference
        ├── calcStats()         ← Numeric statistics
        ├── runCleaning()       ← Full cleaning engine
        ├── buildReport()       ← HTML report generator
        └── DataCleaningBot()   ← Main React component
```

---

## 📋 Available Scripts

```bash
npm run dev        # Start development server (hot reload)
npm run build      # Build for production → dist/
npm run preview    # Preview the production build locally
```

---

## 🖥️ How to Use

1. **Upload** — drag & drop or click to select a CSV file
2. **Review** — inspect the raw data preview and column summary
3. **Clean** — click **Clean Data** to run the automatic cleaning engine
4. **Inspect** — review the cleaning log, before/after stats, and visual charts
5. **Analyse** — click **AI Analysis** to get Groq-powered insights (requires API key)
6. **Export** — download the cleaned CSV or the full HTML report

---

## ⚙️ Cleaning Rules Reference

```
Numeric columns  → median imputation for nulls, strip $,€£% symbols
String columns   → fill nulls with "Unknown", trim/collapse whitespace
Boolean columns  → normalise yes/no/true/false/1/0 → true/false
Columns >60% null → dropped entirely with a log entry
Exact duplicate rows → removed (first occurrence kept)
Fully empty rows → removed before any other step
```

---

## 🔧 Troubleshooting

| Problem | Fix |
|---------|-----|
| `npm run dev` not found | Run `npm install` first |
| Blank page on load | Check browser console for errors; ensure Node 18+ |
| AI Analysis button disabled | Configure Groq API key via the Admin panel |
| API key error | Ensure key starts with `gsk_` and has not expired |
| Charts not rendering | Try a different browser; disable ad-blockers |
| CSV not loading | Ensure file is valid UTF-8 CSV with a header row |

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🙏 Acknowledgements

- [Groq](https://groq.com) — ultra-fast LLM inference API
- [PapaParse](https://www.papaparse.com) — robust CSV parsing for the browser
- [Recharts](https://recharts.org) — composable charting library for React
- [Vite](https://vitejs.dev) — fast frontend build tooling
