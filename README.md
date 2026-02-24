# 🚀 Release Risk Intelligence Agent

A multi-agent, context-aware release risk evaluation system that analyzes pull requests before merge and provides structured risk recommendations.

Instead of relying only on static branch protection rules, this system evaluates change intent, code impact, and historical regression patterns to generate a calibrated risk score.

---

## 🧠 What This Project Does

When a Pull Request is raised, the system:

1. Interprets the PR intent
2. Analyzes changed files
3. Retrieves similar historical issues using RAG
4. Aggregates multi-signal intelligence
5. Computes a risk score (0–100)
6. Validates decision consistency
7. Sends Slack notification:

- ✅ Safe to Merge  
- ❗ Needs Manual Review  

---

## 🏗 Architecture Overview

The system is built using a multi-agent orchestration workflow in n8n.
<img width="1704" height="760" alt="image" src="https://github.com/user-attachments/assets/85434282-93c6-402b-95a9-11d872f7e144" />

### 🧠 Release Intent Planner
- Interprets PR title and commit message
- Identifies impacted domains
- Defines testing objectives
<img width="338" height="166" alt="image" src="https://github.com/user-attachments/assets/8e25ab90-b73e-4ecd-8556-cf1e9aabb3db" />

### 🔎 Static Change Risk Engine (Git Diff Analyzer)
- Analyzes changed files
- Classifies change type (feature / fix / refactor)
- Detects critical modules
<img width="200" height="237" alt="image" src="https://github.com/user-attachments/assets/7e4b7025-1cc1-4e5e-835a-068b5bb28349" />

### 📚 Historical Regression Intelligence (RAG Layer)
- Stores historical bug patterns in vector store
- Performs semantic similarity search
- Extracts recurring failure signals
- Generates contextual risk weight
<img width="653" height="233" alt="image" src="https://github.com/user-attachments/assets/f5846526-1cd6-46dd-8dd2-765985571526" />

### ⚖️ Release Risk Decision Engine
- Aggregates planner, diff, and historical signals
- Computes calibrated risk score (0–100)
- Produces confidence metric
- Recommends action
- <img width="204" height="246" alt="image" src="https://github.com/user-attachments/assets/7e85eb26-0285-46ce-bf43-9febae5f576c" />


### 🛡 Release Governance Guardrail (Validation Agent)
- Validates scoring consistency
- Detects conflicting signals
- Adjusts confidence if required
<img width="169" height="234" alt="image" src="https://github.com/user-attachments/assets/7033d808-e6dd-485c-8651-cddc2c8ad2de" />

---

## 🔔 Final Output

Slack Notification:

- ✔ Safe to Merge  
- ❗ Needs Manual Review  

With structured reasoning and risk score.
![Slack](https://github.com/user-attachments/assets/6cd1bcf1-c584-45c2-8665-89e0279e585b)

---

## 🛠 Tech Stack

- n8n (workflow orchestration)
- Multi-Agent Structured Outputs
- Vector Store (RAG)
- GitHub Integration
- Slack Integration

---

# 🔗 GitHub Trigger Setup

There are two ways to connect GitHub to this workflow.
---

## ✅ Method 1 — Using GitHub Trigger Node (Automatic)
Recommended if you have repository admin access.
### Steps:
1. Generate GitHub Personal Access Token (classic)
   - Go to GitHub → Settings → Developer Settings → Personal Access Tokens
   - Select scopes:
     - `repo`
     - `admin:repo_hook`
2. Add GitHub credential in n8n
   - Authentication: Personal Access Token
   - Paste token
3. Add GitHub Trigger Node
   - Event: Pull Request
   - Repository: Select your repo
4. Add IF condition:
   - `action == opened`

Now the workflow triggers automatically when a new PR is raised.
---

## ✅ Method 2 — Using Webhook Node (Manual Setup)
Recommended if you do not have admin privileges for auto-hook creation.
### Steps:
1. Add a Webhook node in n8n
2. Copy the generated webhook URL
3. Go to your GitHub repository:
   - Settings → Webhooks → Add Webhook
4. Configure:
   - Payload URL: (n8n webhook URL)
   - Content Type: `application/json`
   - Event: Pull Requests
5. Save webhook

Now the workflow triggers when a PR is opened.
---
# 📊 Risk Scoring Logic
Risk Score (0–100) is computed using:
- PR intent classification
- File impact sensitivity
- Historical regression similarity (RAG)
- Multi-signal aggregation
- Confidence calibration

No hardcoded rules.
No blind approvals.
Structured reasoning with explainability.
---
# 🚧 Future Improvements
- Persistent vector database (Pinecone / Supabase)
- CI log intelligence integration
- Weighted risk calibration tuning
- Dashboard for historical risk analytics
- PR auto-approval for low-risk cases
---
# 💡 Why This Project?
Traditional CI/CD gates are rule-based.
This system explores contextual release intelligence:
- Predictive instead of reactive
- Multi-signal instead of single-metric
- Structured reasoning instead of binary checks
---
## 👩‍💻 Author
Built as a personal project to explore:
- Agent orchestration
- RAG-based reasoning
- Risk synthesis pipelines
- AI-assisted release governance

---

⭐ If you find this interesting, feel free to fork or share feedback!
