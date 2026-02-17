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
