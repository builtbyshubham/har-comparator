# HAR Comparator – Performance Regression & API Change Analyzer

An **open-source HAR file comparison tool** designed to detect **API regressions, payload changes, header differences, and performance deviations** between two application runs.

This repository focuses on **engineering clarity, correctness, and extensibility**. It is intended for developers, QA/performance engineers, and as a **serious backend / SDE portfolio project**.

---

## 🚀 Why HAR Comparator?

In distributed systems, regressions often appear in subtle ways:

* Payload fields change silently
* Headers are modified by middleware or gateways
* Response times degrade after deployment

These issues are difficult to detect using logs or dashboards alone.

**HAR Comparator provides a deterministic, request-level comparison between two executions**, making regressions explicit and reviewable.

---

## 🚧 Project Status

> **Status:** 🛠️ Under Active Development

The project is **functional but evolving**. Core parsing, comparison, and reporting features are implemented and stable. Scalability, persistence, and automation layers are planned and tracked.

The repository is intentionally public to:

* Encourage architectural feedback
* Enable transparent iteration
* Serve as a reference implementation

---

## ⚠️ Known Limitations & Open Issues

The following items are **known, intentional gaps** in the current version. These are architectural features under design — not bugs.

---

### 🔐 Authentication & User Management (Pending)

* No user login or authentication
* No user or role separation
* Application runs in a single-user local mode

**Planned:**

* JWT-based authentication
* OAuth (Google / GitHub)
* Role-based access control

---

### 💾 Data Persistence (Pending)

* No database integration
* Results are not persisted across restarts
* No project or comparison history

**Planned:**

* PostgreSQL-backed persistence
* User → Project → HAR upload hierarchy
* Metadata storage (raw HAR files excluded)

---

### 📤 Manual HAR Upload Only

* HAR files must be uploaded manually
* No CI/CD or automated capture

**Planned:**

* CI integration (GitHub Actions / Jenkins)

---

### 🧠 In-Memory Processing

* Parsing and comparison are in-memory
* Large HAR files (10k+ entries) may increase CPU/memory usage

**Planned:**

* Redis caching
* Background workers for heavy diffs

---

### 🧾 Header Noise

* Auth tokens and trace headers may produce non-actionable diffs
* Header filtering is minimal

**Planned:**

* Configurable header allowlist / denylist

---

### 🧮 Payload Diff Cost

* Character-level diffs are computationally expensive
* Executed synchronously

**Planned:**

* Payload hashing
* Selective diff execution

---

## ✨ Current Features

### 🔍 Request Comparison

* ➕ Added requests
* ➖ Removed requests
* 🔄 Status code changes
* ✅ Fully unchanged requests

### 🧠 Difference Analysis

* Character-level payload diff (side-by-side)
* Request header comparison
* Classification of payload-only, header-only, or combined changes

### 📊 Performance Analysis

* Response time deviation (absolute and percentage)
* Endpoint-level latency comparison

### 📄 Reporting

* Excel export (added / removed / changed / payload diff / deviation)
* Standalone HTML report with highlighted diffs

---

## 🏗️ Architecture Overview

The project follows a **layered architecture** inspired by backend service design:

```
UI (Streamlit)
   ↓
Services Layer (Orchestration, Caching, Exports)
   ↓
Core Domain Logic (Parsing, Comparison, Diffing)
   ↓
Utilities & Helpers
```

This separation enables:

* Clear responsibility boundaries
* Easier refactoring and extension
* Straightforward integration of caching and persistence layers

---

## 📁 Project Structure

```
har-comparator/
│
├── app.py                     # Streamlit entry point
│
├── core/                      # Core domain logic
│   ├── har_parser.py
│   ├── comparator.py
│   ├── payload_diff.py
│   └── header_diff.py
│
├── services/                  # Orchestration and exports
│   ├── cache_service.py
│   ├── analytics_service.py
│   └── export_service.py
│
├── ui/                        # Streamlit UI components
│   ├── styles.py
│   ├── loaders.py
│   ├── tabs.py
│   └── components.py
│
├── utils/                     # Shared helpers
│   ├── hashing.py
│   ├── pagination.py
│   └── helpers.py
│
├── models/                    # Data models / schemas
│   └── schemas.py
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## 🛠️ Tech Stack

| Layer           | Technology                    |
| --------------- | ----------------------------- |
| UI              | Streamlit                     |
| Data Processing | Python, Pandas                |
| Diff Engine     | difflib (character-level)     |
| Caching         | Streamlit cache (Redis-ready) |
| Export          | Excel (openpyxl), HTML        |
| Architecture    | Modular, service-oriented     |

---

## ⚙️ Installation & Run

```bash
git clone https://github.com/your-username/har-comparator.git
cd har-comparator
pip install -r requirements.txt
streamlit run app.py
```

---

## 🧪 High-Level Workflow

1. Upload **Old** and **New** HAR files
2. Parse HAR logs into normalized request entries
3. Match requests using `(URL + Method)`
4. Classify differences (added, removed, changed, unchanged)
5. Compute payload, header, and latency differences
6. Render results and export reports

---

## 📈 Roadmap (High-Level)

* Redis-based caching
* Persistent storage (PostgreSQL)
* Automated CI/CD ingestion
* Async diff processing
* Multi-project and multi-user support

---

## 🎯 Intended Use

* Deployment regression analysis
* API contract validation
* Performance engineering workflows
* Backend / SRE debugging
* Engineering portfolio demonstration

---

## 👤 Author

**Shubham Pandey**
Software Engineer | Backend & Systems

---

## 📌 Note

This repository prioritises **engineering discipline and system design clarity** over feature completeness. Trade-offs and limitations are documented intentionally.

Contributions, feedback, and architectural discussions are welcome.
