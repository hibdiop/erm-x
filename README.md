# Enterprise Risk Engine (ERM-X)

A working prototype demonstrating unified risk telemetry, business impact quantification, and Agentic AI governance for payroll and financial systems.

### Purpose

This project normalizes disparate risk sources (cloud, vendor, vulnerability, AI) and weights them against mission-critical services.


### Architecture



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

## Reference Frameworks

| Framework | Purpose | Link |
|---|---|---|
| NIST CSF 2.0 | Cybersecurity framework | [nist.gov/cyberframework](https://nist.gov/cyberframework) |
| NIST AI RMF 1.0 | AI risk management | [nist.gov/itl/ai-risk-management-framework](https://nist.gov/itl/ai-risk-management-framework) |
| OWASP Top 10 for LLMs | LLM security risks | [owasp.org/www-project-top-10-for-large-language-model-applications](https://owasp.org/www-project-top-10-for-large-language-model-applications) |
| ISO/IEC 27001 | Information security management | [iso.org/standard/27001](https://iso.org/standard/27001) |
| COSO ERM | Enterprise risk management | [coso.org](https://coso.org/) |
| FAIR | Quantitative risk analysis | [fairinstitute.org](https://fairinstitute.org/) |

## Streamlit Snapshot

<img src="https://github.com/hibdiop/fisa-erm-x/blob/main/Risk.png" alt="Operational Risk Ecosystem" width="900">





### Key Finding
An autonomous AI agent with write-access to the payroll ledger scores 12.00 / 15.0 — the highest enterprise risk in the portfolio. See docs/EXECUTIVE_MEMO.md for the Triple-Gate governance framework.




### Tech Stack
- Python 3.10+
- SQLite3
- pandas
- Streamlit
- OWASP Top 10 for LLMs / NIST AI RMF (conceptual alignment)

