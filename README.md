# Improving Pull Requests with PR-Agent & SonarQube

This guide explains how **[PR-Agent](https://github.com/Codium-ai/pr-agent)** and **[SonarQube](https://www.sonarsource.com/products/sonarqube/)** can be used individually to improve pull requests, and how they differ.

---

## 1. PR-Agent — How It Works Alone

**Purpose:** AI-assisted pull request reviews and summaries.

**How It Works:**
1. **Installation & Integration**  
   - Install PR-Agent as a GitHub/GitLab/Gitea/Bitbucket app or run it via a webhook/bot in your infrastructure.
   - Configure API keys for the AI model (e.g., OpenAI, DeepSeek, Ollama).
   
2. **Triggering a Review**
   - When a PR is created or updated, PR-Agent automatically:
     - Reads the diff.
     - Generates a summary.
     - Suggests improvements.
   - Or, you can trigger it manually with a PR comment:  
     ```
     /review
     ```
   
3. **What It Produces**
   - AI-generated comments inside the PR.
   - Feedback on:
     - Code structure
     - Style consistency
     - Security hints
     - Readability suggestions
   - Optional: `/suggest` can rewrite code snippets.

**Key Benefits:**
- Fast first-pass review.
- Reduces reviewer workload.
- Context-aware explanations for changes.

**PR-Agent Workflow**  
```
Developer Creates/Updates PR
           │
           ▼
    PR-Agent Reads Diff
           │
           ▼
 AI Generates Summary & Suggestions
           │
           ▼
 Feedback Posted in PR Comments
```

---

## 2. SonarQube — How It Works Alone

**Purpose:** Static code analysis & enforcing quality gates.

**How It Works:**
1. **Installation & Setup**
   - Install SonarQube server (self-hosted or use [SonarCloud](https://sonarcloud.io)).
   - Integrate it into your CI/CD pipeline using:
     - GitHub Actions
     - Jenkins
     - Azure DevOps
     - GitLab CI, etc.
   
2. **PR Analysis Process**
   - Developer pushes changes → CI/CD triggers SonarQube scan.
   - SonarQube analyzes:
     - Only changed code (Pull Request mode).
     - Checks against language-specific rules.
   
3. **What It Produces**
   - Bug detection
   - Vulnerability alerts
   - Maintainability (code smell) warnings
   - Test coverage metrics
   - Duplicated code reports
   - Pass/fail **Quality Gate** status in the PR.

**Key Benefits:**
- Objective, rule-based checks.
- Prevents low-quality code from merging.
- Supports 25+ programming languages.

**SonarQube Workflow**  
```
Developer Pushes Code / Opens PR
           │
           ▼
     CI/CD Pipeline Runs
           │
           ▼
 SonarQube Scans Changed Code
           │
           ▼
  Generates Report & Quality Gate
           │
           ▼
   Pass/Fail Status on PR + Dashboard
```

---

## 3. Differences in Action

| Feature                | PR-Agent | SonarQube |
|------------------------|----------|-----------|
| **When It Runs**       | When PR is opened/updated or on command | During CI/CD pipeline |
| **How It Analyzes**    | AI reading diff & context | Static rule-based analyzers |
| **Output Location**    | PR comments | PR status check + SonarQube dashboard |
| **Focus**              | Readability, style, context | Bugs, vulnerabilities, maintainability |
| **Dependency**         | AI API key | SonarQube server/cloud instance |

---

## 4. Summary  
- **Use PR-Agent alone** if you want fast, human-like feedback inside PRs.  
- **Use SonarQube alone** if you want strict rule enforcement and detailed code health metrics.  
- **Use both together** for the best of AI + static analysis.  
