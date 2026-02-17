# BOLD prevention project
Enabling prevention through data for individuals with multiple needs. 
How to transform the use of data across agencies to personalise services to manage down socioeconomic risk, tackle rising demand pressures across public services, and improve the lives of the most vulnerable in society.

#!python -m venv .venv && . .venv/bin/activate

# MoJ/BOLD Project Specification — BOLD prevention

> **Doc owner:** Dr. Leila Yousefi 
> **Senior Responsible Owner (SRO):** <Name>  
> **Delivery lead:** <Name>  
> **Data Protection Officer contact:** <Name/Team>  
> **Last updated:** <YYYY-MM-DD>  
> **Status:** Draft / In review / Approved  
> **Programme alignment:** MoJ / BOLD / Other: <...>  
> **Links:** <Repo>, <Data catalog>, <DPIA>, <DSA/MoU>, <AQA log>, <Model registry>, <Runbook>

---

## 0) Executive summary (plain English)
- **What problem are we solving and for whom?**
- **What data is being linked/used (high level)?**
- **What will the system do (prediction / decision support / LLM assistance)?**
- **What is the public benefit / intended outcomes?** (BOLD emphasis on outcomes from joined-up data)
- **Key risks & mitigations:** <3–5 bullets>

---

## 1) Scope, outcomes and success criteria
### 1.1 Objective and users
- **Operational/policy objective:** <...>
- **Primary users / decision points:** <...>
- **AI role:** decision support / triage / forecasting / insight / summarisation / extraction / RAG / other

### 1.2 In-scope / out-of-scope
- In scope: <...>
- Out of scope: <...>

### 1.3 Success metrics (set upfront)
- **Outcome metrics:** <service/user outcomes aligned to BOLD>
- **Model metrics:** <AUC/F1/MAE/Calibration + confidence intervals where relevant>
- **Data-linkage metrics:** <linkage rate, false match estimate, join coverage>
- **Operational metrics:** <latency, throughput, cost, analyst time saved>
- **Minimum acceptance criteria:** <go/no-go thresholds + sign-off>

---

## 2) UK governance and assurance (mandatory artefacts)
> Complete/attach these before moving beyond discovery where personal data or significant risk is present.

### 2.1 Data protection & information governance
- **Is personal data processed?** yes/no  
- **Lawful basis & purpose:** <UK GDPR basis + DPA 2018 considerations; note if Part 3 law enforcement processing applies> :contentReference[oaicite:1]{index=1}
- **DPIA:** link + status + key risks/actions :contentReference[oaicite:2]{index=2}
- **Data Sharing Agreement / MoU:** link + parties + purpose + retention + disposal :contentReference[oaicite:3]{index=3}
- **Security classification & handling:** <Official / Official-Sensitive etc; reference MoJ handling guidance if applicable> :contentReference[oaicite:4]{index=4}

### 2.2 Ethical and public benefit assurance
- **Ethics framework self-assessment:** link + outcomes (Data & AI Ethics Framework / prior Data Ethics Framework) :contentReference[oaicite:5]{index=5}
- **Public benefit statement:** why linking/AI is necessary and proportionate (BOLD emphasis on “safe, secure and ethical” linking) :contentReference[oaicite:6]{index=6}
- **Public engagement considerations:** affected groups, transparency commitments, comms plan (if relevant to BOLD-style work)

### 2.3 Analytical quality assurance (AQA)
- **AQA approach (AQuA Book):** proportionate checks, independent review, sign-off points :contentReference[oaicite:7]{index=7}
- **Evaluation approach (Magenta Book) if assessing interventions/outcomes:** link/summary :contentReference[oaicite:8]{index=8}

### 2.4 Safe access model (Five Safes / TRE)
- **Safe Projects:** purpose, public benefit, approvals
- **Safe People:** who can access, training/accreditation
- **Safe Data:** minimisation, de-identification, pseudonymisation
- **Safe Settings:** where processing happens (eg TRE/SDE), controls
- **Safe Outputs:** disclosure control/output checking process :contentReference[oaicite:9]{index=9}

---

## 3) Data inventory and acquisition (collection)
### 3.1 Data sources register
| Dataset | Owner | System of record | Location | Access method | Frequency | Sensitivity/PII | Notes |
|---|---|---|---|---|---|---|---|
| <...> | <...> | <...> | <...> | <SQL/API/files> | <...> | <...> | <...> |

### 3.2 Collection/extraction plan
- **Ingestion mode:** batch / near-real-time / streaming / secure transfer
- **Incremental logic:** CDC keys / watermarks / late-arriving events policy
- **Backfill plan:** time range, idempotency, reconciliation checks
- **Retention & disposal:** raw/curated/features; deletion triggers; audit trail

### 3.3 Minimisation & proportionality (UK standard practice)
- **Minimum necessary fields:** <list>
- **Purpose limitation:** how use stays within stated purpose
- **Access controls:** roles, approvals, logging

### 3.4 Data dictionary (minimum viable)
- **Entities:** <Person/Case/Service contact/Offence/Appointment/Document…>
- **Keys:** <person_id, case_id, event_id…>
- **Time semantics:** event_time vs ingestion_time; timezone; “as at” rules
- **Label/target definition:** <precise; windowing; leakage notes>

---

## 4) Data quality, validation and monitoring
### 4.1 Automated validation tests (define thresholds)
- **Schema:** required columns, types, constraints
- **Completeness:** null thresholds per critical field
- **Uniqueness:** PK uniqueness
- **Referential integrity:** FK validity / domain checks
- **Freshness SLA:** expected availability time

### 4.2 Observability & drift
- **Data drift:** distribution checks on key variables
- **Linkage drift:** match rate changes; join coverage changes
- **Label delay & backfill impacts:** how monitored and corrected

### 4.3 Failure policy
- **Block pipeline if:** <critical checks fail>
- **Degrade if:** <optional feeds missing>
- **Incident response:** owner, escalation, comms

---

## 5) Pre-processing and manipulation specification
> Must support reproducibility and train/serve parity.

### 5.1 Cleaning rules (explicit)
- Missing values: <drop/impute/sentinel>
- Outliers: <cap/remove/robust handling>
- Normalisation/scaling: <method + parameters + where stored>
- Deduplication: <rules + tie-breakers>
- Text processing: <normalise, redact, language detection, PII removal rules>

### 5.2 Transform pipeline (reproducible)
- **Pipeline steps (ordered):**
  1. <...>
  2. <...>
- **Determinism:** random seeds, stable sorts, versioned reference tables
- **Versioning:** code + config + dataset snapshot IDs
- **Lineage:** raw → curated → linked → features → train/test splits

### 5.3 Leakage controls (especially for linked admin data)
- **Prediction time definition:** <T0>
- **Only use data available before T0:** how enforced (time filters / as-of joins)
- **Post-event variables:** explicitly excluded list

---

## 6) Data linking (BOLD core)
### 6.1 Linkage purpose and approach
- **Why link?** (benefit vs risk; why single datasets insufficient)
- **Linkage type:** deterministic / probabilistic / hybrid / graph-based
- **Linkage unit:** person / household / case / location / organisation

### 6.2 Match keys and rules
- **Primary match keys:** <...>
- **Secondary/fallback keys:** <...>
- **Standardisation rules before matching:** <names/addresses/DOB formats etc.>
- **Blocking strategy (if probabilistic):** <...>

### 6.3 Linkage quality and error measurement
- **Linkage rate targets:** <...>
- **False match / missed match estimation:** method + sample design
- **Clerical review (if any):** process + audit trail
- **Sensitivity analysis:** effect of linkage error on model outcomes

### 6.4 Join semantics (downstream features)
- **Join types:** left/inner + rationale
- **Temporal joins:** as-of logic; window length; late data handling
- **Coverage monitoring:** join coverage by subgroup, time, source

---

## 7) Predictive modelling specification (non-LLM)
### 7.1 Modelling task and baselines
- Task: classification / regression / ranking / forecasting
- Baseline: <simple heuristic/GLM>
- Candidate models: <GBM, survival, hierarchical, neural, etc.>
- Constraints: explainability, latency, cost, fairness, operational usability

### 7.2 Evaluation design (AQA-ready)
- **Split strategy:** time-based / grouped / stratified; rationale
- **Primary metrics:** <...>
- **Uncertainty:** confidence intervals / bootstrapping
- **Subgroup performance:** protected characteristics where lawful/appropriate; proxy risk notes
- **Calibration:** reliability curves; decision thresholds

### 7.3 Deployment and monitoring
- Batch vs online: <...>
- Monitoring: performance, drift, linkage drift, data quality, latency
- Rollback/kill switch: <...>
- Documentation: model card / decision record / runbook

---

## 8) LLM specification (LLMs + RAG + safety)
### 8.1 Use cases and boundaries
- Use cases: extraction / summarisation / triage notes / Q&A / drafting / decision support
- **What the LLM must never do:** (eg make final decisions; reveal personal data; invent sources)

### 8.2 Data handling for LLMs (UK IG controls)
- **Inputs:** which fields/docs; redaction rules; PII minimisation
- **Where processing occurs:** approved environment; vendor/tool assurance notes
- **Logging & retention:** what is stored; retention period; access controls
- **Prompt injection & data exfiltration risks:** controls and testing plan

### 8.3 RAG design (if used)
- Corpus definition + versioning
- Chunking strategy
- Embedding model + vector index + refresh cadence
- Retrieval: top-k, filters, hybrid search, reranking
- Grounding: citations required, answer constraints, “I don’t know” policy
- Evaluation: retrieval recall@k, groundedness/faithfulness rubric, adversarial tests

### 8.4 Fine-tuning (if used)
- Training data spec: sources, sampling, de-duplication, labelling
- Safety filters: disallowed content, privacy screening
- Overfitting controls: holdout sets, topic diversity, regression tests

### 8.5 LLM evaluation & assurance
- Offline eval set: representative + edge cases
- Human review: rubric + inter-rater agreement
- Harm testing: bias, toxicity, privacy leakage, hallucination
- Release criteria: go/no-go thresholds + sign-off

---

## 9) Implementation: pipelines, environments, and controls
### 9.1 Pipelines (reproducible, auditable)
- Ingestion: <tool/schedule/retries>
- Linking: <tool/approach/logging>
- Feature build: <feature store or tables>
- Training: <orchestration + experiment tracking>
- Inference: <batch/online + SLAs>

### 9.2 Secure environments and access
- Dev/stage/prod separation
- Secrets management
- Output checking/disclosure controls (Five Safes: Safe Outputs)

### 9.3 Cost and sustainability
- Compute budget/quotas
- Data refresh cadence vs need
- Technical debt plan

---

## 10) Risks, assumptions, and open questions
### 10.1 Key risks & mitigations
| Risk | Likelihood | Impact | Mitigation | Owner | Review date |
|---|---:|---:|---|---|---|
| <...> | <L/M/H> | <L/M/H> | <...> | <...> | <...> |

### 10.2 Assumptions (with validation)
- <Assumption> → validation plan: <...>

### 10.3 Open questions
- <Question> (owner: <...>, due: <...>)

---

## 11) Deliverables and sign-off
### 11.1 Deliverables checklist
- [ ] Data source register + dictionary
- [ ] DPIA completed/approved (if required)
- [ ] Data sharing agreement/MoU in place (if required)
- [ ] Five Safes assessment recorded
- [ ] Linkage method + linkage quality report
- [ ] Reproducible pipelines + automated data tests
- [ ] Model/LLM evaluation report + monitoring plan
- [ ] AQA sign-off recorded
- [ ] Runbook + incident process

### 11.2 Sign-off table
| Area | Approver | Date | Notes |
|---|---|---|---|
| Product / policy | <...> | <...> | <...> |
| Data owner(s) | <...> | <...> | <...> |
| Information governance / DPO | <...> | <...> | <...> |
| Security | <...> | <...> | <...> |
| Lead analyst (AQA) | <...> | <...> | <...> |
| Technical lead | <...> | <...> | <...> |
