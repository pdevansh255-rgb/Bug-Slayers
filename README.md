# 🩺 Vitalis — AI Healthcare Agent

Vitalis is a **rule-based AI healthcare reasoning agent** built and demoed in a
Jupyter Notebook (`agent.ipynb`). It reasons across six healthcare domains —
symptom triage, hospital routing, medication safety, hereditary risk, lab
interpretation, and health tracking — entirely offline, with no external APIs,
no network calls, and no paid services required.

This repository also contains the original interactive web-app prototype
(`vitalis-agent.html`) that the notebook agent is ported from.

> ⚠️ **Medical disclaimer:** Vitalis is an educational, rule-based reasoning
> demo. It is **not** a medical device, does **not** provide medical
> diagnoses, and does **not** replace a licensed clinician. In a real
> emergency, always contact local emergency services directly.

---

## 1. Features

| Module | Description |
|---|---|
| 🩺 **Symptom Intelligence** | Parses a free-text symptom description, scans for critical red-flag patterns, and returns a severity level (self-care / clinic / urgent-care / emergency), likely causes, and a recommended specialty |
| 🏥 **Hospital Navigator** | Ranks a local hospital directory by specialty fit and estimated ETA, with real Google Maps directions |
| 💊 **Medicine & Interaction Checker** | Tracks medications, logs doses, and flags known drug-drug interactions (e.g. Warfarin + Ibuprofen) |
| 👪 **Family Risk Mapping** | Builds a hereditary-risk map from a family health profile, weighted by relation (parent/sibling/child vs. grandparent) |
| 🧪 **Lab Report Explainer** | Parses pasted lab values and flags anything outside the normal adult reference range, in plain language |
| 📊 **Health Dashboard** | Aggregates everything the agent has tracked into one summary view, with a chart |

---

## 2. Development Environment

- **Jupyter Notebook** — build and run the agent in `agent.ipynb` (recommended, works locally)
- **Google Colab** — upload `agent.ipynb` if you don't want to configure anything locally
- Any other standard Python 3.9+ environment that can run Jupyter notebooks also works

---

## 3. GitHub Project Structure

```
AI-Agent-Project/
├── README.md
├── agent.ipynb
├── requirements.txt
├── data/
│   └── sample_data/
│       ├── sample_family_profile.json
│       ├── sample_medications.json
│       └── sample_lab_report.txt
├── screenshots/
│   ├── dashboard_example.png
│   └── project_structure_reference.png
├── vitalis-agent.html        (original interactive prototype)
├── LICENSE
└── .gitignore
```

---

## 4. Quick Start

### Option A — Run locally

```bash
# 1. Clone your repository
git clone https://github.com/<your-username>/AI-Agent-Project.git
cd AI-Agent-Project

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch Jupyter and open the notebook
jupyter notebook agent.ipynb
```

Then run the cells from top to bottom with `Shift + Enter`.

### Option B — Run in Google Colab

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. `File → Upload notebook` → select `agent.ipynb`
3. Run all cells (`Runtime → Run all`)

---

## 5. How the agent works

`agent.ipynb` is organized into numbered sections that mirror the six modules
above. Each section defines:

1. A **knowledge base** (Python dicts/lists) — e.g. symptom → specialty
   mappings, drug interaction pairs, lab reference ranges
2. A **reasoning function** that scores/classifies the input against that
   knowledge base
3. A short **worked example** so you can see the agent run immediately after
   opening the notebook

Everything is wrapped at the end into a single `VitalisAgent` class so the
whole toolkit can be driven from one object:

```python
vitalis = VitalisAgent()
vitalis.check_symptoms("Sharp pain in my lower right abdomen, mild fever", age=34, severity="moderate")
vitalis.find_hospitals(specialty="Cardiology", city="Mumbai")
vitalis.add_medication("Metformin", dose="500mg", times="9:00 AM")
vitalis.analyze_family_risk()
vitalis.explain_labs("Glucose: 110 mg/dL\nTSH: 5.8 mIU/L")
vitalis.dashboard()
```

State (symptom history, medications, family profile, lab checks) persists
between notebook sessions in `data/vitalis_state.json`.

---

## 6. Sample data

The `data/sample_data/` folder contains example inputs you can paste directly
into the notebook to try each module immediately:

- `sample_family_profile.json` — a 3-person family health history
- `sample_medications.json` — two medications that trigger a known interaction
- `sample_lab_report.txt` — a lab report with several out-of-range values

---

## 7. Screenshots

`screenshots/dashboard_example.png` shows the notebook's dashboard chart
output, and `screenshots/project_structure_reference.png` is the assignment
reference used to structure this repository.

---

## 8. License

Released under the [MIT License](LICENSE), with an included medical
disclaimer. See the `LICENSE` file for details.

## 9.Updated README




