DocuGoSync (docuguard) 🛡️📄
==========================

Catching documentation drift on every pull request before outdated prose reaches users. An automated CI & CLI engine that links source-code AST changes and CLI flag modifications directly to natural-language documentation sentences.

🚨 The Problem: Documentation Drift
----------------------------------

According to GitHub’s 2024 Open Source Survey, 86.7% of respondents reported "documentation that is incomplete or difficult to understand" as the #1 most discouraging experience in open-source software.

When a Pull Request renames a CLI flag, changes a function signature, or modifies a default configuration value, existing tools (rustdoc, doctest, mktestdocs) only verify runnable code snippets—completely missing natural-language prose, configuration tables, and flag descriptions.

💡 How docuguard Solves It
-------------------------

DocuGoSync (implemented in the docuguard package) runs automatically on every Pull Request to detect semantic contradictions between code changes and documentation prose:

1. Diff & CLI Inspection: Analyzes Git diffs (git\_analyzer.py) and CLI argument definitions (cli\_analyzer.py) to pinpoint exact behavioral changes.
2. Code-to-Doc Mapping: Indexes AST symbols (code\_indexer.py) and parses documentation (document\_crawler.py, content\_extractor.py) to build implicit links (relationship\_engine.py).
3. Drift Detection & Patching: Flags stale sentences (drift\_detector.py) and generates actionable text corrections (suggestion\_engine.py).

### Example Drift Alert

⚠️ Documentation Drift Detected Code Change: app.py — CLI flag --timeout renamed to --request-timeout (default 30s). Outdated Prose: README.md — "Pass --timeout to configure the connection limit." Suggested Fix: Replace --timeout with --request-timeout.

🏗️ Repository Structure
-----------------------

DocuGoSync/
├── .github/
│   └── workflows/
│       └── docuguard.yml           # GitHub Actions CI workflow for automated PR checks
├── docuguard/                      # Core Python package
│   ├── \_\_init\_\_.py
│   ├── cli\_analyzer.py             # Extracts & compares CLI flags, options, and defaults
│   ├── code\_indexer.py             # Parses source code ASTs and extracts symbols
│   ├── content\_extractor.py        # Extracts clean prose from Markdown/reST/HTML docs
│   ├── document\_crawler.py         # Discovers documentation files across the repository
│   ├── drift\_detector.py           # Detects mismatches between code diffs and doc prose
│   ├── git\_analyzer.py             # Inspects Git commit history and PR diffs
│   ├── relationship\_engine.py      # Maps code symbols & CLI flags to doc sentences
│   └── suggestion\_engine.py        # Generates proposed documentation fixes
├── tests/                          # Automated unit test suite
│   ├── test\_cli\_analyzer.py        # Tests for CLI flag extraction & drift
│   ├── test\_drift\_detector.py      # Tests for prose contradiction detection
│   └── test\_suggestion\_engine.py   # Tests for patch & fix generation
├── app.py                          # Main CLI & CI entry point
└── .gitignore

🚀 Quick Start & Usage
---------------------

### 1. Clone & Install

git clone https://github.com/YOUR-USERNAME/DocuGoSync.git
cd DocuGoSync
pip install google-genai pytest

### 2. Set Your API Key

export GEMINI\_API\_KEY="your\_api\_key\_here"

### 3. Run the Application (app.py)

Run a documentation drift check against your current repository changes:

python app.py

🧪 Running Tests
---------------

The repository includes unit tests under tests/ covering CLI analysis, drift detection, and fix suggestions:

pytest tests/

⚙️ GitHub Actions CI Integration
--------------------------------

Automated drift checks are configured in .github/workflows/docuguard.yml. Whenever a Pull Request or push occurs:

1. GitHub Actions checks out the repository history.
2. Runs python app.py using the GEMINI\_API\_KEY repository secret.
3. Flags any documentation sentences invalidated by the code changes before merge.

👥 Project Context
-----------------

Built for Hackathon Problem Statement 3 (Catching Documentation Drift) — combining deterministic AST/CLI analysis with AI-powered prose auditing.
