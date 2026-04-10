⚠️ Scanning Scope

This project scans only the latest commit of the repository.

For a stricter version that scans the entire Git commit history (not just current files), refer to:

👉 https://github.com/AkshitSharma07/CI-CD-Security-Pipeline-Strict




🔐 CI/CD Security Pipeline (DevSecOps)
🚀 What This Project Is

A fully automated CI/CD Security Pipeline built using GitHub Actions that runs security checks on every code commit.

Whenever code is pushed to the repository, multiple security tools automatically scan it before it can be merged.

👉 This approach is known as DevSecOps — integrating security directly into the development lifecycle instead of testing at the end.

⚙️ How It Works — Full Flow
🧪 Job 1: Bandit (SAST)

Performs Static Application Security Testing on Python code.

Scans source code line-by-line
Detects:
SQL Injection
Shell Injection
Weak Cryptography
Hardcoded Passwords
Covers 30+ vulnerability types


📦 Job 2: Safety (Dependency Scanning)

Checks Python dependencies for known vulnerabilities.

Reads requirements.txt
Matches libraries against a live CVE database
Outputs:
CVE ID
Severity
Fixed versions


🔑 Job 3: TruffleHog (Secrets Detection)

Detects hardcoded secrets in Git history.

Scans commits for:
API Keys
AWS Credentials
Tokens
Private Keys
Uses:
--only-verified to reduce false positives


📊 Job 4: Summary
Runs after all scans complete
Generates a pass/fail summary
Stores reports as downloadable artifacts



🧩 Component Breakdown
⚡ GitHub Actions Workflow

📁 .github/workflows/security-pipeline.yml

This is the core pipeline configuration.

Key Elements:
on: push / pull_request → triggers pipeline automatically
runs-on: ubuntu-latest → uses a fresh Linux environment
actions/checkout → clones repository
actions/upload-artifact → saves scan reports
needs: → ensures job dependency order
🔍 Tools Used
🛡️ Bandit — SAST

Developed by the OpenStack Security Project.

Builds Abstract Syntax Tree (AST) of code

Command:

bandit -r . -ll -f json
Reports:
Severity: LOW / MEDIUM / HIGH
CWE references
Common Issues:
B201 → Flask debug mode
B303 → Weak hash (MD5)
B608 → SQL Injection
B602 → subprocess shell=True



📦 Safety — Dependency Scanner

Command:

safety check -r requirements.txt
Detects vulnerable libraries (Supply Chain Attacks)

💡 Example: Log4Shell vulnerability — impacted millions globally



🔑 TruffleHog — Secret Scanner
Scans Git commits for leaked secrets
Detects 700+ credential types
Key Config:
fetch-depth: 1 → scans latest commit
--only-verified → reduces noise



📁 Project Structure
.
├── .github/workflows/security-pipeline.yml
├── app.py
├── requirements.txt




▶️ How to Set Up & Run
1.Create a new GitHub repository
2.Push all project files
3.Go to the Actions tab
4.Make a small change in app.py and push
5.Watch the pipeline execute in real-time
6.Download reports from the Artifacts section



This project scans only the latest commit.

For a stricter version that scans the entire Git commit history, refer to:

👉 CI-CD-Security-Pipeline-Strict GitHub Repository
