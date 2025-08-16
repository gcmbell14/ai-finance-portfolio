# 🧾 AI-Powered Compliance Monitoring (30-sec overview)

**What it is:** LLM-assisted summaries of AML/KYC/regulatory updates into a **2-page Executive Brief**, mapped to concrete monitoring actions and owners.

**Business impact**
- 80–90% reduction in review time (200 pages → concise brief)
- Clear action list tied to thresholds, controls, and KYC refresh cadence
- Shareable Executive Brief export for stakeholders

**Results (demo)**
- Coverage: 100% of updates summarized
- Flag match rate to recent activity: ~70%
- Positive UAT feedback from analysts (qualitative)

**See it live:** Compliance tab in the hero app → https://github.com/gcmbell14/ai-compliance-risk-insights  
**Screenshot:**  
![Compliance Monitoring Diagram](../visuals/compliance-ai-diagram.png)

<details>
  <summary><strong>Details (inputs, approach, Azure stack, governance, tests)</strong></summary>

## Inputs & Features
- **Regulatory text** (guidance, circulars, policy changes) chunked for LLM context
- **Entity risk flags** (PEP/adverse media) to prioritize changes
- **Transaction snippets** for mapping rules → recent activity
- **Thresholds** (cash, cross-border) and **KYC refresh cadence** to translate text → actions

## Approach
1. **Ingest & chunk** documents (sections/paragraphs).
2. **Summarize** with LLM to produce: key changes, obligations, due dates, owners.
3. **Synthesize an Executive Brief** (Markdown/PDF) + change log.
4. **Map to monitoring**: link actions to thresholds, queries, and KYC schedules.

## Technical Stack
- **AI Platforms:** Azure Cognitive Services (Document Intelligence/Language), Azure OpenAI (GPT)
- **App & Integration:** Streamlit (demo UI), Azure Functions (brief generation API), Azure Blob/SQL (storage)
- **Ops:** Azure Key Vault (secrets), App Insights (telemetry), GitHub Actions (CI, optional)

## App UX
- Paste/upload regulatory excerpt → see **bullet summary**
- **Download Executive Brief (Markdown)** button
- Change log (date, prompt/model version) for audit

## Governance & Auditability
- Redact PII; store **prompt/model versions**, timestamps, approver
- Maintain **exception register** and quarterly attestations
- Keep **source snippets** alongside the brief for traceability

## Metrics (pilot/POC)
| Metric | Target / Example | Notes |
|---|---|---|
| Review time reduction | 80–90% | Large docs → brief |
| Coverage | 100% | All updates summarized |
| Flag match rate | ~70% | Alignment to recent activity |
| Analyst satisfaction | Qual | UAT survey/feedback |

## Test Scenarios (UAT)
- **Cross-border threshold change** → brief updates limit & owners
- **Enhanced due diligence requirement** → action appears with due date
- **KYC cadence update** → schedule adjustment captured

## Next Steps
- Add PDF export & routing for approvals
- Link actions to **live monitoring queries** (SQL/Power BI)
- Introduce SLA tracking and completion dashboards

</details>
