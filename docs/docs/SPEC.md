<!-- BEGIN FILE: SPEC.md -->
# BOLD prevention project
Enabling prevention through data for individuals with multiple needs. 
How to transform the use of data across agencies to personalise services to manage down socioeconomic risk, tackle rising demand pressures across public services, and improve the lives of the most vulnerable in society.

```bash
# Optional local setup (if needed for repo tooling)
#!python -m venv .venv && . .venv/bin/activate
```


# MoJ/BOLD Project Specification — BOLD prevention

> **Doc owner:** Dr. Leila Yousefi 
> **Senior Responsible Owner (SRO):** MoJ Justice Data (Cross-Government Division) Deputy Director — on behalf of MoJ & HMT Prevention sponsors (TBC)  
> **Delivery lead:** BOLD Prevention Workstream Lead (CGD) (TBC)  
> **Data Protection Officer contact:** MoJ Information Assurance / DPO function (TBC)
> **Last updated:** <YYYY-MM-DD>  
> **Status:** Draft (for review)  
> **Programme alignment:** MoJ Justice Data (CGD) | BOLD Partnership | Data First | HMT Prevention Framework (2024) | System Challenge K (2024)  
> **Links:** Repo: TBC | Data catalog: MoJ Data Catalogue + Data First dataset catalogue | DPIA: TBC | DSA/MoU: TBC | AQA log: TBC | Model registry: TBC | Runbook: TBC

---

## 0) Executive summary (plain English)
- **What problem are we solving and for whom?** Rising prevalence of multiple, overlapping socioeconomic needs is driving costly, late intervention and increasing demand on public services. This workstream supports earlier, more personalised, joined-up intervention for high-needs cohorts (e.g., vulnerable children/young people; adults experiencing multiple disadvantage; people at risk of homelessness/offending/ill-health), and improves strategic planning by understanding needs and trajectories across systems.

- **What data is being linked/used (high level)?** Build an incremental national data asset on socioeconomic needs and outcomes by linking Data First justice datasets (courts, prisons, probation, family, civil) with cross-government socioeconomic datasets (e.g. HMRC, DfE, DWP, DHSC, DLUHC, HO where lawful and proportionate). Test national-local linkage via a partnership with London Borough of Barking & Dagenham (LBBD), and develop a proof-of-concept using Welsh data via SAIL (and Data First where appropriate).

- **What will the system do (prediction / decision support / LLM assistance)?** Deliver:
    (1) Population and locality estimates of met and unmet needs;
    (2) Life-course / trajectory analysis for cohorts with multiple needs;
    (3) Predictive risk scoring / early warning flags to support secondary prevention;
    (4) NLP/LLM-enabled extraction and summarisation (within secure settings) to identify unmet needs in unstructured data and support evidence-based case triage and policy insight (not automated decision-making).

- **What is the public benefit / intended outcomes?** (BOLD emphasis on outcomes from joined-up data), Improve life outcomes and reduce downstream costs across six “egregious outcomes”:
    **Offending; ill-health & early mortality; in-work poverty; long-term inactivity & unemployment; homelessness & home insecurity; poor child outcomes.**
    The work targets common drivers/risk factors: **poor mental health; poor physical health/activity/nutrition; low income; substance misuse; employment; early years & education; accommodation; family & marital factors.**

- **Key risks & mitigations:** 
    - Information governance & public trust → DPIA/DSAs, Five Safes, transparency, comms plan, strict access controls
    - Linkage error & bias → SPLINK QA, linkage quality reporting, sensitivity analyses, subgroup monitoring
    - Misuse/over-reliance in operational settings → decision-support only, clear guidance, human-in-the-loop, audit trails
    - Data quality & timeliness constraints → data discovery, automated validation, refresh SLAs, iterative delivery (“test and learn”)
    - LLM safety risks → redaction/minimisation, secure processing, grounding/RAG, prompt-injection tests, human review
---

## 1) Scope, outcomes and success criteria
### 1.1 Objective and users
- **Operational/policy objective:** Develop and scale a national needs data asset and national-local linked data products to enable earlier intervention and improved coordination for people with multiple socioeconomic needs; and deliver analytics that help identify cohorts, risks, protective factors and effective intervention points.

- **Primary users / decision points:**
    - Policy teams (MoJ/HMT and OGDs) shaping prevention and commissioning priorities
    - Analysts across MoJ/OGDs/local areas building cohort insight and evaluating interventions
    - Local multi-agency teams/frontline services (where operational products are in scope) for earlier identification, referral and coordinated support

- **AI role:**
    - Decision support / triage / forecasting / insight / summarisation / extraction / RAG — supporting professional judgement, not replacing it.


### 1.2 In-scope / out-of-scope
- In scope:
    - **Project 1 — National data asset** on met & unmet socioeconomic needs and outcomes (iterative build; early “quick wins” using MoJ-held datasets and priority OGDs such as HMRC/DfE as feasible).
    - **Project 2 — National-local products:** pilot linkage with **LBBD** to deliver use-case-driven linked datasets and prototype a “single view” tool concept (frontline decision support) designed for scalability.
    - **Project 3 — Advanced analytics:** early warning flags, predictive risk models, trajectory/pattern analysis, and NLP/LLM extraction from unstructured text (within approved environments).
    - **Discovery (to Aug 2026):** data mapping, data quality assessment, policy landscape, stakeholder mapping, use case definition, IG artefacts (DPIA/DSA), proof-of-concept where feasible (SAIL/Data First).

- **Out of scope: (for this phase unless explicitly agreed)**
    - Fully automated decisions on individuals (e.g., eligibility, enforcement, sentencing, triage decisions without human review).
    - Nationwide operational rollout to all local authorities without a proven pilot, governance model, and evaluated benefits.
    - Any processing outside approved secure settings (TRE/AP/SAIL/ONS SRS as applicable).
    - Clinical diagnosis or replacing health professional judgement.

### 1.3 Success metrics (set upfront)
- **Outcome metrics (BOLD/public benefit):**
    - Improved early identification and engagement with support for target cohorts (measured via agreed proxies)
    - Evidence of improved coordination (fewer repeat contacts/bounces; faster referrals; reduced time to access support)
    - Medium-term signals (where measurable): reduced repeat homelessness, improved treatment uptake, reduced reoffending for targeted cohorts, improved stability indicators

- **Model metrics:** AUC/PR-AUC (classification), MAE/RMSE (regression), calibration (Brier score / reliability), plus confidence intervals; decision thresholds set with operational partners.

- **Data-linkage metrics:** Linkage rate by dataset/time/subgroup; estimated false match / missed match rates (sampled QA); join coverage for key variables.

- **Operational metrics:** Refresh timeliness vs SLA; analyst time saved; tool usability (user testing); latency/throughput where operational prototypes exist.

- **Minimum acceptance criteria(Go/No-Go):**
    - Linkage quality meets pre-agreed thresholds and is stable over time
    - Model adds value over baseline and is well-calibrated for intended use
    - Clear IG position (DPIA/DSAs) and safe-setting controls in place
    - Named customer/owner commits to using outputs and participating in evaluation


### 1.4 Programme context (BOLD Prevention Workstream)
- Established September 2025 to link data across government for prevention.
- Focused on socioeconomic risk factors identified in the **2024 System Challenge K** review.
- The **MoJ-HMT Prevention Report (2025)** highlights rising demand pressures due to socioeconomic needs and the case for earlier, personalised interventions to reduce long-term public spending.
- Builds on evidence that **joined-up interventions can work** (e.g., Sure Start; Supporting Families) but are limited by fragmented data and siloed delivery.


### 1.5 Alignment with government strategic drivers
- Supports senior priorities including:
    - Deputy Prime Minister focus on **youth justice and prevention**
    - Government missions on **health, safety and opportunity**
    - **Changing Futures** and homelessness strategies targeting complex needs
    - **Justice Delivery Plan** ambitions for rehabilitation and improved data sharing
    - **Devolution and Community Empowerment Bill** direction of travel (local control and place-based delivery)


### 1.6 Workstream structure (Projects 1–3)

#### Project 1: National data asset on socioeconomic needs and outcomes
- Iterative linked dataset across England & Wales on needs, key interventions, and outcomes.
- Initial focus on linking available datasets (including those held by MoJ and priority OGDs such as HMRC and DfE, subject to IG).
- Proof-of-concept via **Welsh data (SAIL)** and relevant Data First assets.
- **Deliverables**:
    - Locality-level estimates of met/unmet needs for strategic planning
    - Life-course/trajectory analysis for cohorts (e.g., Changing Futures, cusp of offending/homelessness)
    - Analytical enablement for policy areas (e.g. reoffending; community cohesion)

#### Project 2: Scalable national-local data products
- Partnership with LBBD data & innovation hub to link local residents’ data to national justice data and later to the wider national data asset.
- Deliverables:
    - Linked offender–resident dataset for agreed use cases
    - Prototype “single view” tool concept (household/individual at risk) for earlier, personalised intervention
    - Scalable approach/products built on MoJ analytical platform where feasible to reduce local infrastructure barriers

#### Project 3: Advanced analytics
- Early delivery using accessible data and early asset iterations (e.g., SAIL).
- Includes:
    - NLP/LLM processing to identify unmet needs in free text/case notes not captured in structured data
    - Predictive risk modelling / early warning flags
    - Pattern and trajectory analysis; “impactability” (when/for whom/where interventions work)


### 1.7 Stakeholder engagement (initial set)
- Strong support for national asset and frontline tools. Stakeholders engaged include:
    - Changing Futures programme and analytical teams (MHCLG/DLUHC context)
    - Community Help Partnership team and Evaluation Taskforce (Cabinet Office)
    - Reducing Reoffending policy and analysts (MoJ)
    - London Borough of Barking & Dagenham
    - Joint Combatting Drugs Unit
    - Drug Misuse team (DHSC)
    - Data First and BOLD Programme teams


### 1.8 Provisional timeline (Discovery to be completed by Aug 2026)
#### Project 1 — National needs data
- **Finalise use case and end-product definition**
- **Data mapping across government and local areas; quality/feasibility assessment**
- **Policy landscape of flagship interventions and prevention initiatives**
- **Data sharing agreements and DPIAs**
- **Assess Data First and SAIL datasets; build proof-of-concept where feasible**

#### Project 2 — National-local products
- Identify and prioritise pilot use case(s) for linking LBBD and national justice data
- Define and prototype frontline “single view” use case
- Establish LA consultation group for scalability
- Put in place MoUs/DSAs; assess data quality; deliver proof-of-concept if feasible

#### Project 3 — Advanced analytics
- Identify, prioritise and agree cross-cutting analytical use cases aligned to prevention


### 1.9 Delivery capability and track record (Justice Data / CGD)
- CGD is the delivery arm for the BOLD Partnership; seven strands: BOLD Partnership, Data First, Youth Justice, Turing Internships, Mental Health, AI, Prevention.
- BOLD Partnership (established 2021) reported:
    - 36 completed data linking projects; 22 linked data assets
    - Collaboration with 16 organisations (government and third sector)
    - 19 published reports and 4 awards (including British Data Awards 2024)
    - Example impacts: identifying offenders not attending treatment; linking to support children with incarcerated parents; homelessness prevention insights
- Data First: ADR UK funded, unlocking justice admin datasets for research/policy; secured further investment to scale linkage infrastructure.
- AI Unit: develops software to extract value from underutilised text/unstructured data (e.g., Python package “Laurium”).
- Turing internships: embeds PhD researchers into MoJ to strengthen AI/data science capability.

---



## 2) UK governance and assurance (mandatory artefacts)
> Complete/attach these before moving beyond discovery where personal data or significant risk is present.

### 2.1 Data protection & information governance
- **Is personal data processed?** Yes - during linkage and validation (with minimisation), with outputs primarily **pseudonymised/anonymised** for analysis; any operational outputs require additional controls.

- **Lawful basis & purpose:** Expected to be primarily public task (UK GDPR Art 6(1)(e)) with relevant conditions for special category data (e.g. Art 9(2)(g) substantial public interest / other applicable conditions) and/or **DPA 2018** provisions. Where MoJ acts as a competent authority for law enforcement processing, **Part 3** may apply. Final basis to be confirmed with IG/DPO as part of DPIA and DSAs.

- **DPIA:** To be completed/approved in discovery for each linking activity/work package (Project 1/2/3) - **link: TBC**

- **Data Sharing Agreement / MoU:** Required with each data controller/data owner and for the LBBD pilot - **link: TBC**

- **Security classification & handling:** (personal data) handled in approved secure settings (MoJ Analytical Platform / TRE / SAIL / ONS SRS as applicable), with strict role-based access, logging, and output checking.


### 2.2 Ethical and public benefit assurance
- **Ethics framework self-assessment:** MoJ / HMG Data & AI Ethics Framework (or successor) self-assessment; BOLD public benefit statement - **link: TBC**

- **Public benefit statement:** why linking/AI is necessary and proportionate (BOLD emphasis on “safe, secure and ethical” linking) - Linking is necessary to understand interacting risk factors across systems and to enable proportionate prevention (primary/secondary/tertiary) where single datasets cannot provide a holistic view.

- **Public engagement considerations:** affected groups, transparency commitments, comms plan (if relevant to BOLD-style work) - Transparency and communications plan, especially for any operational tool use; articulate safeguards, minimisation, and benefits - **plan: TBC**


### 2.3 Analytical quality assurance (AQA)
- **AQA approach (AQuA Book):** Follow MoJ AQuA Book proportionate QA; independent peer review at key gates (end of discovery; pre-release of linked data asset; pre-deployment of models/tools).
- **Evaluation approach (Magenta Book) if assessing interventions/outcomes:** Magenta Book-aligned evaluation / benefits realisation plan for pilots and analytical outputs.


### 2.4 Safe access model (Five Safes / TRE)
- **Safe Projects:** purpose, public benefit, approvals - Approved prevention/public benefit case; documented scope and exclusions
- **Safe People:** who can access, training/accreditation - Access only for trained/authorised analysts; named owner(s) and auditable access
- **Safe Data:** minimisation, de-identification, pseudonymisation - Minimisation; pseudonymisation; separation of identifiers; secure linkage processes
- **Safe Settings:** where processing happens (eg TRE/SDE), controls - MoJ Analytical Platform / TRE / SAIL / ONS SRS as appropriate
- **Safe Outputs:** disclosure control/output checking process - Output checking and disclosure controls; operational outputs require stricter governance

---


## 3) Data inventory and acquisition (collection)
### 3.1 Data sources register (initial)

| Dataset | Owner | System of record | Location (example) | Access method | Refresh | Sensitivity / PII | Notes (coverage highlights) |
|---|---|---|---|---|---|---|---|
| Magistrates’ Court defendants (Data First “Dataset 1”) | MoJ | Magistrates’ courts administrative systems | Secure setting / curated tables | SQL | Snapshot | Personal data in source | Jan 2011–Mar 2023; defendant characteristics, offences, disposals |
| Crown Court appearances (Data First “Dataset 2”) | MoJ | Crown Court administrative systems | Secure setting / curated tables | SQL | Snapshot | Personal data in source | Since 2013; defendant characteristics, offences, case outcomes |
| Prison custodial journey (Data First “Dataset 3”) | MoJ / HMPPS | Prison administrative systems (e.g., NOMIS) | Secure setting / curated tables | SQL | Snapshot | Personal data in source | Custody spells, movements within prison system, offender characteristics |
| Family Court cases (Data First “Dataset 4”) | MoJ | Family courts administrative systems | Secure setting / curated tables | SQL | Snapshot | Personal data in source | Jan 2011–Mar 2023; case types, parties involved, outcomes |
| Probation (Data First “Dataset 5”) | MoJ / HMPPS | Probation administrative systems (e.g., nDelius) | Secure setting / curated tables | SQL | Snapshot | Personal data in source | Since 2014; offender characteristics, supervision outcomes |
| Civil Court cases (Data First “Dataset 6”) | MoJ | County courts administrative systems | Secure setting / curated tables | SQL | Snapshot | Personal data in source | Largely complete from 2012; individual actions, outcomes |
| Cross-justice linkage scores / IDs (Data First “Dataset 7”) | MoJ | Data linking outputs | AP tables / linked dataset | SQL | Periodic | Pseudonymised IDs | Probabilistic matching score for individuals across datasets |
| Homelessness ↔ justice linkage (Data First “Dataset 8”) | MoJ + partners | Linked dataset product | Secure setting | SQL | Periodic | Pseudonymised IDs | Links homelessness data with justice datasets to analyse repeat homelessness |
| Continuity-of-care dashboard integration (Data First “Dataset 9”) | MoJ + partners | Integrated operational product | Secure setting | Product / API | TBC | Controlled | Dashboard integrating probation, prison and police data to support continuity of care |
| LBBD residents / service contact data (pilot) | London Borough of Barking & Dagenham (LBBD) | Local authority operational systems | LA secure environment + agreed pathway | Secure transfer / TRE | TBC | Personal data | Used to test national-local linkage and “single view” tool use case |
| Welsh proof-of-concept (SAIL) | SAIL | SAIL TRE | SAIL secure environment | TRE analysis | TBC | Controlled | PoC development and feasibility testing using Welsh data |
| Cross-government socioeconomic datasets (HMRC / DfE / DWP / DHSC / DLUHC / HO) | OGDs | OGD systems | TBC | TBC | TBC | Personal data | Subject to discovery, IG approvals, and feasibility; used to derive socioeconomic risk factors and outcomes |


### 3.2 Collection/extraction plan
- **Ingestion mode:** Discovery phase primarily **batch/snapshot** ingestion. Operational pilots may require tighter refresh cycles subject to feasibility and IG.
- **Incremental logic:** CDC keys / watermarks / late-arriving events policy - Snapshot date / extract date watermarks; idempotent loads; reconciliation against source counts where feasible.
- **Backfill plan:** time range, idempotency, reconciliation checks - Full historical backfills for core datasets in secure settings; late-arriving data captured in subsequent snapshots; clear “as-at” reporting rules.
- **Retention & disposal:** raw/curated/features; deletion triggers; audit trail - Raw identifiers held only where required for linkage; curated and linked pseudonymised layers retained per DSAs; disposal triggers and audit trail documented in runbook.


### 3.3 Minimisation & proportionality (UK standard practice)
- **Minimum necessary fields (discovery baseline):**
    - **Linkage identifiers** (e.g., name elements, DOB, sex, postcode/address tokens where lawful), stable system IDs, and only the variables needed to represent the agreed risk factors/outcomes and evaluate interventions.
    - **Purpose limitation:** Use strictly for prevention/public benefit objectives stated here; prohibit secondary use without re-approval.
    - **Access controls:** Role-based access; least privilege; logging; separation of duties for linkage vs analysis where appropriate.


### 3.4 Data dictionary (minimum viable product (MVP))
- **Entities:** Person, household (where feasible), case, offence, disposal, custody spell, probation episode, service contact/referral, homelessness episode, education record, benefit/employment episode, health contact (as feasible), document/text artefacts.
- **Keys:** Pseudonymised person cluster IDs; case IDs; event IDs; geography codes; time stamps.
- **Time semantics:** Event time vs ingestion time; snapshot dates; “as-at” rules for analysis.
- **Label/target definition (initial modelling candidates):** Examples: risk of homelessness repeat episode within X months; risk of reoffending within X months; risk of escalating service contact; each defined with strict time windows and leakage controls.

---


## 4) Data quality, validation and monitoring
### 4.1 Automated validation tests (define thresholds)
- **Schema:** equired columns/types; enforce enumerations for key categoricals
- **Completeness:** null thresholds for critical linkage variables and core outcomes
- **Uniqueness:** primary key constraints where applicable; dedup rules for repeated events
- **Referential integrity:** FK validity / case ↔ person; event ↔ case; cross-table domain checks
- **Freshness SLA:** expected availability time - agreed per dataset (discovery: “best available”; pilots: explicit SLA)


### 4.2 Observability & drift
- **Data drift:** monitor distribution of key risk factors and outcomes across time
- **Linkage drift:** monitor match rates and join coverage (overall and by subgroup)
- **Label delay & backfill impacts:** how monitored and corrected - track revisions and re-score where necessary


### 4.3 Failure policy
- **Block pipeline if:** critical schema breaks; severe completeness failures; linkage QA fails thresholds
- **Degrade if:** non-critical feeds missing (produce partial outputs with warnings)
- **Incident response:** named on-call owner (TBC), escalation route, comms plan

---


## 5) Pre-processing and manipulation specification
> Must support reproducibility and train/serve parity.

### 5.1 Cleaning rules (explicit)
- Missing values: explicit missingness flags; targeted imputation only where justified; otherwise “unknown”
- Outliers: robust handling (winsorisation/capping) where meaningful; investigate data errors
- Normalisation/scaling: recorded parameters; consistent across train/serve
- Deduplication: deterministic tie-break rules (latest record, best completeness) with audit log
- Text processing: normalise; redact/minimise PII; language detection if needed; store only approved derived features


### 5.2 Transform pipeline (reproducible)
- **Pipeline steps (ordered):**
  1. Ingest raw extracts/snapshots (secure landing)
  2. Standardise identifiers and core fields (names/DOB/postcode tokens, event times)
  3. Validate quality (schema/completeness/consistency)
  4. Deduplicate within each source
  5. Link datasets (deterministic + probabilistic via SPLINK where appropriate)
  6. Create curated “linked” analytical layer + coverage metrics
  7. Feature engineering (time-bounded windows, as-of joins)
  8. Train/test split (time-based) + model development
  9. Publish outputs with disclosure controls

- **Determinism:** fixed seeds; versioned reference data; stable sorting
- **Versioning:** code + config + dataset snapshot identifiers; model registry entry
- **Lineage:** raw → curated → linked → features → train/test → outputs


### 5.3 Leakage controls (especially for linked admin data)
- **Prediction time definition (T0):** defined per use case (e.g., “as at first contact”, “as at release”, “as at start of supervision”).
- **Only use data available before T0:** enforced via time filters and as-of joins; exclude post-outcome data.
- **Post-event variables:** explicit list maintained in feature spec.

---


## 6) Data linking (BOLD core)
### 6.1 Linkage purpose and approach
- **Why link?** (benefit vs risk; why single datasets insufficient) - **Single datasets do not capture interacting risk factors across systems; linkage enables holistic needs assessment**, pathway/trajectory analysis, and evaluation of joined-up interventions.
- **Linkage type:** hybrid deterministic + probabilistic. Use existing Data First linked IDs where available; apply **SPLINK** for probabilistic matching when required.
- **Linkage unit:** person (primary), plus household/location where feasible and lawful for prevention use cases.


### 6.2 Match keys and rules
- **Primary match keys (illustrative; subject to IG):** name elements, DOB, sex, postcode/address tokens; stable system IDs when available.
- **Secondary/fallback keys:** partial DOB, phonetic name tokens, historical postcodes, etc.
- **Standardisation rules before matching:** consistent casing, trimming, de-punctuation, DOB formatting, postcode normalisation, alias handling.
- **Blocking strategy (if probabilistic):** block on coarse attributes (e.g., year of birth + postcode district + initial) to reduce comparisons; tune per dataset.


### 6.3 Linkage quality and error measurement
- **Linkage rate targets:** set per dataset and use case during discovery (with realistic ceilings).
- **False match / missed match estimation:** sampled QA with clerical review where permitted; comparison to known links; sensitivity analysis of thresholds.
- **Clerical review (if any):** process + audit trail
- **Sensitivity analysis:** quantify effect of linkage uncertainty on key metrics and model outputs.


### 6.4 Join semantics (downstream features)
- **Join types:** default left joins from core cohort tables; inner joins only where analytically justified.
- **Temporal joins:** as-of joins with defined windows; late data captured on refresh.
- **Coverage monitoring:** join coverage by time, geography, and subgroup to detect bias.

---


## 7) Predictive modelling specification (non-LLM)
### 7.1 Modelling task and baselines
- Task: classification (risk flags), regression (need intensity), survival/time-to-event, clustering/cohort discovery, forecasting.
- Baseline: transparent GLM / simple scoring heuristic using a small set of predictors.
- Candidate models: gradient-boosted trees; survival models; hierarchical models; calibrated logistic regression; where appropriate, interpretable ML methods.
- Constraints: explainability, fairness, operational usability, calibration, and proportionate performance, operational usability.


### 7.2 Evaluation design (AQA-ready)
- **Split strategy:** time-based / grouped / stratified; time-based splits aligned to operational reality; group splits where repeated individuals exist.
- **Primary metrics:** PR-AUC/AUC; calibration; Brier; recall at fixed precision for triage use cases.
- **Uncertainty:** bootstrapped confidence intervals; sensitivity to linkage thresholds.
- **Subgroup performance:** monitor by legally/ethically appropriate groupings; document proxy risks.
- **Calibration:** reliability curves; decision thresholds, reliability plots; threshold selection with service partners.


### 7.3 Deployment and monitoring
- Batch vs online: Batch scoring first; operational near-real-time only where justified.
- Monitoring: performance drift, data drift, linkage drift, data quality, latency
- Rollback/kill switch: documented in runbook.
- Documentation: model card, decision record, and user guidance / runbook.

---


## 8) LLM specification (LLMs + RAG + safety)
### 8.1 Use cases and boundaries
- Use cases: extraction / summarisation / triage notes / Q&A / drafting / decision support, identify unmet needs in free text; summarise case notes for analysts; extract structured indicators from documents; evidence Q&A grounded in approved corpora.
- **What the LLM must never do:** make final decisions about individuals; reveal personal data; provide ungrounded assertions without citations; infer sensitive attributes without lawful basis.


### 8.2 Data handling for LLMs (UK IG controls)
- **Inputs:** which fields/docs; redaction rules; PII minimisation, minimised/redacted text only; derived features preferred over raw text.
- **Where processing occurs:** only in approved secure environments; no external vendor processing unless explicitly assured/contracted and approved.
- **Logging & retention:** store prompts/outputs only as needed for audit; access controlled; retention per DPIA.
- **Prompt injection & data exfiltration risks:** adversarial testing; strict system prompts; retrieval filtering; output constraints.


### 8.3 RAG design (if used)
- Corpus definition + versioned policy/evidence docs and approved internal guidance.
- Chunking strategy
- Embedding model + vector index + refresh cadence
- Retrieval: top-k, hybrid + filters; reranking where available.
- Grounding: citations required, answer constraints, “I don’t know” policy enabled.
- Evaluation: retrieval recall@k, groundedness/faithfulness rubric, adversarial tests; red-team tests.


### 8.4 Fine-tuning (if used)
- Only if justified; training data de-identified; privacy screening; strong holdout sets.
- Training data spec: sources, sampling, de-duplication, labelling
- Safety filters: disallowed content, privacy screening
- Overfitting controls: holdout sets, topic diversity, regression tests


### 8.5 LLM evaluation & assurance
- Human review with rubric; inter-rater agreement; bias/toxicity/privacy leakage testing; clear release criteria.
- Offline eval set: representative + edge cases
- Human review: rubric + inter-rater agreement
- Harm testing: bias, toxicity, privacy leakage, hallucination
- Release criteria: go/no-go thresholds + sign-off

---


## 9) Implementation: pipelines, environments, and controls
### 9.1 Pipelines (reproducible, auditable)
- Ingestion: scheduled batch loads with retries and reconciliation checks.
- Linking: SPLINK pipelines with versioned configs and linkage QA reporting.
- Feature build: curated linked tables (and/or feature store pattern where available).
- Training: orchestration + experiment tracking; reproducible training runs.
- Inference: batch scoring initially; governed access for operational prototypes.


### 9.2 Secure environments and access
- Dev/stage/prod separation where applicable.
- Secrets management and access logging.
- Output checking/disclosure controls (aligned to Five Safes: Safe Outputs)


### 9.3 Cost and sustainability
- Compute budget and refresh cadence aligned to use case.
- Avoid over-engineering early; iterate with “test and learn
- Data refresh cadence vs need
- Technical debt log and maintenance ownership.

---


## 10) Risks, assumptions, and open questions
### 10.1 Key risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner | Review date |
|---|---:|---:|---|---|---|
| IG approvals / DSAs delay delivery | M | H | Start DPIA/DSA early; define clear use cases and proportionality; phased “test and learn” delivery; use existing TRE assets (Data First/SAIL) for proof-of-concept while approvals progress | Policy + IG (TBC) | Monthly |
| Linkage error leading to bias/harms | M | H | Linkage QA (clerical review/sampled validation where permitted); threshold sensitivity analysis; subgroup coverage monitoring; independent peer review at key gates | Data linking lead (TBC) | Monthly |
| Public trust / transparency issues | M | H | Clear public benefit statement; minimisation; communications and engagement plan; explain safeguards and limits; local partner/stakeholder engagement | Comms/Policy (TBC) | Quarterly |
| Misuse or over-reliance on risk scores in frontline settings | M | H | Decision-support only; documented decision thresholds and intended use; user training; human-in-the-loop controls; audit trails; access restrictions; evaluate operational impacts | Product/Policy (TBC) | Quarterly |
| Data quality / missingness undermines models and insight | H | M | Data discovery and profiling; automated validation tests; agreed minimum data standards; prioritise robust variables; data quality reporting and remediation backlog | Data engineering (TBC) | Monthly |
| LLM privacy leakage / hallucination / unsafe outputs | M | H | Redaction/minimisation; secure processing only; RAG grounding with citations; prompt-injection testing; human review gates; release criteria; monitoring and incident process | AI lead (TBC) | Monthly |


### 10.2 Assumptions (with validation)
- Cross-government datasets can be accessed for prevention purposes under appropriate lawful basis → validate via IG engagement and DSAs during discovery.
- Data First and SAIL assets are sufficient to demonstrate PoC value → validate with rapid scoping analysis.
- Local partner (LBBD) can support timely data extraction and secure linkage → validate with MoU, technical feasibility, and pilot plan.
- Users can define actionable use cases and success measures → validate via discovery workshops and user research.


### 10.3 Open questions
- Confirm named SRO, delivery lead(s), and product ownership model (including cross-government co-ownership where appropriate).
- Which OGD datasets are highest priority for “quick wins” and legally feasible first (HMRC/DfE/DWP/DHSC/DLUHC)?
- Agree the first operational pilot use case(s) with LBBD and define governance for any frontline tool.
- Define evaluation design for pilots and what “value” looks like for each partner (benefits realisation).

---


## 11) Deliverables and sign-off
### 11.1 Deliverables checklist
- [ ] Data source register + dictionary (versioned)
- [ ] DPIA completed/approved (per project component where required)
- [ ] Data sharing agreement/MoU in place (per dataset/pilot)
- [ ] Five Safes assessment recorded
- [ ] Linkage method + linkage quality report (incl. subgroup coverage)
- [ ] Reproducible pipelines + automated data tests
- [ ] Model/LLM evaluation report + monitoring plan
- [ ] AQA sign-off recorded
- [ ] Runbook + incident process + user guidance


### 11.2 Sign-off table

| Area | Approver | Date | Notes |
|---|---|---|---|
| Product / policy | SRO (TBC) | TBC | Prevention workstream priorities confirmed |
| Data owner(s) | Each data controller / data owner | TBC | DSAs agreed; purpose limitation and retention confirmed |
| Information governance / DPO | MoJ Information Assurance / DPO (TBC) | TBC | DPIA approved; IG risks/actions logged and tracked |
| Security | MoJ Security / Platform Security (TBC) | TBC | Secure setting, access controls, logging and output checking confirmed |
| Lead analyst (AQA) | G6/G7 analytical lead (TBC) | TBC | AQA checks complete; methodology and outputs signed off |
| Technical lead | Data/engineering/tech lead (TBC) | TBC | Pipelines, monitoring, documentation and runbook in place |

---


## Annex: Prevention project summary (reference: *20250415 Prevention Report formated final (002).pdf*)

### The prevention project
- The document outlines a prevention project aimed at transforming data use across agencies to personalize services, manage socioeconomic risks, and improve the lives of vulnerable populations in society.

### The Prevention Project Overview
- The Prevention Project aims to leverage data across agencies to personalize services, manage socio-economic risks, and improve the lives of vulnerable citizens.
- Sponsored by the Ministry of Justice and HM Treasury.
- Focuses on addressing key risk factors like poverty, housing insecurity, and poor health.
- Aims to improve public service efficiency and reduce costs associated with socio-economic risks.
- Highlights the need for multi-agency collaboration and data sharing to provide holistic support.

### Key Risk Factors Affecting Quality of Life
- Socio-economic risks significantly impact individuals' quality of life and public service demand.
- Key risks include poverty, housing insecurity, low educational attainment, and poor health.
- Individuals facing multiple risks often incur 4-5 times higher public service costs.
- Poor outcomes lead to instability and anti-social behavior, affecting broader society.
- Evidence shows that combined interventions yield better long-term results than isolated efforts.

### Barriers to Effective Data Sharing
- Current data management practices hinder effective prevention and service delivery.
- Public agencies operate in silos, focusing on their own client groups.
- Data is rarely integrated across agencies, leading to incomplete information for caseworkers.
- Caseworkers often spend excessive time gathering data from multiple sources.
- Cultural, legal, and bureaucratic barriers impede effective data-sharing initiatives.

### Successful Local Data-Sharing Initiatives
- Innovative local projects demonstrate the potential of data-sharing to enhance service delivery.
- Sunderland uses Child View for youth justice management.
- Leeds Office of Data Analytics integrates case management and service assessments.
- Barking and Dagenham's OneView Tool enables secure identification of at-risk individuals.
- Thames Valley Together facilitates collaboration across various local services.

### Recommendations for Improved Data Use
- The report outlines several recommendations to enhance data sharing and prevention efforts.
- Expand data-sharing initiatives using a test-and-learn approach.
- Prioritise data-sharing for adults with severe multiple disadvantages.
- Establish a Central Prevention Data Office to oversee data-led prevention work.
- Invest in capacity building for assessing risks across systems.
- Develop communication strategies to address privacy concerns and promote data-sharing benefits.

### Trends in Socio-Economic Risks and Outcomes
- The prevalence of socio-economic risks has increased, straining public services and finances.
- 40% increase in economic inactivity due to long-term sickness over the past decade.
- 62% rise in young people with probable mental health conditions in five years.
- 61% increase in rough sleeping estimates over the last decade.
- Child poverty remains stable at 30% among children after housing costs.

### Rising Mental Health Concerns
- Mental health issues are increasingly prevalent among both adults and children.
- 20.3% of children aged 8-16 have a probable mental disorder, up from 12.5% in 2017.
- The incidence of Common Mental Disorder in adults rose from 55.9 to 76.9 per 1,000 persons from 2000 to 2020.
- Health inequalities persist, particularly in deprived areas, affecting overall well-being.

### Understanding Severe and Multiple Disadvantage
- Severe and Multiple Disadvantage (SMD) refers to the complex interplay of socio-economic risk factors affecting vulnerable populations.
- SMD affects adults involved in offending, substance misuse, or homelessness.
- In 2015, an estimated 584,000 people in England were in contact with services addressing these issues.
- Over 250,000 individuals faced at least two of the three outcomes (homelessness, substance misuse, offending).
- Approximately 58,000 people experienced all three outcomes.
- Key risk factors include universal poverty, poor mental health, childhood trauma, and domestic abuse for women.
- SMD individuals often have estranged relationships with children, exposing them to additional risks.

### System Challenge Findings on Socio-Economic Risks
- A review in 2024 identified overlapping socio-economic risk factors driving negative outcomes.
- Education and poor early years experiences were the most prominent risk factors.
- Family and marital factors, along with low income and poverty, were also significant.
- The government lacks a strong understanding of how multiple risk factors interact to drive negative life outcomes.
- There is a need for improved data and analytical capacity to address these challenges.

### Economic Activity and Associated Risks
- Low income and unemployment are significant risk factors linked to various negative outcomes.
- Children from low-income households are more likely to have poor health and lower educational outcomes.
- Families with disabled members face higher poverty rates (25% vs. 18% for non-disabled families).
- In 2021-22, 31% of disabled individuals lived in poverty, rising to 38% for those with long-term mental health conditions.

### Young People at Risk of Negative Outcomes
- High prevalence of risk factors exists among children involved in the justice system and those in care.
- 80% of cautioned or sentenced children had special educational needs.
- 69% were eligible for free school meals, and 32% were assessed as children in need.
- Children with multiple socio-economic risks received harsher sentences, with 40% of custodial sentences involving over 15 concerns.

### Family Stability and Its Impact
- Adverse childhood experiences are strong predictors of poor adult outcomes.
- The Dunedin Study found that more adversity in childhood correlates with poorer adult health and social outcomes.
- Young people in violent relationships often come from backgrounds of lower educational attainment and early educational disengagement.

### Homelessness and Associated Vulnerabilities
- Homeless individuals typically face multiple vulnerabilities and risk factors.
- 96% of homeless individuals have at least one additional vulnerability.
- 82% report mental health issues, and 60% have substance misuse concerns.
- Negative educational experiences, such as truancy and exclusion, are common among those who have slept rough.

### Health Risks Linked to Socio-Economic Factors
- Poor mental health is prevalent among various vulnerable groups, including those with SMD and the homeless.
- Low income is strongly associated with poor physical health outcomes.
- Individuals experiencing economic inactivity and homelessness are more likely to have poor health.

### Rising Demand for Acute Services
- Demand for public services is increasing due to rising socio-economic risks.
- Since 2019, there has been a 21% increase in demand for local authority housing services.
- The number of children looked after has risen by over 75% since 1994, reaching 83,630 in 2024.
- Mental health service access for children and young people increased by 27% from 2021 to 2024.

### High Costs of Acute Services
- Acute services are becoming increasingly expensive, with a shift in spending priorities.
- Spending on homelessness services has doubled over the last decade, averaging £15,350 per individual with multiple risk factors.
- The cost for looked-after children is approximately £190,000 per child with acute needs, compared to £490 for universal support.

### Importance of Early Intervention
- Investing in early intervention can significantly reduce future demand for acute services.
- The Heckman Curve suggests that early investments yield high economic returns.
- Late intervention costs in England were estimated at £16.6 billion in 2016, with significant costs associated with looked-after children and domestic violence.

### Evidence on Effective Early Interventions
- Research supports the efficacy of early interventions in improving outcomes.
- The Sure Start program significantly reduced serious offending and hospitalizations while improving educational outcomes.
- For every pound spent on Sure Start, approximately 19 pence was saved in public spending on youth justice and children’s services.

### Data Sharing Barriers and Initiatives
- Data-sharing across agencies is crucial for effective intervention but faces significant barriers.
- Fragmented data systems hinder the understanding of socio-economic risks.
- Successful initiatives exist, such as the Intelligence Driven Integrated Offender Management tool, but many lack comprehensive data-sharing frameworks.

### Recommendations for Improved Data Sharing
- A national-local partnership is needed to enhance data-sharing for prevention.
- Establish a Central Prevention Data Office to facilitate data pooling and sharing.
- Develop a framework for joint governance and standard data definitions to improve comparability and support multi-agency interventions.

### Economic Risks and Data Sharing Initiatives
- The text discusses the potential of linking local operational data with national datasets to better understand socio-economic risks and improve public services.
- The Integrated Data Service (IDS) has faced challenges in development, emphasizing the need for clear use cases and simplified legal procedures for data access.
- The National Data Library (NDL) aims to provide ethical access to government data for researchers and businesses, enhancing economic growth and public service quality.
- Smaller programs like the Better Outcomes through Linked Data (BOLD) have shown that targeted data-sharing can yield significant benefits, with £21.8 million invested resulting in 31 data linking projects and 22 linked data assets.
- BOLD has successfully linked datasets to identify adults at risk of multiple disadvantages, demonstrating the potential for effective interventions.

### Test-and-Learn Approach for Data-Enabled Prevention
- The text advocates for local trailblazers to test national-local data-sharing across public services to improve outcomes for individuals at risk.
- Local area 'trailblazers' can demonstrate the value of data-sharing and optimize frontline tools for better service delivery.
- The complexity of data-sharing across agencies presents challenges, but smaller initiatives can provide valuable insights and quick wins.
- A test-and-learn approach allows for user testing and evaluation, ensuring that local agencies are engaged in the design and implementation of linked data tools.

### Building Public Trust in Data Sharing
- The text highlights the importance of public trust in data-sharing initiatives and the need for transparency regarding data use.
- Public support for data-sharing exists if the benefits are clear and safeguards are in place.
- Government must communicate how personal data will be used and the positive outcomes expected from data-sharing initiatives.
- A proactive communication strategy is essential to articulate the benefits and risks associated with data-sharing.

### Recommendations for Improving Data Sharing
- The text outlines several recommendations to enhance data-sharing and improve public service delivery.
- Government should expand data-sharing initiatives using a test-and-learn approach to demonstrate value and facilitate rapid scaling.
- Prioritize data-sharing for adults with severe multiple disadvantages, as they represent a high service demand cohort.
- Establish a Central Prevention Data Office to oversee data-led prevention work and ensure high-quality linked data is available for operational use.
- Invest in building capacity for assessing risks across systems to improve intervention effectiveness and sustainability.

### Business Case for Prevention Data Tool
- The text presents a business case for developing a data tool to identify adults at risk of severe and multiple disadvantages.
- The project aims to create linked data and a digital tool for frontline practitioners to enable early intervention.
- Estimated costs for the project range from £4.7 million to £5.7 million over four years, with a discovery phase costing £1.2 million in the first year.
- The tool is expected to improve data efficiency, targeting of interventions, and user experiences, ultimately reducing demand for acute services.
- Successful implementation could lead to significant savings, with only a small change needed in offending or homelessness to recover the investment.
<!-- END FILE: SPEC.md -->

---

<!-- BEGIN FILE: Annex_DataFirst_dataset_mapping_to_prevention_outcomes_and_drivers.md -->
# Annex: Data First dataset mapping to prevention outcomes & drivers (BOLD Prevention)

**Purpose.** This annex summarises how the Ministry of Justice (MoJ) **Data First** datasets can be used as the foundational national justice data asset for the BOLD Prevention workstream, and how they map to:

- the **six “egregious” social outcomes** used to frame System Challenge K, and  
- the **cross‑cutting socioeconomic drivers / risk factors** (needs) that drive demand across public services.

It is designed to be appended to `SPEC.md` and used during **Step A** of delivery (establishing a repeatable “Use case → Data → Linkage” pipeline), including creation of a **risk factor register** and an incremental data-linking plan.

---

## A1. What Data First provides (and why it matters for prevention)

### A1.1 Data First cross‑justice datasets (England & Wales)

Data First provides seven core justice datasets plus a cross‑justice linking dataset that enables person‑level linkage across them.

**Core datasets (7):**
- **Magistrates’ courts (defendant‑level)**
- **Crown Court (defendant‑level)**
- **Prisoner custodial journeys**
- **Probation (nDelius)**
- **Offender assessments (OASys)**
- **Family court (FamilyMan)**
- **Civil court (possession) (CaseMan / PCOL)**

**Linkage assets:**
- **Cross‑Justice System (XJS) linking dataset**: person‑level linkage across the seven datasets (via an estimated person ID)
- **Mags ↔ Crown “journey” table**: case‑level linkage for criminal court pathways

> Practical takeaway: for BOLD Prevention, Data First gives a **national, person‑level justice spine** for cohort identification, life‑course / trajectory analysis, and downstream outcomes (e.g., offending, court progression, probation, custody).

### A1.2 MoJ–DfE data share (England)

Separately, the **MoJ–DfE data share** links **criminal history data (PNC)** to education and children’s social care in the **National Pupil Database (NPD)**. This is critical for **early years / child outcomes** and upstream prevention targeting.

---

## A2. Mapping: six social outcomes → Data First datasets

Below is a practical mapping for where each outcome is measured (directly) vs. where Data First provides only partial proxies (requiring enrichment linkage).

### Offending (MoJ / HO)
**Primary measurement in Data First**
- Magistrates’ court dataset (offences, outcomes, disposals)
- Crown Court dataset (indictable outcomes, sentencing)
- Probation dataset (community orders, requirements, supervision events)
- Prison custodial journeys (custody spells, releases)
- Cross‑justice linking dataset (journeys and repeat contact)

**Prevention use**
- Primary: place‑based demand forecasting, cohort profiling  
- Secondary: early warning flags for escalation (e.g., increasing court contact frequency)  
- Tertiary: recurrence/reoffending trajectories and “impactability” by cohort/place

### Ill‑health and early mortality (DHSC)
**What Data First can do now**
- OASys includes **mental and physical health need proxies** (assessment‑based), plus indicators such as healthcare requirement.

**What typically needs linkage**
- NHS service use (primary care, hospital episodes, mental health services)
- ONS mortality registrations

### In‑work poverty (DWP)
**What Data First can do now**
- OASys includes **income source / benefits and finance** indicators
- Family court includes **fee exemption** (administrative proxy)
- Civil possession includes **rent/arrears** trajectory indicators (financial strain)

**What typically needs linkage**
- DWP benefits and employment support
- HMRC earnings (PAYE/RTI) to measure in‑work poverty robustly

### Long‑term inactivity and unemployment (DWP)
**What Data First can do now**
- OASys includes employment status, unemployment duration proxies, and employment‑related needs/commitments

**What typically needs linkage**
- DWP employment spell data and benefit history
- Education / skills datasets for long‑term pathways

### Homelessness and home insecurity (DLUHC)
**Primary measurement in Data First**
- Civil court possession dataset (claims → orders → warrants → possession gained)
- OASys accommodation needs (e.g., suitability, stability)

**What typically needs linkage**
- DLUHC homelessness case‑level systems
- Local authority housing, temporary accommodation, supported housing

### Poor child outcomes (DfE)
**Primary measurement in Data First**
- Family court (public/private law case types; harm alleged; number of children)
- MoJ–DfE (PNC ↔ NPD/CSC) for: attendance, attainment, exclusions, SEND, CSC involvement

---

## A3. Mapping: socioeconomic drivers / needs → Data First measures

System Challenge K identified common overlapping drivers:
**poor mental health; poor physical health/activity/nutrition; low income; substance misuse; employment; early years and education; accommodation; and family and marital.**

Data First contributes to these drivers via (a) rich assessed needs in OASys, and (b) administrative “events” in civil/family courts that act as real‑world escalation signals.

### A3.1 Driver-by-driver mapping (summary)

| Driver / risk factor | Strongest Data First source(s) | Typical “signals” available now | Key enrichments to plan next |
|---|---|---|---|
| Poor mental health | **OASys** | current psychological problems, psychiatric treatment, self-harm proxy | NHS MH services; GP/hospital; mortality |
| Poor physical health / disability / nutrition | **OASys** | chronic health indicators, disability impacts, healthcare requirement | NHS clinical data; DWP disability benefits |
| Low income | **OASys**, **Family**, **Civil possession** | benefits / income source; fee exempt; rent/arrears | DWP benefits; HMRC earnings; local welfare |
| Substance misuse | **OASys** | drug/alcohol misuse indicators; treatment proxy | NDTMS; NHS |
| Employment | **OASys** | unemployment proxy, employment support needs | DWP employment; HMRC PAYE; skills datasets |
| Early years & education | **MoJ–DfE**, **OASys** | NPD/CSC modules; basic skills proxies | early help; health visiting; LA data |
| Accommodation | **Civil possession**, **OASys** | possession process; accommodation suitability/instability | DLUHC homelessness; LA housing |
| Family & marital | **Family court**, **OASys** | harm alleged; children involved; relationship problems | domestic abuse data; CSC; local services |

> The detailed, field-level version of this mapping is captured in the **Step A risk factor register** (CSV) produced alongside this annex.

---

## A4. Step A implementation guidance: how to use Data First catalogues & synthetic data

### A4.1 Use the Data First catalogues as your “variable discovery backbone”
For each driver, use keyword-based discovery against the ODS catalogues to identify:
- **candidate indicators** (single variables),
- **feature sets** (groups of variables),
- **event sequences** (e.g., possession claim → warrant → possession gained).

Recommended workflow:
1. Start with a *use case question* (e.g., “identify early housing insecurity risk for adults with multiple disadvantages”).
2. Translate to *drivers* (accommodation, low income, substance misuse, mental health).
3. Translate drivers to *measures* (specific variables or derived features).
4. Record in the **risk factor register** (variable name, dataset, coverage, limitations).
5. Confirm linkage feasibility using the **XJS linking dataset** keys and linkage-quality flags.

### A4.2 Use synthetic datasets for rapid prototyping
Data First publishes low‑fidelity synthetic datasets that mirror the structure of the real datasets. Use these to:
- draft feature engineering logic,
- build reproducible pipelines,
- test cohort definitions and linkage code,
- estimate compute requirements and runtime.

### A4.3 Linkage quality implications (design into Step A)
- Criminal justice datasets (mags/crown/prison/probation/oasys) generally have **stronger identifiers** and linkage quality.
- Family and civil court datasets are **less well‑populated** for identifiers, reducing linkage quality and increasing missingness risk.

Design implications:
- Prefer *within‑justice* linkage first for quick wins and stable coverage.
- Treat family/civil linkage as **higher uncertainty**: use match flags/thresholds; validate with sensitivity analysis; consider aggregate or case-level outputs where person-level linkage is weak.

---

## A5. Recommended incremental linkage plan for BOLD Prevention

### Wave 0 (quick wins): within Data First
**Goal:** Create a national justice spine + needs proxies.

- Join the seven datasets via **XJS estimated person ID**
- Build stable cohort definitions (e.g., Changing Futures-like overlap proxies using OASys needs + justice contact)
- Add place-based context by attaching IMD and local indicators using **LSOA/LA codes**

**Outputs:** cohort profiles; baseline trajectories; “risk factor register” validated against real structure (synthetic first).

### Wave 1: add child outcomes and early-life drivers (MoJ–DfE)
**Goal:** enable upstream targeting for vulnerable young people, and intergenerational risk analysis.

- Link to NPD/CSC modules: attendance, attainment, exclusions, SEND, CIN/CP/LAC where approved

### Wave 2: add income, employment and health for robust prevention modelling
**Goal:** replace proxies with gold-standard measures.

- DWP benefits and employment spell history; HMRC earnings
- DHSC/NHS service use; ONS mortality

### Wave 3: national–local linking pilots (e.g., LBBD)
**Goal:** enable frontline “single view” tools, and local early warning interventions.

- Link to local authority resident/household data for early help, housing, public health, and service contacts
- Expand to other local areas via scalable patterns and standardised governance artefacts

---

## A6. Outputs for Step A (this annex + register)

- **Annex (this document):** Data First dataset mapping to prevention outcomes & drivers  
- **Risk factor register (CSV):** structured list of drivers → measures → candidate datasets and linkage needs

**Local catalogue files referenced in this project workspace**
- `ONS_mags_gov_uk_v2.ods` (magistrates)
- `ONS_CR_1.ODS` (Crown Court)
- `ONS_prison_gov_uk_v2.ods` (prison)
- `ONS_PR_1.ODS` (probation)
- `OASys_ONS_data_catalogue_NOV25_External.ods` (offender assessment / OASys)
- `ONS_family_gov_uk_v1.ods` (family court)
- `ONS_civil_gov_uk_v1.ods` (civil court / possession)
- `ONS_linking_gov_uk_v1.ods` (cross‑justice system linking)

---

## A7. Reference links (for embedding into the SPEC)

```text
GOV.UK: Ministry of Justice – Data First (datasets, catalogues, synthetic data, access routes)
https://www.gov.uk/guidance/ministry-of-justice-data-first#data-first-datasets
```
<!-- END FILE: Annex_DataFirst_dataset_mapping_to_prevention_outcomes_and_drivers.md -->

---

<!-- BEGIN FILE: data_first.md -->
# Data First

## refs: 
https://www.gov.uk/guidance/ministry-of-justice-data-first

https://assets.publishing.service.gov.uk/media/683863d5c99c4f37ab4e867c/Data_First_User_Guide_Version_8.2.pdf

https://assets.publishing.service.gov.uk/media/68f2032028f6872f1663efb8/MoJ_DfE_data_privacy_notice__002_.pdf

https://www.adruk.org/our-work/browse-all-projects/data-first-harnessing-the-potential-of-linked-administrative-data-for-the-justice-system-169/

https://saildatabank.com/

https://www.gov.uk/government/publications/ministry-of-justice-areas-of-research-interest-2020


1) Where Data First sits in BOLD Prevention (and where to access it)

Data First is a ready-made “justice spine” to start mapping socioeconomic risk factors for prevention, because it already links person-level records across seven justice datasets and provides a cross-justice linking dataset to join them up.

Access routes (and what’s available where):

    - ONS Secure Research Service (SRS) and SAIL Databank host the cross-justice datasets.

    - The separate MoJ-DfE data share (PNC ↔ National Pupil Database) is ONS SRS-only.
        
    - Data catalogues (ODS files) exist for each dataset and are the fastest way to find variables for risk-factor register.

    - Synthetic datasets exist for prototyping pipelines and feature engineering before secure access is in place.

Important constraint: Data First datasets are designed for research and evidence building, not operational decision-making (helpful for model development + evaluation, but your frontline tool will need a separate operational data route and IG).


2) Using Data First to cover the six social outcomes

Below is “which Data First dataset(s) help, and what they give us” for each outcome.

    - Offending (MoJ/HO)
        - Use: Magistrates’ courts + Crown Court + Probation + Prisoner cuts
        - Gives you: end-to-end justice journeys (charges/cases → outcomes/sentences → custody episodes → supervision/requirements → assessed needs/risks).

    - Ill-health and early mortality (DHSC)
        - Use (within Data First): OASys has assessed indicators for mental health / some physical health/disability and related flags.
        - Gap: true “ill-health & early mortality” outcomes require health datasets (NHS / mortality) via agreed external linkage in SRS/SAIL. The user guide explicitly anticipates external linked data “where agreed”.

    - In-work poverty (DWP)
    Use (within Data First):
        - OASys finance/income section variables (income source, money management issues, benefits flags).
        Civil court can give housing cost pressure signals (e.g., rent/arrears/possession).
        - Gap: actual earnings/benefits require DWP/HMRC linkage.

    - Long-term inactivity and unemployment (DWP)
        - Use (within Data First): OASys education/training/employment variables (employment status, employability barriers, skills).
        - Gap: sustained labour market status best comes from DWP/HMRC.

    - Homelessness and home insecurity (DLUHC)
        - Use (within Data First):
            - Civil court possession claims / warrants (strong “home insecurity” signal).
            - OASys accommodation section flags + address-based geography for instability proxies
            - Gap: statutory homelessness / support usage needs DLUHC + local authority datasets.

    - Poor child outcomes (DfE)
        - Use (within Data First):
        - MoJ-DfE data share: PNC linked to NPD (education + social care) for England.
        - Family court dataset: children involved, harm alleged, divorce/child proceedings signals.


3) Where the drivers / socioeconomic risk factors live in Data First

Driver set: poor mental health; poor physical health/activity/nutrition; low income; substance misuse; employment; early years and education; accommodation; family and marital. 

    - Key insight
        - OASys (offender assessments) is the richest single source for “socioeconomic needs” inside Data First, because it explicitly records needs/barriers across accommodation, ETE (education/training/employment), finance, relationships, emotional wellbeing, substance misuse, etc.
        - Civil and family court data then add structural risk signals (possession claims, fee exemption, harm alleged, children involved), and the courts/custody/probation datasets give the journey + timing context.


4) A practical “how-to” workflow: build the risk factor register using Data First catalogues + MoJ data discovery

This is a discovery/alpha-friendly approach that matches your spec’s need for iterative delivery and quick wins. 


### Step A — “risk factor register” (canonical list)
- risk factor register sheet/table with:
    - Risk factor → definition (operational) → preferred measure → fallback proxy measure → dataset candidate(s) → notes on bias/missingness.

### Step B — Use Data First data catalogues to populate candidate variables

- From the Data First GOV.UK page, use the ODS catalogues (one per dataset) and:

    - Search within each catalogue for your driver keywords (e.g., “accommodation”, “employment”, “benefit”, “drug”, “alcohol”, “depression”, “domestic abuse”, “children”, “rent”, “possession”).

- For each candidate variable, capture:

    - table name, variable name, definition, value set, time coverage, and expected missingness.

### Step C — Decide “justice spine join strategy” early

- Use the *cross-jus to join the seven datasets at person-level (and magistrates ↔ Crown case-level where needed).
- Also plan for linkage quality: family/civil have weaker identifiers than criminal justice datasets, so linkage-bias assessment must be explicit (especially for equalities).

### Step D — Use the MoJ data discovery tool to find non-justice risk factor sources (for the gaps)

- For each driver where Data First is “proxy only”, use discovery tooling to identify:

    - dataset owner + legal gateway + refresh cadence
    - geographic granularity + person identifiers available for linkage
    - known quality issues and representativeness constraints

Then prioritise “linkage waves” (see section 6).

### Step E — Prototype quickly using synthetic datasets

- Use synthetic Data First datasets for:
    - pipeline scaffolding, feature engineering patterns, joining logic, and disclosure-safe aggregate outputs.


| Driver / risk factor                            | Best Data First dataset(s) to start                          | What you typically extract                                                                                                                                                           | Main gaps (what to link next)                                                               |
| ----------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------- |
| **Poor mental health**                          | **OASys** ([GOV.UK][1])                                      | Flags for psychological problems, self-harm/suicidality, psychiatric treatment/medication; plus related risk/need scores                                                             | Clinical diagnosis + service use + outcomes (NHS MH services, HES, mortality) ([GOV.UK][2]) |
| **Poor physical health / activity / nutrition** | **OASys** ([GOV.UK][1])                                      | Disability/chronic health problem flags; learning disability screening; limitations affecting suitability for interventions                                                          | BMI/obesity, primary care, hospital, mortality (DHSC/NHS) ([GOV.UK][2])                     |
| **Low income / poverty**                        | **OASys** + **Family court** + **Civil court** ([GOV.UK][1]) | OASys income source + benefits indicators + money management problems; family court fee exemption proxy; civil rent/arrears/possession signals                                       | Earnings + benefit receipt at scale (HMRC/DWP) ([GOV.UK][2])                                |
| **Substance misuse**                            | **OASys** ([GOV.UK][1])                                      | Drug misuse history/current flags; alcohol misuse; whether alcohol/drugs were disinhibitors at offence; treatment engagement indicators                                              | Treatment service data (NDTMS / local treatment) + health comorbidity (DHSC) ([GOV.UK][2])  |
| **Employment**                                  | **OASys** ([GOV.UK][1])                                      | Employment status, employability barriers, skills/training needs, planned employment status                                                                                          | DWP employment status + HMRC PAYE/RTI for sustained outcomes ([GOV.UK][2])                  |
| **Early years & education**                     | **MoJ-DfE (PNC↔NPD)** + **OASys** ([GOV.UK][1])              | NPD: attainment, attendance proxies, SEN/SEND, CSC history; OASys: literacy/numeracy/learning difficulty flags                                                                       | Wider children’s services, health, youth services (DfE/LAs/DHSC) via linkage ([GOV.UK][2])  |
| **Accommodation / housing insecurity**          | **Civil court** + **OASys** ([GOV.UK][1])                    | Civil: possession claims/warrants + tenancy/rent/arrears; OASys: accommodation instability/addresses (plus LSOA/LAD for area joins)                                                  | Statutory homelessness (DLUHC) + LA housing systems / support services ([GOV.UK][2])        |
| **Family & marital / relationships**            | **Family court** + **OASys** ([GOV.UK][1])                   | Family court: divorce/child proceedings, harm alleged, number of children involved; OASys: domestic abuse involvement, childcare/caring responsibilities, care experience indicators | Social care case management + DV services + health impacts (LA/DHSC) ([GOV.UK][2])          |

[1]: https://www.gov.uk/guidance/ministry-of-justice-data-first "https://www.gov.uk/guidance/ministry-of-justice-data-first"
[2]: https://assets.publishing.service.gov.uk/media/683863d5c99c4f37ab4e867c/Data_First_User_Guide_Version_8.2.pdf "https://assets.publishing.service.gov.uk/media/683863d5c99c4f37ab4e867c/Data_First_User_Guide_Version_8.2.pdf"


6) “Linkage waves” recommendation for BOLD Prevention (fastest path to a national needs asset)

This sequencing gives quick wins while building toward the full cross-government risk factor picture.

- Wave 0 — Data First only (fastest proof of value)
    - Build a person-level dataset using OASys + probation + custody + criminal courts, enriched with civil possession and family court signals, using the cross-justice linking dataset.
    - Derive baseline risk factor flags/scores for: substance misuse, accommodation, ETE, finance/income proxy, relationships/domestic abuse proxy, mental health proxy.
    - Aggregate to place (LSOA/LAD) where permitted to support primary prevention planning (needs prevalence by locality).

- Wave 1 — Children/young people (prevention ROI)
    - Bring in MoJ-DfE (PNC↔NPD) to support the “poor child outcomes” axis and early years/education drivers.

- Wave 2 — Income & employment “ground truth”
    - Link to DWP/HMRC (benefits + earnings/employment) to turn OASys “finance/ETE” from proxy → validated outcomes.

- Wave 3 — Health & mortality outcomes
    - Link to DHSC/NHS datasets for physical health, MH service use, and mortality outcomes (critical for the ill-health outcome line and for understanding comorbidity).

- Wave 4 — Housing and local authority systems
    - Link to DLUHC homelessness + LA housing/support systems to move from “possession/housing stress” to a full homelessness pathway model.


7) What this means for the prevention analytics + modelling plan

- Feature coverage is strong for justice-proximal needs (especially via OASys) and for housing insecurity via civil possession + accommodation in OASys.

- The biggest analytical blind spots without external linkage are: (1) robust health outcomes, (2) true income/benefits, and (3) local service touchpoints outside justice—so those should be your priority linkage asks in the BOLD programme plan.

- Treat linkage quality as an explicit analytical risk: family/civil linkage is weaker than criminal justice datasets, so you’ll want a standard “linkage sensitivity” pack for all prevention use cases.




## What is Data First?
Data First is an ambitious data-linking, academic engagement and research programme led by the Ministry of 
Justice (MoJ) and funded by ADR UK (Administrative Data Research UK), who in turn are funded by the Economic 
Social Research Council (ESRC). The programme began in 2019 and has received a three-year extension to 2025. 
Data First unlocks the potential of the wealth of data already collected by MoJ by linking administrative datasets from across the justice system and beyond. It enables accredited researchers across government and academia to access anonymised, research-ready datasets ethically and responsibly. The programme also enhances the linking of justice data with other government departments (OGDs).
Data First datasets are deidentified, deduplicated and then shared, in most cases, with both the ONS Secure ResearchService (SRS) and SAIL (Secure Anonymised Information Linkage) Databank (there are some exceptions to this, which can be found in Section 2, Table 1, where a full list of available datasets can also be found). Approved researchers can then access the relevant data through a number of methods, including ONS safe 
rooms, approved remote desktop connections and the Safe Pod Network. Data cannot be removed to be stored, for example, on a researcher’s own PC or university servers.


## Data quality issues
1. Data First identify appropriate extracts of data to make available for research purposes from sometimes complex existing pipelines or from new copies of live databases. While certain fields are used by Ministry of Justice analysts, for example for release in Official Statistics publications, the programme includes data for which less is known about quality and limitations. 
2. Documentation may also be incomplete. In releasing this resource to the wider research community, our understanding of the source data will be increased. By collaborating, sharing experiences and expertise our assessment of its strengths and weaknesses in addressing research questions can be improved.
3. Data collection is carried out largely by frontline staff and users of services. Gaps in coverage are to be expected where items have not been considered essential to the original operational need, or even where entire populations of interest or categories of experience are absent from administrative sources.
4. Data may also be recorded inconsistently over time, across the country, or depending on entry method, meaning that data may not be of the desired quality or comprehensiveness to address important research questions. There is little harmonisation of the fields collected on different systems, creating inconsistency in data definitions, data formats and values. Researchers will therefore need to carry out their own cleaning and preparation ahead of analysis.
5. Over time, changes to management information systems, processes and policies may have introduced breaks in time series that could affect analysis and interpretation. Whiledata linkage creates great potential for in-depth longitudinal questions to be considered, researchers should remain aware of the scope and origin of the datasets being made available through Data First.

## Data linkage
### What data is being linked?
The internal administrative datasets that MoJ are bringing together as part of Data First 
each represent an interaction of a ‘user’ of the justice system (for example, a defendant, 
offender, or a user of the civil or family courts) with justice processes or services.
Most datasets contain duplicates of individuals (i.e., many records pertaining to a single 
person), and the same individual may appear in different datasets (for example, both as a 
defendant in a criminal trial, and as a respondent in a family law case). The challenge is 
that generally no reliable unique ID exists, either within or between datasets, to link 
information about a person back to previous ‘journeys’ through the justice system.
Data First aims to provide a unique ID for researchers working with one dataset, and also 
to identify through linked datasets when the same individual is thought to appear across 
multiple datasets (for instance, in both a court and a prisons dataset). 
Data First are linking records only at the level of an individual, to allow analysis of a 
person’s journey through the justice system. Data First are not identifying networks of 
individuals linked by personal information such as shared addresses over time (although 
some relationships such as between co-defendants in a single criminal case are linked in 
the source data). Combined magistrates’ courts and Crown Court datasets can also be 
linked at a case level, to follow the progression of a case through the court system. 

### Data linking process
Without a unique personal identifier, other identifying information is compared, such as 
names, date of birth and addresses, that are held in the source data to inform these 
decisions. This personal information will not be shared by MoJ and will be replaced in the 
data linking process by a meaningless identifier (one that has been generated for these 
datasets and is not used in any existing operational systems).
In some cases, two records will contain the same values in each of these fields, making it 
clear that they refer to the same defendant. However, duplicate records may not match for 
a variety of reasons, including:
• Typographical/phonetic errors
• Change of name/address
• Aliases/nicknames/diminutives
• Missing data
Internal data linking for Data First is done by adopting a probabilistic approach (using the 
canonical model of Fellegi and Sunter, 19691
) whereby each pair of records is assigned a 
match score based on the level of agreement in each attribute used for linking. Each 
attribute is assigned a weight that contributes to this match score, so a match on date of birth, for example, would influence our decision more than a match on gender, which adds 
less information. 

### Splink
To link the datasets required for Data First, a solution that can perform the necessary 
probabilistic data linkage at large scales has been developed by data scientists at MoJ.
The open-source Splink package uses Python and Apache Spark to link and deduplicate 
data flexibly, transparently and efficiently. The package implements the Fellegi-Sunter 
linkage model, estimating the parameters using the Expectation-Maximisation algorithm 
described by the authors of the fastLink R package in their paper.

## Limitations of data linking
Given the limitations of the personal identifying information in source data it is sometimes not possible to know with certainty whether two similar records relate to the same person. 
The choice of threshold match score will always represent a trade-off between the risks of false positives (linking records which belong to two different people) and false negatives (not linking records which do belong to the same person); each has different implications for research.
The probability threshold used should be suitable for most research and statistical purposes, for example, providing sensible estimates of the frequency of repeat interactions (individuals returning to court in a given time frame), and insights into shared characteristics of individuals with similar patterns. However, it is expected that a small proportion of false links will be included, where records belonging to two or more people are erroneously attributed to one person, and that not all genuine links will have been made due to the matching probabilities previously mentioned.
**The quality, consistency, and uniqueness of source data about individuals affect data linking accuracy. For example, it is much more difficult to determine that records belong to one person if they have used different names and moved address often, while namesthat appear less frequently can be grouped together more confidently. Researchers should be aware that accuracy in data linking for groups with different characteristics (such as socio-economic status or ethnicity) could differ because of these factors.
The proportions of false and missed links varies between datasets and is dependent on the completeness of demographic variables used during the linking process. In the case of family courts for example, missingness of key fields has led to non-randomness in linking taking place, and linkage being dependent, at least in part, on an individual’s role in a case. This will need to be considered as part of designing, reviewing, refining, and approving research projects.**

## How is the data protected?
The Data First programme has been developed within the framework established under the Digital Economy Act (DEA) (2017) which enables government to prepare administrative data for the purposes of research, and to provide de-identified versions of those data to researchers and projects accredited by the UK Statistics Authority (UKSA).
Data First is not sharing data directly with individual researchers but making pre-defined extracts securely available through our partnerships with the ONS Secure Research Service and SAIL Databank and **using the Five Safes Framework to ensure the safety and security of its stored data**. This is a set of principles adopted by a range of secure labs to provide complete assurance for data owners. 
### The Five Safes are:
• Safe People – trained and accredited researchers are trusted to use data 
appropriately. To access the data individuals must complete training and become 
accredited researchers under the DEA.
• Safe Projects – data are only used for valuable, ethical research that delivers clear 
public benefits. To access data the research project must have been approved by 
both the data owners (data access panels at MoJ and its agencies) and the 
Research Accreditation Panel (RAP). In order for research projects to be approved 
they must comply with the Research Code of Practice and Accreditation Criteria
which was approved by the UK Parliament in July 2018.
• Safe Settings – access to data is only possible using secure technology systems
through our partners at the ONS Secure Research Service and the SAIL Databank.
These are Accredited Processing Environments under the DEA which meet 
rigorous standards of security and data capability controls.
• Safe Outputs – all research outputs are checked to ensure they cannot identify data 
subjects.
• Safe Data – researchers can only use data that have been de-identified. Personal 
identifiers used in the linking are not made available for analysis and replacement 
values are generated for internal system IDs to prevent direct linkage back to the 
raw data source. Some special category data is being shared because of its value 
to research. It is highly unlikely that a researcher will be able to identify individuals 
from these fields alone.
Data processing within Data First is compliant with all applicable data protection 
legislation, including the General Data Protection Regulation and Data Protection Act 
2018, and a suitable legal gateway is required for all external data linkage. The MoJ-DfE 
data share does not rely on powers in the DEA.


## What are the benefits of Data First?
• Research – the programme enhances the strategic research capabilities of 
researchers across both government and academia.
• Better understanding of justice system users – the linkage of data provides a better 
understanding of justice system users, their characteristics and the journeys they take 
through the system.
• Improving the evidence base – linking justice-related datasets provides researchers 
with the capability to address research questions and develop a stronger evidence 
base to inform policy development and the effects of policy interventions.
• Relationship with academia – Data First brings together academia and government, 
building a partnership to utilise knowledge and expertise, and maximise the impact of 
the research.
• Lessons learnt – the programme allows MoJ to share the lessons they learn across 
government, academia and other stakeholders. 
• Improving the transparency of policy-making – research published under the Data 
First programme further enhances the openness of the use of evidence in 
policymaking.


## Workstreams of the Data First programme within MoJ:
• Internal data linking – development of a robust, automated linking pipeline between 
MoJ cross-justice system datasets using the Splink package.
• External data linking – establishing data shares with external partners, linking justice 
data with OGDs and managing research and analysis using the MoJ-DfE data share.
• Data engineering and data mapping – creating pipelines to bring new data sources 
into scope, agreeing what can be shared, designing and developing research-ready 
datasets with documentation.
• Research, academic engagement and communications – facilitating the link 
between Data First and the academic research community, supporting researchers to 
access and understand the data, and working in partnership to identify priority research 
questions to make best use of the linked datasets.


## What can the data be used for?
Administrative data can help to answer certain types of questions. Broadly speaking, Data 
First can address questions about who is interacting with the justice system in what ways, 
the processes and timings involved, and ‘hard’ outcomes such as sentencing or frequency 
of repeat appearances. The kind of data shared through Data First cannot provide insight 
into unmet needs, circumstances and experiences of people engaging with justice 
services.
Data First focuses on justice system users (for example defendants, prisoners, parties to 
family court and civil court cases). There is little information about the judiciary, court and 
prison staff, or legal professionals. Additionally, limited administrative data is held by MoJ 
on some public users such as victims and witnesses. 
Administrative data provides a good window into the big picture and small subsets. The 
datasets contain information on all relevant cases in England & Wales over the time 
periods covered. This means it is often possible to look at niche groups such as outcomes 
for different ethnicities, or at specific o
## Where does the data come from?
The Data First programme links and shares extracts of data from a range of administrative 
databases owned by the Ministry of Justice and its agencies, His Majesty’s Courts and 
Tribunals Service (HMCTS) and His Majesty’s Prison and Probation Service (HMPPS), as 
well as works to put agreements in place with other government departments to share data 
from other sources. Currently, the datasets linked and shared by Data First include 
information on:
• Criminal court cases and defendants in magistrates’ courts and the Crown Court in 
England and Wales
• Offenders in prison custody or under supervision of probation services in England 
and Wales
• Civil and family court jurisdiction cases and parties (the people and organisations 
involved) in England and Wales
• Department for Education data on young people in England’s education data from 
the National Pupil Database (NPD) linked to Police National Computer (PNC) data 
on criminal histories.
In future, data will be made available on offender assessments and from other government 
departments subject to agreements.ffence types.
<!-- END FILE: data_first.md -->

---

<!-- BEGIN FILE: System_Challenge_K_and_BOLD_Prevention_notes.md -->
# System Challenge K and BOLD Prevention Implementation Notes (MoJ/BOLD)

> Outline:  
> (1) System Challenge K context converted to Markdown (no information removed)  
> (2) Implementation stages for BOLD Prevention aligned to MoJ/BOLD data-linking discovery  
> (3) Ideas for using data discovery + use cases to plan/initiate/develop data linking and generate insights

---

## Part 1 — System Challenge K context (converted to Markdown, with no information removed)

# System Challenge K – Scope and Ambition: A focus on prevention and collaboration 

Amid high levels of demand on public services, the need to improve public sector productivity, and changing expectations and requirements of public services stemming from the Covid-19 pandemic, Government is reflecting on how best to utilise resources to meet need and why a preventative approach isn't taken when we recognise that it is better than intervening at acute crisis stage. **How are circumstances different now to the previous 10-20 years?**

## Hypothesis
Our hypothesis is that a more preventative approach to public spending, that focuses on intervening earlier to prevent problems before they develop and intervening earlier when they do, could both improve outcomes for high-needs cohorts and reduce demand on public services. 

## Why a cross-government approach is required
This work requires a cross-government approach, due to the interdependencies between departments impacting demand for public services. Activity in one area of government can drive upstream or downstream demand elsewhere, and therefore requires joint solutions – for example, strong joint working between probation, housing services and health can support can help ensure offenders access the support they need improving their outcomes across offending, homelessness and health, and potentially reducing longer term demand for those services. By taking a system-wide approach to reviewing this challenge, there is an opportunity to enhance collaboration to improve life outcomes.

## Aim of the overall “System Challenge” work
Our aim for this as an overall, ‘System Challenge’ piece of work is to: 
- Develop a shared evidence base where we understand the risk factors impacting outcomes, the drivers of demand across services, and the different cohorts and places where there may be opportunity to improve outcomes and reduce demand;
- Identify and shape joint policy options to that enable greater impact on early intervention and managing demand across services; 
- Identify systemic barriers to cross-government working and early intervention and develop proposals to address these in the long-term.  

---

## Defining “egregious” social outcomes
Through cross-government mapping, we identified the most egregious social outcomes. We are defining ‘egregious’ as:

- Patterns of public service provision which drives people up the ‘cost spiral’, thus ultimately fuels public spending to a higher level than otherwise needed.
- Exceptionally ineffective engagement from public services from a user perspective, with multiple reactive contact points which do not consider how a person got there or builds on strengths.
- Exceptionally high cost/volume areas of public services where there is a plausible set of preventative interventions that we could – but currently do not – do to flatten the curve of future demand and reduce future spending.  

---

## The six social outcomes used to frame the challenge
The six social outcomes that we used to frame the challenge, drawing on the existing evidence base and analysis, were:
- Offending (MOJ and HO)  
- Ill-health and early mortality (DHSC)  
- In-work poverty (DWP)  
- Long-term inactivity and unemployment (DWP)  
- Homelessness and home insecurity (DLUHC)  
- Poor child outcomes (DfE)

---

## Drivers of the six egregious social outcomes
See Cross-government demand mapping identified the drivers of the six egregious social outcomes: A set of common and overlapping risk factors drive those outcomes: **poor mental health; poor physical health/activity/nutrition; low income; substance misuse; employment; early years and education; accommodation; and family and marital.**

### Figure 1: Drivers of social outcomes
Analysts used publicly available evidence and frameworks to determine the key drivers or risk factors of each social outcome.

### Figure 2: Network analysis
MoJ analysts then mapped risk factors against social outcomes and explored their linkages, to produce a ‘map of maps’ or network analysis.

### Figure 3: Network of weighted links of drivers of outcomes
MoJ analysts rated the level of impact of cross-cutting drivers and the level of evidence to support this. 

---

## Complexity and analytical capability
Understanding the drivers of poor outcomes – what they are, how they manifest for different cohorts, including their relative strength – is incredibly complex and HMG does not have a strong understanding of the way multiple risk factors interact to drive poor life outcomes. This indicates that there is latent civil service capacity and capability to think across systems and, despite increase sophistication of our data and analytical capacity, there are still areas for improvement.

---

## Deep-dive focus: three ‘no-regrets’ areas with greatest potential impact
Leveraging our understanding of demand mapping across government and the range of interventions already in place, we agreed with XWH DGs to take a deep-dive approach, focusing on three ‘no-regrets’ areas with the greatest potential to make an impact.

### 1) Population wide health challenge (obesity): primary prevention  
This deep dive focuses on primary prevention for obesity – which is the most significant modifiable risk factor, after smoking, for the six major conditions which collectively are the greatest contributors to ill-health and early mortality.

**Rationale:**
- Good health is an asset, improving quality of life, supporting economic growth and reducing demand for public services. This is particularly the case if we can target and prevent the main causes of premature and disabling ill health - 'compressing' morbidity so people spend fewer years in ill health, later in their lives, and more years in good health.
- Obesity is growing in prevalence and leads to a range of poor outcomes: **12% of avoidable death and disability is attributable to high BMI; cost per person of severe obesity doubles that of someone with a healthy weight; obesity is associated with 38% higher probability of unemployment for age 50-65.**
- Trends indicate that these outcomes may worsen, with OECD estimating obesity causing increased labour costs, lowering GDP, reducing the workforce, and increasing the average tax rate between 2020-50.
- Tackling obesity is a shared responsibility across government, with different departments holding influence over wider factors that act directly on health or shape behaviour.

**NB:** Following the general election announcement, this deep dive is being taken forward directly by DHSC with HMT. 

### 2) Upstream targeting for vulnerable young people: secondary prevention  
This deep dive looks at secondary prevention opportunities to intervene earlier with children and young people, to prevent poorer outcomes later in life, avoid costs to the system and alleviate demand pressures.

**Rationale:** 
There are a rising numbers of children with needs and circumstances in childhood that lead to worsening outcomes:
- Child poverty and housing security – which acts as a backdrop to a range of poor outcomes. Rates of relative and absolute poverty rising since 2016/17 for families with 3 or more children.
- Whole family support – ensuring that a broader range of challenges for a child and their families are tackled to prevent longer term impacts (currently seen in rising CSC numbers, more complex needs, and poor outcomes).  
- Mental health and SEND – rising child MH and SEND, flowing into rising child DLA & 18-24 disability benefit claims (as well as pressure on the SEND system / LAs and wider poor outcomes)  
- Attainment and transitions into work – following re-widening of the attainment gap post covid, [increasing] NEET, [low attainment translating into poor employment outcomes]. 

Trends indicate that these outcomes may worsen: the overall rate of 16-18-year-olds who are NEET increased by **8.4% in 2022**, the highest rate since 2012. Without interventions, LAs will need to spend **£18.5bn by 2032-2** to meet children's social care demand.  

### 3) Vulnerable adults with multiple disadvantages: tertiary prevention  
This tertiary prevention deep dive looks at vulnerable adults with multiple disadvantages, defined by Changing Futures as those with overlapping experiences of homelessness, substance misuse, mental health issues, domestic abuse, and contact with the CJS.  

**Rationale:** 
- Vulnerable adults with MD require holistic service provision to address their interdependent needs. Effective join-up between local services is therefore required. This deep dive looks at how people interact with services from the bottom-up (local-level) and where the opportunities are to intervene earlier to prevent ('rescue’) at the multiple disadvantage stage. This will enable us to identify points for effective, targeted intervention to address risks earlier across issues, with a focus on delivering joined-up services that increase the likelihood of an individual maintaining their health, housing and employment.
- MD represents a high cost to the system, with high needs individuals interacting with multiple different public services repeatedly: for example, those on the Fulfilling Lives programme cost public services an average of over **£28,000 per year**.
- With demand on public services on the rise, problems for this cohort will continue to worsen without foundational services in place to support them:
  - In 2023, mental health services recorded **5 million referrals**, up **33% from 2012**;
  - demand for prison places is outstripping supply;
  - a record **112,000 households were homeless and living in temporary accommodation in December 2023** (a **12.1% increase** from the previous year).

---

## International comparators
- A ‘whole system’ approach which focuses on tackling the drivers of poor outcomes has produced positive results: over **500 communities** in high-income countries have trialled a ‘Communities that Care’ intervention, which uses a community-level, cross-system preventative approach to decrease risk, enhance protection and reduce mental-risking behaviour in youth. This has effectively prevented delinquency, violence, and substance abuse amongst young people.
- There is benefit in bringing together wraparound support services into a single location, particularly for those with complex needs: **Common Ground** is a programme available in some cities in the USA and Australia which offers wraparound support for vulnerable adults with multiple disadvantages in a single building. Success has been indicated by high retention rates, however, there are some negative unintended effects of co-locating people with complex needs.
- Several countries have allocated specific funding to tackle cross-system social challenges, which has proved beneficial: The Australian government provides funding to support several measures related to student mental health including a new voluntary mental health check to ensure students get the support they need.​

---

## Expert thinkers
- External experts believed there are opportunities for better cross-government working to improve outcomes: The House of Lords Public services Committee’s inquiry into transitions from education to employment for young disabled people highlighted the lack of joined-up thinking across government for this cohort and advocated for a ‘one-stop shop’ approach.
- Experts also advocate for funding changes to promote greater investment in preventative activity and encourage spending cross-cutting challenges:
  - The Independent Review into Children’s Social Care found that the system has become overwhelmingly focused on the costliest, crisis end of intervention. It recommended a shift in the way CSC services respond to families who need help by creating a new Family help service, which is adequately funded by actors across government. ​
  - To address multiple and complex needs, the Future Governance Forum ‘Place-Based Public Service Budgets’ proposes understanding total local public spending and bringing together local services to plan how to best spend that money, with more responsibility given to local areas and greater involvement from local communities. 
- Experts have identified opportunities to take a more person-centred approach to achieve intended outcomes:
  - Academics promoted the ‘Liberated Method’ as a flexible, person centred approach to public services for those with MD. It recommends focusing on the needs of the individual, rather than delivery of a pre-defined service.
  - The Centre for Social Justice advocates for a whole family approach to prevention, bringing services together before they escalate. 

---

## Equalities
There are complex disparities in the representation and experience of men and women across various outcomes and risk factors:
- While most adults with MD are male, women are more likely to have experienced domestic violence, and this in turn makes them more likely to have other disadvantages including contact with the CJS, mental health problems, homelessness, and substance abuse.
- In younger people, boys are more likely to have an identified SEND need (**21.9% vs 12.2% of girls**), while young women under 24 are almost three times more likely to experience a common mental disorder such as anxiety or depression.

Poor outcomes and associated risk factors are disproportionately represented among ethnic minorities: people from Black, Asian, and minority ethnic communities experience a range of socioeconomic disadvantages which contribute to their experience of multiple disadvantages. 

There are clear links between individuals with experience of care and poor outcomes and disability, which is overrepresented in the population experience multiple disadvantages.  

---

## Geographies
Poor outcomes are disproportionate concentrated in more deprived areas: there are large geographic differences in the percentage of children with a good level of development, ranging from **55% in the most deprived neighbourhoods to 75% in the leas deprived areas.** MD is also associated with areas with high rates of unemployment and/or poverty.

There are regional disparities between places that experience poor outcomes and variation between local authorities in the quality of services and in their overall financial position: MD was found to be heavily concentrated in Northern cities, some seaside towns and central London boroughs; higher levels of absolute poverty were identified in the North, Midlands, and London (after housing costs), as well as higher rates of NEET (young people not in education, employment, or training) in the North East. 

---

## Common themes: systemic change is required to overcome barriers in prevention

### 1) Opportunities to improve central government processes to support prevention

#### Funding  
There is a lack of clarity around prevention and preventative spending. Current funding processes are also too short term and act as a barrier to joined up XWH working. Funding is largely allocated on a short-term basis i.e. 1-3 years making it hard for preventative programmes to plan for the long term. Political pressures also mean that funding is skewed towards acute pressures rather than longer term strategies that would take years, or even decades, to see the benefit.

Options to address this include:
- Long-term funding horizons (over more than one spending cycle) to secure buy-in for necessarily long-term preventative policies;
- Cross-department funding bids, devolution of budgets or central pooling of budgets – recognising that savings often do not accrue where preventions spend is invested.
- Approaches to evaluation and options appraisal which respond to systemic interventions rather than issue-based interventions and give weight to benefits beyond short-term cashable savings.
- Ringfencing for prevention that is underpinned by evidence and governed by “rules”. 
- Developing ‘ready-reckoners’ on how costs flow through and technocratic measures.

#### Governance  
A common barrier to cross-cutting preventative work identified throughout this work is the siloed structure and culture of government, as preventative policies often require cross-departmental collaboration. Currently, departments tend to work in isolation and focus on their own policy areas. There is also a lack of data sharing across government, which further prevents XWH strategic join up.

Options to address this include:
- Mission delivery boards as a way of cross-government collaboration to overcome working in silos and to design interventions to address people's in the round rather than thematic service interventions.
- Bolder use of non-spending levers, such as regulation, tax, behavioural nudges.  

#### Data
Creating a common data-sharing framework across OGDs could help standardise this process so that we can maximise the usage of data between and across departments. To conduct robust, comprehensive demand mapping, government would need to ensure that individual data sets are complete and then develop ‘data linking’ infrastructure for modelling. 

#### Evidence and Evaluation  
There is limited evidence around preventative interventions to support their funding and implementation. This is partly because of time taken to have an impact e.g. Sure Start evaluation has only just been released a decade after the programme ended. It can also be difficult to prove causality between upstream interventions like social action and sports programmes and downstream outcomes, especially as there are often interrelated programmes targeting similar outcomes.

Options to address this include:
- Drawing more evidence from international examples
- Encouraging more experimental and ambitious pilots and policies
- Embedding prevention into spending and performance frameworks, perhaps by improving the current ODP system.  

### 2) Local systems changes to help partners deliver preventative services

#### National vs Local  
Current funding and governance is overcentralised, meaning that while local authorities are largely responsible for delivering preventative interventions, they often have limited scope to influence or design preventative policies according to their specific needs. This leaves local services struggling to support vulnerable cohorts, as central government does not make policies or allocate funding in line with locally-specific needs.

Options to address this include:
- More flexible, responsive, person-centred local services rather than nationally prescribed threshold for access to services
- Data sharing and join up services to spot warning triggers of repetitive use earlier and detect users bouncing between services
- Flexibility of local funding to support focus on prevention.
- Refreshing strategic relationships with the VDS.  

---

## Policy ideas – what are our ‘big bets’ in these deep-dive areas?
As well as changes at national and local level, we have identified some 'big bets' we are keen to land with any potential incoming government. 

While we paused the formal commissioning of our planned ‘Phase 2’ work on developing policy options, we have maintained engagement with our deep-dive leads to conduct several workshops to identify these 'big bets'. 

### Upstream Targeting for Vulnerable Young People: Lead Policy Options

#### Scope of Services  
Providing universal provision of positive services (e.g. youth activities and clubs) alongside targeted help to families with multiple problems, improving outcomes and driving down demand for significantly more expensive services i.e. child in care, youth justice system, long term benefit demand, NEET.

#### Mental Health  
a focus across government on children’s mental health, particularly acute given the impact of the pandemic, social media etc.  

#### Other Policy Options:
- Workforce Provision: We will need the right workforce across public services to deliver support and prevention. Important to examine a long-term plan to foster this workforce.
- SEND & Disability: Joint work between DWP & DfE, on importance of early identification and support, providing effective services, focused on positive life outcomes, maximising employment outcomes, and reducing benefit dependency, with a particular focus on opportunities for better identification and support in the early years.
- School Attendance: Improving school attendance is an important goal to surround vulnerable children with stability and structure.   

#### 'Process' Options:
- Long-term focus on Prevention: Making the case for greater, multi-year intervention funding in the long run, to avoid high numbers of children in custody or other difficulties five/ten years down the line. 
- LA as Strategic Partner: Getting our cross-government approach to this right is vital to delivering any reforms successfully. We need to make sure the partnership with LA and stakeholders/the third sector is as effective as possible. This includes consideration of funding, multiple grants, local partner infrastructure, and the capability to drive innovation & change.
- Government Structure and Spending Review Bids: should departments bid on prevention (e.g. MoJ), it may be other departments which see the benefits. How do we ensure that how the mechanisms of central govt are there to support this cohort when provision will need to come from a range of departments? How do we strike the right balance between building long-term preventative focus but without losing focus (and ringfence?) on children already in the criminal justice system, for example?  

#### Crucial Focus:
Mental Health: there is a need to focus on mental health to prevent risk factors from emerging amongst children, particularly given the effects of the pandemic and rising social media use. 

#### Early years/family services  
Early years intervention and whole family support has provided foundational in improving outcomes and reducing costs. This is reflected in the success of Sure Start, which provided support for local families through a range of services with the aim of enhancing development and life chances of children under 5. Evaluation shows that children who lived close to a Sure Start centre for their first 5 years performed better in their GCSEs by **0.8 grades** and there was a reduction in the likelihood of having an Education, Care, and Health Plan by age 16.   

#### Alignment with Manifesto Commitments: CONSERVATIVES
The Conservatives have also made commitments to improve skills and opportunities for young people by investing in apprenticeships and implementing National Service for 18-year-olds and increasing childcare for families. They will also open mental health  ‘early support hubs’ for 11–25-year-olds.  

#### Alignment with Manifesto Commitments: LABOUR
The Labour ‘Opportunity’ Mission has a strong focus on early years and young people. There are specific references to some of the common risk factors we identified as impacting social outcomes, such as mental health, SEND and childrens social care. 
- Family - Family support and child poverty through benefits and improved data-sharing between services and ensure families don’t fall through the cracks with a single unique identifier.
- SEND and Mental Health – Community-wide approach to improve services for SEND.
- Universal services – ‘Expanding Experiences’ with Art, Music and Sport.
- The Safer Streets mission's commitment to halving knife crime in 10 years alongside a greater focus on prevention will rely on more effective and joined-up interventions with at-risk teenagers.

---

## Vulnerable Adults with Multiple Disadvantages: 'Process' Options
- Adopting an equality lens to ensure specific needs of female offenders, offenders from an ethnic minority background and those from other protected characteristics are supported.
- Strengthening the use of Justice Impact Tests (JITs) to ensure we increase the use of JITs for all upstream policy changes across government that have an impact on downstream demand, and that the department is compensated for the associated costs of the policy changes. 
- Data: Create a common data-sharing framework across OGDs to help standardise this process so that we can maximise the usage of data between and across departments.
- Female offenders: Share the burden for funding the women's community sector across all departments/agencies who benefit (e.g. health service and substance misuse services benefitting from co-location at women's centres).
- Female offenders: Support the implementation of Whole Systems Approaches at a local level to better support complex women. A WSA in all local areas would see improved collaboration between agencies/services with more women offered earlier intervention and diverted away from the CJS.
- Commissioning: Work on a devolved/pooled local commissioning model to create integrated Health & Justice teams with pooled budgets, including probation services who will be best placed to support the needs of those in their communities.
- Working to ensure funding restrictions are not a significant barrier to this cohort requiring support.  

### Policy Options:
- Changing Futures (DULHC to add), including a focus on housing.
- Diversion: To fund and commission bespoke mental health treatment interventions for diversionary OOCDs.
- Diversion:  Support cross-gov coalescence around the need to intervene early and effectively divert away from the CJS into a more appropriate service.
- Strengthen existing services in their support of these cohorts.
- Health: To support, co-create and fund a cross-government public health strategy for crime reduction which the addresses the social determinants of poor health and crime. This would mark a shift away from thinking about crime and violence as individual pathology and towards thinking about it as a public health issue. 
- Multiple complex needs: To pilot a flagging scheme to identify people making multiple contacts with agencies - showing complex needs and escalating requests for support. Explore how information systems could support staff across health and justice to identify people with multiple complex needs (MCN)
- Early intervention: Use jobcentres/schools/GPs/ frontline services as opportunity for early intervention through identifying and signposting vulnerable to appropriate support.  

### Crucial Focus:
- Housing: even when efforts are made to improve system join-up for this cohort, severing housing shortages are a barrier to access that disproportionately affect the most vulnerable. The system for the supply and delivery of supported housing needs to be rebuilt. This is a key preventative intervention for adults at risk of or experiencing MD, who are at risk of housing insecurity, homelessness and rough sleeping without suitable accommodation and support. This in turn drives negative outcomes including poor physical and mental health and being victims and/or perpetrators of crime and ASB. 
- Health: MD is associated with a poor high health profile, indicating a link between poor health outcomes and MD. Policy options also note a need to focus on a public health strategy for crime reduction.  

### Alignment with Manifesto Commitments :  CONSERVATIVES
LAs will be given multi-year funding to support social care and continue plans to end rough sleeping through the LA Housing Fund.  

### Alignment with Manifesto Commitments :  LABOUR
The Labour manifesto pledges to intervene earlier to stop young people being drawn into crime, creating a new Young Futures programme with a network of hubs reaching every community. These hubs will have youth workers, mental health support workers, and careers advisers.  

---

## Ensuring effective delivery of demand prevention doesn’t end here: We are keen to:
- Using our cross-Whitehall Senior Working Group as a community of practice.
- We propose immediate next steps for this group to continue to work virtually on cross-cutting prevention and early intervention proposals, including relating to thinking on the Labour mission on opportunity and Cabinet Office coordination of those, and to take stock after the election on continued meeting as a community of practice.
- Embed a Prevention First approach across government, by agreeing a shared definition and approach. 

As per HMT's 2024 Prevention Framework, we have defined prevention as **'an intervention that prevents further downstream costs and/or produces better outcomes for the public in areas of social policy’.** There are three ways of categorising prevention:
1. Primary prevention – preventing a problem from occurring in the first place (e.g. early years family based-interventions)
2. Secondary prevention – intervening early when a problem starts to emerge to prevent it becoming established (e.g. therapeutic foster care)
3. Tertiary prevention – making sure an ongoing problem is well-managed to avoid crises and reduce its harmful consequences (e.g. victim/offender mediation)

We can go further and develop a Prevention First mission with our devolved partners, local authorities and the third sector.

- Feed this thinking into briefings for incoming ministers, using one cross-government voice where possible.
- Alongside HMT, use this work to inform potential joint spending-review bids and long-term planning.
- Continue gathering rich data to inform our approach.

---

## Part 2 — Practical implementation stages for BOLD Prevention (mapped to the MoJ/BOLD data-linking discovery approach)

The attached MoJ/BOLD discovery pack sets out a **data-linking-specific Discovery** with seven stages and clear role expectations across policy, analysts/data science, and service design.  
Below are implementation stages for the **BOLD Prevention SPEC** (Projects 1–3), using that structure, and then extending into delivery/pilots/scale.

### Stage 0 — Scope your discovery (mobilise + boundaries)
**Purpose:** Avoid “boil the ocean” and make discovery tractable.

**Actions for BOLD Prevention**
- Fix the initial boundary using System Challenge K:
  - pick **one deep-dive cohort** to prioritise for early value (e.g., MD adults; vulnerable young people) *and* one **cross-cutting outcome** (e.g., offending + homelessness, or child outcomes + MH/SEND).
- Explicitly decide:
  - Are we scoping a **programme** (multi-year) or **one linkage project**?
  - Do we include **operational linking** (frontline single view) now, or only **strategic/policy** linking first?
- Define “Discovery exit criteria” up front:
  - clear use-case shortlist,
  - mapped data landscape + maturity assessment,
  - IG route identified (DPIA/DSAs/MoUs),
  - a recommended option with resources/timeline/risks.

### Stage 1 — Stakeholder engagement (continuous, but structured)
**Purpose:** Joint ownership, trust, and feasibility.

**Actions**
- Build a stakeholder map that includes:
  - policy owners for the six outcomes,
  - data owners/controllers,
  - delivery partners (LBBD, Community Help Partnerships),
  - governance: IG/DPO/security, safe outputs, AQA reviewers,
  - lived experience reps where appropriate.
- Run a “cross-system journey” workshop per deep dive:
  - map where users “bounce” between services (a named System Challenge K issue),
  - identify where earlier touchpoints exist (jobcentres/schools/GPs/frontline).

**Outputs**
- Stakeholder map + comms plan; RACI; engagement cadence; agreed decision forum.

### Stage 2 — Problem definition (and theory of change)
**Purpose:** Prevent solution-first thinking.

**Actions**
- Translate System Challenge K into **problem statements** that are measurable:
  - e.g., “Repeated reactive contact points and cost spiral for MD adults due to fragmented service visibility.”
- Build a **theory of change** for each of Projects 1–3:
  - how national asset → better planning,
  - how national–local linking → earlier detection & coordinated action,
  - how analytics/LLMs → better identification/triage/policy design.

**Outputs**
- 1–2 page problem definition per priority deep dive + theory of change diagram.

### Stage 3 — Insight gathering (data landscape + user/system understanding)
**Purpose:** Evidence-led feasibility.

**Actions**
- **User/system mapping:** current process maps for:
  - local referrals, assessments, casework,
  - where data is captured (structured vs free text).
- **Data mapping:** identify datasets for:
  - the six outcomes,
  - the shared risk factors (mental health, income, substance misuse, accommodation, etc.),
  - interventions and service contacts (to observe “cost spiral” patterns).
- Request **safe samples** (where permissible) or run analysis in trusted environments to assess:
  - identifier completeness,
  - timeliness,
  - data quality and coding consistency,
  - linkage feasibility.

**Outputs**
- Data landscape map + “maturity” scorecards,
- initial descriptive insights (coverage by geography/time; known bias risks),
- draft data dictionaries.

### Stage 4 — Options/opportunity development (use-case-led)
**Purpose:** Create deliverable options where **high user value overlaps with robust data**.

**Actions**
- Co-create use cases (½–1 page each) for both:
  - **Strategic/policy** value (national prevalence, cohort discovery, intervention evaluation),
  - **Operational** value (frontline single view; flagging multiple contacts).
- For each use case, define:
  - actor/persona,
  - trigger,
  - step-by-step workflow,
  - desired outcome,
  - system/policy requirements (consent/IG, access, timeliness, product channel).

**Outputs**
- Use case library + prioritised backlog,
- mapping: use case → required datasets → identifiers → feasible linkage approach.

### Stage 5 — Stress-test options (doable, sustainable, appropriate)
**Purpose:** Decide what will actually work.

**Actions**
- Run structured stress tests per option:
  - IG route complexity (DPIA/DSAs/MoUs),
  - data robustness (missingness, timeliness, linkage error risk),
  - operational readiness (frontline workflow, governance, safe outputs),
  - equity impacts (gender/ethnicity/disability/geography risks),
  - benefits realisation and evaluation feasibility.
- Include a “what we will *not* do” section for each option (to manage expectations).

**Outputs**
- Options paper with scored trade-offs + recommended option(s),
- linkage quality plan (false match/missed match estimation; drift monitoring),
- evaluation/benefits plan (including “impactability” questions).

### Stage 6 — Scope definition and planning (turn the option into a delivery plan)
**Actions**
- Convert the chosen option(s) into:
  - a scoped delivery plan (resourcing, milestones),
  - an IG pack plan (DPIA, DSAs/MoUs, Five Safes, safe outputs),
  - a technical plan (pipelines, linkage approach, monitoring),
  - an adoption plan (who uses outputs, how, and when).

**Outputs**
- Delivery plan for Projects 1–3 (with dependencies),
- benefits tracking plan and AQA checkpoints.

### Stage 7 — Decision point (proceed / pivot / pause / stop)
**Purpose:** Ethical, informed decision-making.

**Actions**
- Provide senior leaders with:
  - the recommended plan + costs/resources,
  - explicit risks (incl. equity and public trust),
  - what is excluded,
  - the value proposition to BOLD/MoJ priorities and cross-government demand reduction.

**Output**
- Signed decision + mobilisation of delivery teams.

---

## Part 3 — How to use the “data discovery tool” + use cases to initiate and develop data linking (with insight ideas)

The discovery pack’s core idea is: **blend user needs discovery with data landscape discovery** to find the overlap that is worth building.  
Here’s a practical way to operationalise that for BOLD Prevention.

### A) Set up a “Use case → Data → Linkage” pipeline (repeatable playbook)

1) **Build a use-case backlog first (not a dataset wishlist)**
- Start from System Challenge K “egregious” definition:
  - cost spiral trajectories,
  - ineffective reactive engagement,
  - high cost/volume areas with plausible preventions.
- Ensure the backlog spans:
  - **Primary** (planning/resource allocation),
  - **Secondary** (early warning/triage),
  - **Tertiary** (recurrence reduction + impactability).

2) **For each use case, create a “minimum viable data specification”**
- Outcomes to measure (offending, homelessness, MH crisis, NEET, etc.)
- Risk factors to represent (mental health, accommodation, substance misuse, income…)
- Intervention exposure(s) (who received what, when)
- Time windows (“as at” rules) to avoid leakage for any predictive outputs

3) **Use the MoJ data discovery tool to locate and qualify candidate datasets**
Even if the internal tool differs by platform, the workflow is consistent:
- Search by:
  - outcome domain (e.g., “homelessness”, “reoffending”, “SEND”),
  - risk factor domain (e.g., “mental health”, “substance misuse”),
  - geography/time granularity needs (local authority, monthly/weekly).
- Capture a standard metadata record:
  - owner/controller, access route, sensitivity, update frequency,
  - available identifiers (and completeness),
  - key variables, code lists, data quality notes,
  - safe setting availability.

**Tip:** maintain a single “data landscape register” that becomes the national asset’s living index.

4) **Linkage feasibility screening (fast triage before deep work)**
For each candidate linkage pair/triple, score:
- identifier availability + completeness,
- timeliness (can it support operational use?),
- expected linkage error risk,
- legal/consent route complexity,
- expected value if linked.

5) **Only then do deeper assessment**
- Request safe samples or run analysis in trusted environments:
  - missingness,
  - duplicate rates,
  - stability over time,
  - coding consistency.
- Draft the linkage design:
  - deterministic vs probabilistic,
  - temporal join semantics (“as-of” joins),
  - linkage quality measurement plan.

### B) Use cases that naturally fall out of System Challenge K (starter set)

Below are examples you can use to kick-start the backlog (each should become a ½–1 page use case in the discovery pack format):

#### Strategic / policy use cases (national asset + planning)
- **Needs prevalence by locality**: met/unmet needs across accommodation, MH, substance misuse, income; mapped to the six outcomes.
- **Cost spiral trajectories**: common sequences of multi-service contact that precede high-cost outcomes (e.g., homelessness → ED MH contacts → offending).
- **Cohort discovery**: “vulnerable young people at risk of NEET + later justice contact” (link education/truancy/SEND proxies to later outcomes in safe, pseudonymised form).
- **Impactability**: where flagship interventions appear to work best/worst (place, cohort, timing), with uncertainty explicitly reported.

#### Operational / frontline use cases (national–local + single view)
- **Multiple-contact flagging** (System Challenge K policy option): identify individuals/households with escalating repeated contacts across agencies; trigger proactive multi-agency review.
- **Earlier warning triggers**: detect patterns of “bouncing between services” and surface a structured view to practitioners (not automated decisions).
- **Household single view**: combine local resident data with national justice signals to support personalised interventions (initially LBBD pilot, built for scalability).

#### NLP/LLM-enabled use cases (only where lawful + safe)
- **Unmet need extraction** from case notes/referrals where structured fields miss key needs (e.g., housing insecurity indicators).
- **Structured summarisation** for practitioners (with strict grounding, audit, and human review).

### C) Insights you can generate quickly during discovery (before full linkage)

These are “early value” analyses you can run on first-iteration datasets (e.g., SAIL/DataFirst and/or safe extracts), to show momentum while IG/linkage work progresses:

1) **Risk factor overlap map**
- Recreate/extend the “map of maps” network using actual admin data proxies:
  - which risk factors co-occur most and for whom,
  - which are most predictive of downstream high-cost outcomes.

2) **Geographic concentration**
- Identify hotspots where poor outcomes cluster (and where service capacity/financial stress is highest), aligned to the System Challenge K geography findings.

3) **Service interaction patterns**
- Quantify “reactive contact points” and churn between services:
  - counts of contacts,
  - rapid repeat contacts,
  - transitions between service types.

4) **Equity lens dashboards**
- Track differences by sex, ethnicity (where lawful/available), disability/SEND proxies, care experience proxies, and deprivation:
  - linkage coverage,
  - outcome rates,
  - intervention reach.

### D) Governance and trust built into the discovery outputs (don’t bolt on later)

For each prioritised use case, your discovery outputs should include:
- **Purpose + public benefit statement** (why linkage is necessary and proportionate)
- **IG route map** (DPIA/DSA/MoU needs; roles and responsibilities)
- **Five Safes controls** (especially Safe Outputs)
- **AQA plan** (what gets peer reviewed, when)
- **Linkage quality plan** (false match/missed match estimation + subgroup drift checks)

---

### Next optional artefact
A single **Discovery Workbook** (Markdown) with:
- a use-case template,
- a data landscape register template,
- a linkage feasibility scoring sheet,
- and a senior decision pack structure (for Stage 7).
<!-- END FILE: System_Challenge_K_and_BOLD_Prevention_notes.md -->

---

<!-- BEGIN FILE: data_linking_Splink_Discover.md -->
# Appendix: Data linking (SPLINK) and Discovery (BOLD) packs

## Appendix A: Linked Data on the Analytical Platform (SPLINK)  
*Converted to Markdown from “Linked Data on the Analytical Platform” (March 2022).*  
**Source files:** `Linked Data on the AP.pdf`


### A.1 Title page
**Linked Data on the Analytical Platform**  
A presentation on data linking, for people who don’t care about linking and just want the data  
March 2022  
Powered by SPLINK  
Robin Linacre, Sam Lindsay, Theodore Manassis

---

### A.2 Introductions — Data First and the Internal Data Linking team
- **£2.9 million funding** from ADR UK for the period September 2019 - March 2022 “to harness the potential of administrative data from across the justice system”
- Translation - to link, catalogue and share the biggest datasets at the MoJ:
  - Criminal courts (mags and Crown) 
  - Prisons 
  - Probation - Delius
  - Family courts
  - Civil courts

**Team list (as shown):**
- Robin Linacre
- Sam Lindsay
- Theodore Manassis
- Tom Hepworth
- Zoe Slade
- George Kelly
- Thomas Hirsch
- Tapan Perkins

---

### A.3 Introductions — what the team “really want to do”
**What we really want to do:**
- Make up-to-date, linked data available to all analysts across DASD through the Analytical Platform, facilitating new in-house analysis and research
- Develop a flexible, scalable, open-source data linkage software:
  - to build capability for everyone to add to the linked data products on the AP
  - to collaborate with OGDs (e.g. ONS, NHS Digital) and academics to establish best practices and common ways of working across government

---

### A.4 How is the data linked? (overview)
**How is the data linked?**  
For more detail, ask us about splink...

- We create a standardised table of identifiers from one or more datasets…
- …and then compare all plausible pairwise matches…
- …and assign a match score to each pair

---

### A.5 How is the data linked? (clusters)
For more detail, ask us about splink...

Finally, we identify clusters of matched records, with a minimum threshold match score  
(Threshold examples shown: **>0.8** and **>0.95**)

---

### A.6 Our products — flatfiles
**Tables shared with ONS as part of Data First**  
Athena database: `data_linking_data_first`

**Deduplicated, anonymised datasets:**
- Magistrates’ and Crown court data
- Prisons data
- Probation (Delius)
- Family

**Linked IDs:**
- Person table (mags, Crown & prisons and probation)
- Journey table (mags & Crown cases)

---

### A.7 Our products — linking lookups
**Tables for internal use on the Analytical Platform**  
Athena database: `data_linking_anonymised`

**Linked IDs:**
- Person table (mags, Crown, prisons & probation (Delius and OASys)
- Journey table (mags & Crown cases)

**Note:** these internal tables will include new datasets before the Data First equivalents, they will be more up-to-date, and they will be refreshed more frequently.

---

### A.8 Our products — internal examples shown (queries + example columns)
**Tables for internal use on the Analytical Platform**  
Athena database: `data_linking_anonymised`

**Example query shown: `person_clusters_beta`**
```sql
SELECT *
FROM data_linking_anonymised.person_clusters_beta
ORDER BY cluster_low
LIMIT 10
````

**Example output columns shown (illustrative from slide):**

* `person_id`
* `source_dataset`
* `cluster_high`
* `cluster_medium`
* `cluster_low`

**Example query shown: `mags_crown_journey_beta`**

```sql
SELECT *
FROM data_linking_anonymised.mags_crown_journey_beta
ORDER BY cc_defendant_on_case_id
LIMIT 10
```

**Example output columns shown (illustrative from slide):**

* `estimated_match_score`
* `mc_case_id`
* `mc_defendant_id`
* `cc_defendant_on_case_id`

---

### A.9 How to get access (in 3 easy steps)

**How to get access …in 3 easy steps**

1. Go to `github.com/moj-analytical-services/data-engineering-database-access`
2. Notice that everyone already has access to `data_linking/internal` through `standard_database_access`
3. Get adding `data_linking_anonymised` database tables to your queries!

(or you can request access to the full Data First datasets or other sensitive data produced by the data linking team)

---

### A.10 Quote

“that’s awesome… literally the best thing that has ever happened to DASD”
— Karik Isichei (Lead Data Engineer)
(on giving everyone access to anonymised linked data)

---

### A.11 Using the data — Example 1: Deduplicated prison offenders

**Using the data**
Example 1: Deduplicated prison offenders

(SQL shown in the slide as a screenshot; transcribed below)

```sql
SELECT
  L.cluster_medium AS deduped_offender_id,
  N.*
FROM nomis.offender_bookings AS N

-- Join to person clusters
LEFT JOIN data_linking_anonymised.person_clusters_beta AS L
  ON CAST(N.offender_id AS varchar) = L.person_id
  AND L.source_dataset = 'prison_nomis'

WHERE N.mojap_start_datetime <= date '2021-04-01'
  AND N.mojap_end_datetime > date '2021-04-01'
LIMIT 10
```

---

### A.12 Using the data — Example 2: Linked magistrates’ / Crown court cases

**Using the data**
Example 2: Linked magistrates’ / Crown court cases

(SQL shown in the slide as a screenshot; transcribed below)

```sql
WITH mags AS (
  SELECT *
  FROM mags_curated_v2.hocas_flatfile
  WHERE mojap_snapshot_date = date '2021-05-01'
),

crown AS (
  SELECT *
  FROM xhibit_der_v1.defendant_summary
  WHERE mojap_snapshot_date = date '2021-04-28'
)

SELECT MC.*, CC.*
FROM crown CC

-- Join Crown to journey link
LEFT JOIN data_linking_anonymised.mags_crown_journey_beta L
  ON CAST(CC.defendant_on_case_id AS varchar) = L.cc_defendant_on_case_id

-- Join to mags
LEFT JOIN mags MC
  ON MC.case_id = L.mc_case_id
  AND MC.defendant_id = L.mc_defendant_id
LIMIT 100
```

---

### A.13 Support, feedback and caveats

* Please direct all questions about data linking products to `#data-linking-databases` on Slack so that others can see questions and answers.
* We very much welcome feedback.
* These tables have been designated ‘beta’, so if the format of the data causes problems for you, we may change it in response to user feedback.
* At this stage, please do not share results derived from these datasets with your customers (policy, ministers etc.) without talking to us first about caveats.

---

## Appendix B: Discovery in Data Linking Project (Sept 2025) — Discovery pack

*Converted to Markdown from “BOLD data linking discovery post feedback v1” slide pack.*
**Source files:** `BOLD data linking discovery post feedback v1.pptx`

---

### B.1 Discovery in Data Linking Project — Sept 2025

#### What is the purpose of this slide pack?

These slides introduce the idea and scope of a “discovery phase” to staff who are not from the Government Digital Service (GDS). They use some, but not all, of the language and approach of the GDS. Certain stages included here are in later stages of digital projects (Alpha stage)1.

These slides are tailored to data linking projects. They provide a practical framework for teams to follow. They explicitly include requirements to understand the data landscape that is fundamental to data linking.

These slides help clarify the roles of analysts/data science leads, policy and service design colleagues. These are flexible and can change depending on the team composition and specific team members skills. These slides are therefore a starting point for roles and responsibilities.

These slides also introduce the idea of “use cases”. Use cases are a practical tool to help achieve the aims of discovery. They are not compulsory. They are widely used in Digital projects.

1 Please see Annex A for a comparison between these slides and the GDS discovery approach.

---

### B.2 What is…….

This section explains a number of basic concepts to help understand this slide pack

#### What is data linking in BOLD?

Data linking in BOLD refers to the end-to-end process of connecting information across two or more datasets. This includes:

* Negotiating data sharing agreements.
* Technically matching records (e.g. using identifiers).
* Conducting analysis on the linked data.
* Disseminating findings for policy or operational use.

BOLD data linking can have a strategic/policy or operational focus.

**Strategic / Policy focus**

* Data linked at national or regional data to create a pseudonymised dataset for analysis.
* Can identify specific cohorts, volume of needs and demand at national and regional level.
* Provides strategic level information for better planning and managing demand.

**Operational focus**

* Data linked to provide specific professional users with data about a specific individual.
* Normally provides benefits to professional users in terms of efficiency and better decision making.
* Work on operational data linking is likely to take longer as there are more consent issues and may need to draw on local rather than national datasets due to timeliness of data.

#### What are Use Cases?

Use cases are narratives or scenarios that describe how a user interacts with a system or process to achieve a goal. They help in discovery by:

1. Clarifying User Needs - Use cases show who the users are (e.g., victims, caseworkers, police officers) and what they are trying to accomplish, and why.
2. Identifying Gaps and Pain Points - By walking through real or hypothetical scenarios, you can spot inefficiencies, risks, or unmet needs.
3. Aligning Stakeholders - Use cases create a shared understanding across teams (policy, tech, legal, frontline services) of the problem.
4. Informing Requirements - They translate abstract needs into concrete functional requirements.
5. Prioritizing Features – Use cases help determine which features or interventions will have the most impact.

Use cases are optional in discovery. If you wish to use them, please see Annex B for further advice.

#### What is a Discovery Phase and its Purpose?

The discovery phase marks the beginning of a project, focusing on collecting information, comprehending the issues at hand, and establishing the project's scope. This phase is essential as it lays the groundwork for the entire project and sets expectations.

The objectives of the discovery phase are:

* Determining the project's aims and objectives.
* Gaining insight into the needs and expectations of stakeholders.
* Collecting and evaluating pertinent data and information.
* Outlining the project scope, deliverables, finances, resources/staff, and timelines.
* Recognizing potential risks and challenges.

#### What does this mean in the Data Linking Context?

Data linking discovery phase weaves together:

* Increasing understand of user needs and the value of addressing them with
* Increasing understanding of the data landscape and availability, quality, and value of data that could potentially address these needs

Discovery brings these aspects together to identify opportunities / options arising where is an overlap of high priority user needs with the robust data available.

It sets out a decision-making process to refine, prioritise and decide what opportunities / options to take forward into deliverable projects.

GDS suggests discovery takes about 6 week. In practice, we know discovery for data linking takes longer. This is because of the need to understand unknown data landscapes, the wide scope of potential users that need to be considered and building consensus across complex, cross-department stakeholders takes time. The teams at discovery stage are often smaller. So 4-6 months is more common.

#### What Does a Successful Discovery Look Like?

The outcome of a successful discovery phase would be an agreed decision to pursue or not pursue a data linking project based on:

* Clear and well-defined project objectives and goals.
* Comprehensive understanding of stakeholder needs and expectations and the value added by the project.
* Comprehensive understanding of the relevant data landscape and its maturity to delivery the project
* Detailed and accurate documentation of requirements of the planned project.
* Identification of potential risks and mitigation strategies.
* Realistic project scope, deliverables, and timelines for the recommended option with an evaluation or benefits realisation plan
* Clarity about what the project will not cover to manage expectations
* Strong stakeholder buy-in and support.

When we have achieved these and made a decision, the discovery has been successfully completed.

Your discovery may not complete all the discovery process before a decision is made not to pursue a project. This is still a successful discovery.

---

### B.3 Stages of Discovery

This section explains the stages of discovery

#### Scope your Discovery

Before you start, decide the basic scope of your discovery. This helps you decided how wide your discovery needs to be and keeps you on track.

Consider questions such as:

* Are you scoping a data linking project or a programme?
* Will you consider operational and strategic /policy data linking areas?
* Are you focusing on specific types of data?
* Specific types of users?
* Specific types of vulnerable people?
* Are you focusing on supporting a particular Ministerial priority or recommendation?
* Who are likely to be your key stakeholders?
* Is your project likely to be small, medium or large?

Example goal:
To carry out discovery to inform a programme of work linking mental health and justice datasets. Programme is potentially large scale, multiple year. It is likely to have a mix of operational or strategic/policy data linking elements. The resulting programme must support key ministerial priority areas for both Justice and Health. Both health and justice must be co-partners.

---

### B.4 Data Linking / BOLD Discovery

1. Stakeholder Engagement is ongoing and integrated into all stages
   (Can be iterative process)

#### 1. Stakeholder Engagement

This activity is ongoing across all stages of the discovery. It is about identifying, connecting with, and meaningfully involving people who are affected by or have influence over the problem or opportunity space. This includes users, communities, delivery partners, funders, and challengers. It is less about extracting information and more about building relationships and co-creating understanding.

For Data Linking Discovery this will always involve:

* Engaging with policy and operational stakeholders and representatives of potential end users
* Engaging with data owners, data controllers, analysts, and other data users.
* Producing a stakeholder map and agreeing who leads the different types of engagement with each stakeholder with a clear communications plan

Skills: facilitation, empathy & listening, conflict mediation, excellent communication
Lead: Policy normally, service designer (if purpose is user-research or landscape mapping)
Support: Analyst

#### 2. Problem Definition

This stage is about framing the right problem before jumping to solutions or framing the opportunity before deciding if it is right opportunity to harness. It involves identifying root causes of problem or nature of the opportunity, understanding who is affected, and articulating why the issue matters. A well-defined problem or opportunity sets the direction for the rest of the discovery process.

For Data Linking Discovery this will always involve:

* Defining the core issue or opportunity in plain language.
* Understanding the cause of the problem and its relative importance to achieving Departmental / Government priorities
* Developing a theory of change on how linked data will lead to change

Skills: facilitation, critical thinking, empathy & listening, data interpretation, strategic context understanding
Lead: Co-led by Policy, Service Designer and Analyst.

#### 3. Insight Gathering

In the insight gathering stage of discovery, the focus is on gathering meaningful insights, through qualitative and quantitative evidence, ensuring an ongoing, deep understanding of the problem or opportunity. This stage should involve utilising existing data sources and expertise before exploring new data sources. For datasets this could include basic analysis of data held in trusted environments or requesting anonymised samples from data owners to assess quality and viability.

For Data Linking Discovery this will always involve:

* Detailed mapping of existing and potential datasets landscape and technical assessment of availability, quality and scope for data linking.
  Lead: Analyst
* Mapping of current system that seeking to change (and potentially new system).
  Lead: Service Designer/policy
* Engaging with those impacted by the identified problem to understand their needs and the potential value of the project outcomes.
  Lead: Service Designer/Policy

Skills: quantitative skills, qualitative / user-centre research design, evidence synthesis skills, data visualisation, critical thinking
Support: Policy

#### 4. Options/Opportunity development

This stage is about listening deeply, translating expressed and implicit needs into actionable projects and opportunities and options, and co-creating clarity. To understand what people truly need - not just what they say they want - by engaging them in meaningful, inclusive, and often creative ways. It’s about articulating what matters, why it matters, and how it fits into addressing the identified problem.

For Data Linking Discovery this will always involve:

* Engaging with policy stakeholders and end users (directly or via representatives) to consider both operational and strategic/policy uses
* Mapping emerging requirements (what matters for different end users), and explaining why it matters and its wider strategic fit
* Building on the data mapping to assess the maturity and robustness of the data, its value in addressing the emerging requirements and highlighting issues around legal and technical access to the data
* Reviewing Problem Definition to ensure still accurate and relevant

Skills: facilitation, active listening, empathy & listening, critical thinking, strategic context
Lead: Co-creation - Policy / Analyst / Service Designer

#### 5. Stress-testing the Options

The focus is on understanding whether requirements gathered can be meet in a doable, sustainable, and appropriate way. It is about drawing together all the work of the earlier Discovery stages, setting out a coherent narrative and set of strategic options.

For Data Linking Discovery this will always involve a report covering:

* Strategic, policy and resource fit of the options with BOLD, MOJ and government priorities
* assessment of the quality and value of the existing data and its expected impact on the robustness of the expected linked data for each option
* assessment of expected deliverability within the time and resources available
* the value of the expected linked dataset outcomes to the end user and to vulnerable people’s outcomes, including, if appropriate, the value of reducing uncertainty of the evidence to users

Skills: critical thinking, project planning and management. Strategic context
Lead: Co-creation - Policy / Analyst / Service Designer

#### 6. Scope Definition and Planning

The focus is on the preferred option identified though stress-testing and collaboratively deciding what to explore, how to explore it, and what success might look like, setting direction without locking down solutions. It’s about making a plan that people believe in and can act on.

For Data Linking Discovery this will always involve:

* Producing a project scope with clear requirements and expected outputs and outcomes that align with operational and policy priorities with a deliverable plan showing expected resource allocation.
* Clear plan for evaluation and/or benefits tracking
* Ensuring there is a clear customer owner for the project and any cross-government customers have been fully identified

Skills: critical thinking, project planning and management, influencing
Lead: Co-creation - Policy / Analyst / Service Designer

#### 7. Decision Point

The focus is on making a shared, informed, and ethical decision about whether to proceed, pivot, pause, or stop. This moment is as much about alignment and reflection of the value of the requirements as it is about the deliverability of the project.

For Data Linking Discovery this will always involve:

* Ensuring senior decisions makers are clear on proposed project(s), its requirements, outputs, outcomes, resources (finance and staff), timeline and risks – and, critically, its value to BOLD and MOJ priorities
* Ensuring senior decision makers are clear on what is not included in the project
* Ensuring the views of people impacted by the work are central to the decision making
* If required, finalising the REAP process including quality oversight before commencing the project

Skills: facilitation, critical thinking, consensus building
Lead: Co-creation - Policy / Analyst / Service Designer

---

### B.5 Team Roles

This section explains the team roles for various professions during discovery

#### Team Leaders

All team leaders will:

* Have the opportunity to be the overall lead on discovery projects
* Actively provide expert advice, skill and support to their colleagues at appropriate points
* Ensure all work is tailored to end users’ needs and aligned with BOLD and MOJ priorities
* Ensure that lived experience and systems thinking, robust evidence and practical policy making are central to our projects
* Co-create across the option development, stress-testing, scope definition and planning in support of the Discovery lead

#### Policy Advisors

Policy advisors will…

* Lead on stakeholder engagement (except vulnerable users) and stakeholder mapping, including delegating on-going stakeholder liaison to service designers and analysts as appropriate
* Lead on Discovery where proposal has high policy or culture change focus
* Ensure there is a clear customer for all proposals including consideration of cross-government customers if appropriate
* Ensure that the communications for the aims of data linking projects are clear, consistent and persuasive
* Identify and use levers to influence enablers for the projects, including data holders and data sharing
* Lead on ensuring outputs are used by appropriate end users.

#### Analysts and Data Scientists

Analysts /Data Scientists will…

* Lead on quantitative, qualitative and evaluation research and analysis, and supporting evidence gathering with users
* Lead on mapping datasets, assessing maturity and quality and value if linked
* Lead on Discovery where proposal has high levels of analytical or data linking focus, including REAP if appropriate
* Understand and examine the technical elements of data sharing, data linking and any other techniques to be used
* Lead on evaluating use of outputs.

#### Service Designers

Service designer will…

* Lead on direct user engagement
* Lead on user-centered research and analysis with vulnerable users and mapping of current system
* Lead on Discovery where proposal has a high service design, user-centred design or prototyping focus
* Support analysts / data scientists to visualise the data that is available and make it easy-to-understand for non-data literate teams
* Support policy to run workshops with key stakeholders to consolidate existing insights and evidence gaps if appropriate

---

### B.6 Annexes (from the slide pack)

#### Annex A: Comparison with GDS Discovery

* Scope Differences in Discovery: BOLD includes option development and stress-testing during Discovery, whereas GDS defers these to Alpha phase.
* Operational Planning Emphasis: BOLD emphasizes finances, timelines, and resource allocation early in Discovery, unlike GDS which delays these to Alpha.
* Language and Team Roles: BOLD uses delivery-focused, prescriptive language defining team roles; GDS focuses on flexibility and understanding user needs.
* Stakeholder and Communications Planning: BOLD includes detailed stakeholder mapping and communications plans, which are less explicit in GDS Discovery.

The GDS guidance is sourced from the UK Government Service Manual (How the discovery phase works - Service Manual - GOV.UK).

#### Annex B: Use Cases in Discovery (1)

These slides provides a practical approach for developing and refining use cases throughout the discovery process. It is designed to complement the Data Linking discovery pack by embedding user-centred examples at every stage.

**What are Use Cases?**
Use cases are short, structured scenarios that illustrate how a user (e.g., a service user, service provider, or policymaker) experiences a system, policy, or service. They make abstract needs and options tangible by showing real-world interactions and outcomes.

**Structure of a Use Case**
Each use case should be concise (½–1 page) and include:

* User Persona / Actor – Who is the main user (e.g., 'victim of domestic abuse', 'local authority officer').
* Trigger / Situation – What starts the interaction (e.g., reporting an incident, linking data).
* Steps / Interaction – What happens step by step.
* Desired Outcome – What success looks like from the user’s perspective.
* System / Policy Requirements – Conditions needed for this use case to work.

#### Annex B: Use Cases in Discovery (2)

OPERATIONAL FOCUS
STRATEGIC / POLICY FOCUS

Examples of Use Cases

#### Annex B: Use Cases in Discovery (3)

When to Develop Use Cases in Discovery

#### Annex B: Use Cases in Discovery (4)

How to Build Use Cases Collaboratively

* Run workshops with victims’ representatives, service designers, and analysts to co-create scenarios.
* Use storytelling, journey mapping, or prototyping tools to make cases vivid and engaging.
* Cross-check cases against data and policy constraints to ensure realism and feasibility.
* Iterate continuously – refine use cases as new insights emerge during discovery.

```
::contentReference[oaicite:0]{index=0}
```
<!-- END FILE: data_linking_Splink_Discover.md -->

---
