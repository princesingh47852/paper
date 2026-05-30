# MP TET CBT Mock Test Portal

A full offline CBT (Computer Based Test) simulator for MP TET exam preparation.

---

## 📁 Folder Structure

```
mptet-cbt/
│
├── index.html               ← Main exam portal (open this in browser)
│
└── papers/
    ├── index.json           ← Master list of all papers (update this when adding a new paper)
    ├── varg3_2022.json      ← Paper: MP TET Varg 3 2022
    ├── varg3_2023.json      ← Paper: MP TET Varg 3 2023  (you create this)
    ├── varg2_2022.json      ← Paper: MP TET Varg 2 2022  (you create this)
    └── ... (add more)
```

---

## 🚀 How to Run

**Option A – VS Code Live Server (recommended)**
1. Open the `mptet-cbt/` folder in VS Code
2. Install the "Live Server" extension
3. Right-click `index.html` → "Open with Live Server"

**Option B – Python server**
```bash
cd mptet-cbt
python -m http.server 8000
# Open http://localhost:8000 in browser
```

> ⚠️ **Do NOT open index.html directly as a file:// URL** — the JSON fetch will fail due to browser security. Always use a local server.

---

## ➕ How to Add a New Paper

### Step 1 — Create the paper JSON file

Create `papers/varg3_2023.json` (or any descriptive name) using this template:

```json
{
  "id": "varg3_2023",
  "title": "MP TET Varg 3 — 2023",
  "subtitle": "Official Paper",
  "year": 2023,
  "varg": 3,
  "totalMarks": 150,
  "durationMinutes": 180,

  "sections": [
    { "name": "Hindi Bhasha 01",     "color": "#f472b6" },
    { "name": "Mathematics",          "color": "#60a5fa" },
    { "name": "Environmental Study",  "color": "#34d399" },
    { "name": "English Language 02",  "color": "#fbbf24" },
    { "name": "Child Development",    "color": "#a78bfa" }
  ],

  "passages": {
    "PASS1": "Your passage text here.\nSupports newlines.\nCan be as long as needed.",
    "PASS2": "Another passage for English section..."
  },

  "questions": [
    {
      "id": 1,
      "section": "Hindi Bhasha 01",
      "hi": "प्रश्न का हिंदी पाठ यहाँ लिखें।",
      "en": "English translation of the question (optional)",
      "options": [
        { "hi": "विकल्प 1", "en": "Option 1" },
        { "hi": "विकल्प 2", "en": "Option 2" },
        { "hi": "विकल्प 3", "en": "Option 3" },
        { "hi": "विकल्प 4", "en": "Option 4" }
      ],
      "answer": 2
    },

    {
      "id": 2,
      "section": "Hindi Bhasha 01",
      "passage": "PASS1",
      "hi": "गद्यांश के अनुसार, ...",
      "en": "According to the passage...",
      "options": [
        { "hi": "...", "en": "..." },
        { "hi": "...", "en": "..." },
        { "hi": "...", "en": "..." },
        { "hi": "...", "en": "..." }
      ],
      "answer": 0
    }
  ]
}
```

### Step 2 — Register the paper in index.json

Open `papers/index.json` and add an entry to the array:

```json
[
  {
    "id": "varg3_2022",
    "title": "MP TET Varg 3 — 2022",
    "subtitle": "Official Paper",
    "year": 2022,
    "varg": 3,
    "totalQuestions": 150,
    "totalMarks": 150,
    "durationMinutes": 180,
    "tags": ["Varg 3", "2022", "Official"]
  },
  {
    "id": "varg3_2023",
    "title": "MP TET Varg 3 — 2023",
    "subtitle": "Official Paper",
    "year": 2023,
    "varg": 3,
    "totalQuestions": 150,
    "totalMarks": 150,
    "durationMinutes": 180,
    "tags": ["Varg 3", "2023", "Official"]
  }
]
```

That's it! The paper will appear in the portal immediately.

---

## 📝 JSON Field Reference

### Paper-level fields
| Field | Required | Description |
|-------|----------|-------------|
| `id` | ✅ | Unique identifier, must match filename (without .json) |
| `title` | ✅ | Displayed as paper title |
| `subtitle` | ✅ | Subtitle shown on card |
| `year` | ✅ | Exam year (used for filter) |
| `varg` | ✅ | 1, 2, or 3 (used for filter) |
| `totalMarks` | ✅ | Max marks |
| `durationMinutes` | ✅ | Exam duration |
| `sections` | ✅ | Array of section objects with name + color |
| `passages` | ❌ | Object mapping passage keys to text |
| `questions` | ✅ | Array of question objects |

### Question fields
| Field | Required | Description |
|-------|----------|-------------|
| `id` | ✅ | Sequential question number |
| `section` | ✅ | Must match a section name in sections[] |
| `hi` | ✅ | Question text in Hindi/Devanagari |
| `en` | ❌ | English translation (leave blank if same) |
| `passage` | ❌ | Key from `passages` object for passage-based Qs |
| `options` | ✅ | Array of exactly 4 option objects |
| `answer` | ✅ | Index of correct option (0, 1, 2, or 3) |

### Option format
```json
{ "hi": "हिंदी विकल्प", "en": "English option" }
```
The `en` field is optional — if omitted, only Hindi text is shown.

---

## 🎨 Section Colors (choose any hex color)

Suggested colors per section type:
- **Hindi**  → `#f472b6` (pink)
- **Math**   → `#60a5fa` (blue)
- **EVS**    → `#34d399` (green)
- **English**→ `#fbbf24` (amber)
- **CDP**    → `#a78bfa` (purple)
- **Science**→ `#fb923c` (orange)
- **Social** → `#38bdf8` (sky)

---

## ✅ Features

- ⏱ Auto countdown timer with warning at 5 minutes
- 🗺 Question palette with status colors (answered / not answered / marked)
- 🔖 Mark for review functionality
- 📊 Section-wise score breakdown on result screen
- ❌ Detailed wrong answer review with correct answers highlighted
- 📱 Mobile responsive (sidebar hides on small screens)
- 🔍 Paper filter by Varg (1, 2, 3)
- ➕ Easily extendable with new papers (just add JSON files)
