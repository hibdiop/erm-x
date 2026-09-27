# Enterprise Risk Engine (ERM-X)

A working prototype demonstrating unified risk telemetry, business impact quantification, and Agentic AI governance for NYC's payroll and financial systems.

### Purpose

This project normalizes disparate risk sources (cloud, vendor, vulnerability, AI) and weights them against mission-critical services.


### Architecture

```mermaid
flowchart TD

    A["data/"] --> A1["SQLite database<br/>(generated)"]

    B["scripts/"] --> B1["01_ingest.py<br/>Provisions DB and loads seed telemetry"]
    B --> B2["02_engine.py<br/>Calculates weighted residual risk"]

    C["app.py<br/>Streamlit executive dashboard"]

    D["docs/"] --> D1["EXECUTIVE_MEMO.md"]
    D --> D2["dashboard_screenshot.png"]

    E["tests/"] --> E1["test_engine.py"]
```

```text
┌─────────────────────────────────────────────────────────────────┐
│                    DATA SOURCES (Simulated)                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐        │
│  │ Security │  │  Vendor  │  │    AI    │  │   Ops    │        │
│  │ Scanner  │  │  TPRM    │  │ Registry │  │Incidents │        │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘        │
└───────┼─────────────┼─────────────┼─────────────┼──────────────┘
        │             │             │             │
        ▼             ▼             ▼             ▼
┌─────────────────────────────────────────────────────────────────┐
│              INGESTION & NORMALIZATION LAYER                    │
│   (Python scripts: 01_ingest.py, ingest_*.py)                   │
│   Maps heterogeneous schemas → unified risk_portfolio schema    │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                    DATA STORE (SQLite)                          │
│  ┌────────────────┐  ┌────────────────┐  ┌────────────────┐    │
│  │ business_      │  │ risk_          │  │ ai_            │    │
│  │ services       │  │ portfolio      │  │ controls       │    │
│  └────────────────┘  └────────────────┘  └────────────────┘    │
│  ┌────────────────┐  ┌────────────────┐  ┌────────────────┐    │
│  │ risk_history   │  │ control_tests  │  │ audit_log      │    │
│  └────────────────┘  └────────────────┘  └────────────────┘    │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│               ANALYTICAL ENGINE (Python/pandas)                 │
│   Weighted residual risk calculation                            │
│   Business impact weighting                                     │
│   Monte Carlo simulation (optional)                             │
│   Stress-test scenario engine                                   │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│              PRESENTATION LAYER (Streamlit)                     │
│   Executive KPI cards                                           │
│   Prioritization queue                                          │
│   AI risk spotlight                                             │
│   Business service reference                                    │
└─────────────────────────────────────────────────────────────────┘
```





### Quick Start

```bash
git clone https://github.com/hibdiop/fisa-erm-x.git
cd fisa-erm-x
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
python scripts/01_ingest.py
streamlit run app.py 
```


<img src="https://github.com/hibdiop/fisa-erm-x/blob/main/Risk.png" alt="Operational Risk Ecosystem" width="900">





### Key Finding
An autonomous AI agent with write-access to the payroll ledger scores 12.00 / 15.0 — the highest enterprise risk in the portfolio. See docs/EXECUTIVE_MEMO.md for the Triple-Gate governance framework.


### Tech Stack
- Python 3.10+
- SQLite3
- pandas
- Streamlit
- OWASP Top 10 for LLMs / NIST AI RMF (conceptual alignment)

