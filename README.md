# ChaosGuard AI
**TEAM [Your Team Number] – [Your Course Number, e.g., DAMG7245]**

**ChaosGuard AI** is an autonomous "Safe Autopilot" for CI/CD pipelines. It acts as an automated Site Reliability Engineer (SRE) that detects production failures, performs Root Cause Analysis (RCA) on Git diffs, and safely proposes remediation via Pull Requests, prioritizing immediate mitigation over risky hotfixes.

It leverages Large Language Models (LLMs), LangGraph state machines, and GitHub/Datadog integrations to:
- **Mitigate** outages immediately by recommending or executing rollbacks.
- **Diagnose** root causes by correlating error logs with Git commit diffs (A/B comparison).
- **Remediate** bugs by generating code fixes and opening Pull Requests (never pushing to prod).
- **Audit** every action for compliance and security transparency.

## 🔗 Links

- **Repository**: https://github.com/dhrumil10/chaos-guard-ai
- **Architecture Doc**: [View Architecture](docs/architecture.md)
- **Demo Video**: [Link to Video] *(Coming Soon)*
- **Project Report**: [Link to Google Doc/PDF] *(Coming Soon)*

## 📘 Project Description 

### 1. Mitigation Engine (The First Responder)
- Automatically detects "Critical" severity alerts from CI/CD pipelines.
- Enforces a "Rollback First" policy to restore service stability immediately.
- Prevents "fix-forward" risks during active outages.

### 2. The Detective Agent (RCA)
- Fetches `git diff` between the failing commit and the last known good commit.
- Retrieves stack traces and error logs from observability tools.
- Correlates code changes with errors to identify the "Smoking Gun."

### 3. The Patcher Agent (Remediation)
- Generates precise code patches based on the Detective's findings.
- Runs purely in a sandboxed environment to verify syntax.
- Opens a detailed Pull Request with context, evidence, and fix logic.

### 4. Infrastructure & Orchestration
- **LangGraph**: Manages the state machine (Cyclic graph for retries and human gates).
- **Docker**: Containerized agents for consistent execution.
- **GitHub API**: For reading diffs and managing PRs.

---

## 💻 Technologies and Tools

[![Python](https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue)](https://www.python.org/)
[![LangGraph](https://img.shields.io/badge/LangGraph-1C1C1C?style=for-the-badge&logo=chainlink&logoColor=white)](https://github.com/langchain-ai/langgraph)
[![LangChain](https://img.shields.io/badge/LangChain-2B6CB0?style=for-the-badge&logoColor=white)](https://www.langchain.dev/)
[![FastAPI](https://img.shields.io/badge/fastapi-109989?style=for-the-badge&logo=FASTAPI&logoColor=white)](https://fastapi.tiangolo.com/)
[![Docker](https://img.shields.io/badge/Docker-%232496ED?style=for-the-badge&logo=Docker&color=blue&logoColor=white)](https://www.docker.com)
[![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)](https://github.com/features/actions)
[![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)](https://platform.openai.com/)
[![Datadog](https://img.shields.io/badge/Datadog-632CA6?style=for-the-badge&logo=Datadog&logoColor=white)](https://www.datadoghq.com/)

---

## ⚙️ Setup Instructions (Step-by-Step Guide)

1. **Clone the Repository:**
```bash
git clone [https://github.com/dhrumil10/chaos-guard-ai.git](https://github.com/dhrumil10/chaos-guard-ai.git)
cd chaos-guard-ai
```

2. **Environment Setup:**

```Bash
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

3. **Configure API Keys:**
Create a .env file in the root directory:
```
Code snippet
```
```
OPENAI_API_KEY=your_openai_key_here
GITHUB_TOKEN=your_github_pat_here
DATADOG_API_KEY=your_dd_key_here
```
4. **Run the Agent System**:

``Bash
python src/main.py
``
5. **Run Tests:**

```Bash
pytest tests/
📂 Directory Structure
Plaintext
chaos-guard-ai/
├── config/             # Configuration (API keys, Env vars, Model settings)
├── docs/               # Architecture diagrams and design docs
├── src/
│   ├── agents/         # Agent Definitions (Prompts + LLM Logic)
│   │   ├── detective.py   # Agent 1: RCA & Diff Analysis
│   │   ├── patcher.py     # Agent 2: Code Generation & Fix
│   │   └── auditor.py     # Agent 3: Reporting & Compliance
│   ├── graph/          # LangGraph Workflow Logic
│   │   ├── state.py       # Shared State Schema (The "Brain")
│   │   └── workflow.py    # The Graph Definition (Nodes & Edges)
│   ├── tools/          # Custom Tools for Agents
│   │   ├── git_ops.py     # GitHub API wrappers
│   │   └── observability.py # Datadog/CloudWatch wrappers
│   └── main.py         # Entry point (FastAPI or CLI)
├── tests/              # Unit and Integration tests
├── .env.example        # Template for environment variables
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation
```
## 🏗 Architecture Diagram
```
Code snippet
```
```
graph TD
    Trigger([⚡ Trigger]) --> Rollback{Critical?}
    Rollback -- Yes --> Mitigate[Running Rollback]
    Rollback -- No --> Diagnose[🔍 Detective Agent]
    Mitigate --> Diagnose
    Diagnose --> Policy{🛡️ Policy Check}
    Policy -- Safe --> Patch[🛠️ Patcher Agent]
    Patch --> Verify[🧪 Sandbox Test]
    Verify --> PR[📝 Open PR]
    PR --> Report[📄 Auditor Report]
```
## 👥 Team Members
Dhrumil Patel

## 📜 Disclosures
Plaintext
WE ATTEST THAT WE HAVEN’T USED ANY OTHER STUDENTS’ WORK IN OUR ASSIGNMENT AND ABIDE BY THE POLICIES LISTED IN THE STUDENT HANDBOOK.

### Dhrumil Patel

**MS in Northeastern University, College of Engineering**

[LinkedIn](https://www.linkedin.com/in/dhrumil-patel-10) | [GitHub](https://github.com/dhrumil10)

## 📜 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


