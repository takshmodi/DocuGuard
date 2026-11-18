
# My Application

> **Never repeat past engineering mistakes.** my application extracts hidden architectural decisions and rejected alternatives from developer discussions and surfaces them directly inside new Pull Requests.

---

## 🚨 The Problem
In fast-moving software projects, critical design decisions ("Why did we choose PostgreSQL over MySQL?") are buried in long GitHub issue threads, pull request comments, or forum posts. When contributors leave, that context disappears—causing new developers to waste time re-proposing approaches that were already tested and rejected years ago.

## 💡 Our Solution
**DocuGuard** acts as an automated memory assistant for repositories:
1. **Ingests Discussions:** Reads historical conversations from GitHub issues and discussion logs.
2. **Extracts Decisions:** Uses the **Google AI Studio (Gemini API)** to identify what was decided, which alternatives were rejected, and *why*.
3. **Links to Code:** Maps those decisions directly to the source code files they affect.
4. **Warns Contributors:** Alerts developers when a new change touches code with historical context.

---

## 🏗️ Repository Architecture
* `connectors/` – Adapters for pulling data from GitHub and discussion forums
* `decision-extractor/` – AI pipeline powered by Google Gemini to extract decisions & rationales
* `code-linker/` – Maps extracted decisions to specific source files
* `pr-agent/` – Bot logic for surfacing historical context on Pull Requests

---

## 🛠️ Tech Stack
* **Languages:** C (Fast text parsing/prototyping), Python (AI & API integration)
* **AI Engine:** Google AI Studio (Gemini API)
* **Platform:** GitHub

---

## 🚀 How to Run Locally

### 1. Clone the repository
```bash
git clone https://github.com/YOUR-USERNAME/ProjectRecall.git
cd ProjectRecall
