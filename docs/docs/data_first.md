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

## Additional OASys metadata: variables and tables for outcomes 5–8

**Source:** `OASys_ONS_data_catalogue_NOV25_External.ods`  
**Where in the metadata:** `OASys_ONS_data_catalogue_NOV25_External.ods` → **`data_dictionary`** tab  
**Key columns to use:** **Table Name**, **Variable Name**, **Variable Description**, **Values (optional)**  
*(This section extends the earlier outcomes 1–4 mapping.)*

---

## 5) Housing insecurity (poverty / homelessness)

### Primary OASys tables to use
- **`oasys_assessments_details_core_risk`** — Accommodation section (**Section 3**) is captured as `question_3_*`
- **`oasys_assessments_details_bcs`** — Basic custody screening (accommodation before prison, housing benefit, accommodation problem flags)
- **`oasys_assessments_details_tr_bcs`** — Transfer/basic custody screening (tenancy/rental issues + accommodation need flags)
- **`oasys_assessments_details_rmp`** — Contains a field referencing accommodation considerations (useful as a supporting flag)

### Confirmed variables in the catalogue (Accommodation)
| Table | Variable | What it captures (from the metadata description) | Values (optional) |
|---|---|---|---|
| `oasys_assessments_details_bcs` | `question_bcs33` | Offender’s accommodation status before prison | Coded categories incl. permanent/temporary/rough sleeping (see catalogue) |
| `oasys_assessments_details_bcs` | `question_bcs36` | Type of accommodation lived in before prison | Coded categories (council/HA/private/other; see catalogue) |
| `oasys_assessments_details_bcs` | `question_bcs37` | Suitability of accommodation before prison | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs38` | Claiming housing benefit | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs39` | Has somewhere to live on release (description begins “Has the Offender got somewhere to live when th…”) | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs43` | Accommodation is a problem issue | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_3_1_1` | Records details of type of accommodation | Coded categories (see catalogue) |
| `oasys_assessments_details_core_risk` | `question_3_1_2` | Accommodation status | `CURRENT = …` / `PLANNED = …` (see catalogue) |
| `oasys_assessments_details_core_risk` | `question_3_3` | No fixed abode flag (description begins “currently of no f…”) | `NO/YES` (plus `M = Missing`, see catalogue) |
| `oasys_assessments_details_core_risk` | `question_3_4` | Living in suitable accommodation | `0/1/2` scale (No/Some/Significant problems + `M`) |
| `oasys_assessments_details_core_risk` | `question_3_5` | Permanence/stability issues (description begins “issues with perm…”) | `0/1/2` scale (+ `M`) |
| `oasys_assessments_details_core_risk` | `question_3_6` | Suitability of accommodation location | `0/1/2` scale (+ `M`) |
| `oasys_assessments_details_core_risk` | `question_3_98` | Accommodation issues linked to risk/needs (flag) | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_3_99` | Accommodation issues linked to offending behaviour (flag) | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_3_tot` | Total score for Section 3 — Accommodation | `0 - 8` |
| `oasys_assessments_details_tr_bcs` | `question_tr_bcs309` | Tenancy or rental issues | `NA = Not Applicable` / `NO` / `YES` |
| `oasys_assessments_details_tr_bcs` | `question_tr_bcs33` | Accommodation status on reception | Category codes incl. permanent/temporary/NFA (see catalogue) |
| `oasys_assessments_details_tr_bcs` | `question_tr_bcs37` | Accommodation before prison suitability | `N/A` / `NO` / `YES` |
| `oasys_assessments_details_tr_bcs` | `question_tr_bcs38` | Claiming housing benefit | `DK` / `NO` / `YES` |
| `oasys_assessments_details_tr_bcs` | `question_tr_bcs43` | Accommodation needs / issues (flag) | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_rmp` | `question_rmp_28_0_3_1` | Accommodation taken into account (description begins “taken into account acco…”) | `YES` |

### How to find more housing variables
In `data_dictionary`:
- Filter **Table Name = `oasys_assessments_details_core_risk`** and search **Variable Name contains `question_3_`**
- Search **Variable Description** for: `accommodation`, `no fixed abode`, `tenancy`, `rental`, `housing benefit`, `NFA`, `homeless`

---

## 6) Low income (and debt)

### Primary OASys tables to use
- **`oasys_assessments_details_core_risk`** — Financial management & income (**Section 5**) is captured as `question_5_*`
- **`oasys_assessments_details_bcs`** — custody screening flags for income/benefits/bank account/finance problems
- **`oasys_assessments_details_saq`** — self-assessment items including debt-related prompts
- **`oasys_assessments_details_skillschecker`** — confidence with money management
- **`oasys_assessments_details_tr_bcs`** — limited finance flags (e.g., housing benefit; “gets money every week”)

### Confirmed variables in the catalogue (income/finance)
| Table | Variable | What it captures (from the metadata description) | Values (optional) |
|---|---|---|---|
| `oasys_assessments_details_bcs` | `question_bcs45` | Offender has an income | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs46` | Offender has a pension | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs47` | Offender has any private income | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs48` | Partner has an income | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs49` | Financial family support | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs52` | Receives income support | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs53` | Other finance in receipt of | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs55` | Has a bank account | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs56` | Finance is a problem issue | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_5_1` | Main source of income before custody | Coded list incl. wages/benefits/loans/no income (see catalogue) |
| `oasys_assessments_details_core_risk` | `question_5_2` | Problems with financial situation | `0/1/2` scale (+ `M`) |
| `oasys_assessments_details_core_risk` | `question_5_3` | Financial management problems | `0/1/2` scale (+ `M`) |
| `oasys_assessments_details_core_risk` | `question_5_4` | Problems with illegal earning as income source | `0/1/2` scale (+ `M`) |
| `oasys_assessments_details_core_risk` | `question_5_5` | Over-reliance on others for financial support | `0/1/2` scale (+ `M`) |
| `oasys_assessments_details_core_risk` | `question_5_98` | Financial issues linked to RoSH/risks/needs | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_5_99` | Financial issues linked to offending behaviour | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_5_tot` | Total score for Section 5 — Financial Management & Income | `0 - 9` |
| `oasys_assessments_details_core_risk` | `question_2_9_financial` | Financial motivator for offending (flag) | `YES` |
| `oasys_assessments_details_core_risk` | `question_2_9_v2_financial` | v2 financial motivator (flag) | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_saq` | `question_saqc20_1` | Debt-related SAQ problem flag (description begins “Indicates if the following is a problem for th…”) | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_saq` | `question_saqc20_2` | Debt-related SAQ linked-to-offending flag (description begins “Indicates if this problem is linked to the off…”) | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_skillschecker` | `question_sc8` | Confidence handling money (description begins “feels confident in h…”) | Ordered categories (see catalogue) |
| `oasys_assessments_details_tr_bcs` | `question_tr_bcs45` | Gets money every week | `NO = No` / `YES = Yes` |

### How to find more low-income/debt variables
In `data_dictionary`:
- Filter **Table Name = `oasys_assessments_details_core_risk`** and search **Variable Name contains `question_5_`**
- Search **Variable Description** for: `income`, `benefit`, `bank`, `money`, `finance`, `loan`, `debt`

---

## 7) Substance misuse

### Primary OASys tables to use
- **`oasys_assessments_details_core_risk`** — Drugs misuse section (**Section 8**) is captured as `question_8_*` (incl. drug-specific frequency/current/previous use)
- **`oasys_assessments_details_bcs`** — screening flags for alcohol/drug problems, injecting history, main drug, maintenance programme
- **`oasys_assessments_details_tr_bcs`** — additional screening flags (where present)
- **Lookup sheet:** **`drug_lookup`** tab in the same ODS (maps drug codes used in some questions)

### Confirmed variables in the catalogue (substance misuse)
| Table | Variable | What it captures (from the metadata description) | Values (optional) |
|---|---|---|---|
| `oasys_assessments_details_bcs` | `question_bcs81` | Current substance/drug problem (description begins “current proble…”) | `0/1/2` scale (No/Some/Significant problems + `M`) |
| `oasys_assessments_details_bcs` | `question_bcs82` | Alcohol is a problem area | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs84` | Ever misused drugs (description begins “ever mi…”) | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs86` | Ever injected drugs (description begins “ever in…”) | `0 = Never / 1 = Previously / 2 = Current / M = Missing` |
| `oasys_assessments_details_bcs` | `question_bcs87` | Main drug used (coded) | Code list (see catalogue; uses drug codes) |
| `oasys_assessments_details_bcs` | `question_bcs88` | Drug-related concern flag (description begins “ever had any con…”) | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_bcs` | `question_bcs90` | On drug maintenance programme | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_8_1` | Ever misused drugs | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_8_2_*` | Drug-specific questions (Heroin/Methadone/Opiates/Crack/Cannabis/Ecstasy/Spice/etc.) | Frequency + current/previous use flags (see catalogue) |
| `oasys_assessments_details_core_risk` | `question_2_10_alcho` | Alcohol acted as a disinhibitor at offence | `YES` |
| `oasys_assessments_details_core_risk` | `question_2_10_drugs` | Drugs acted as a disinhibitor at offence | `YES` |
| `oasys_assessments_details_core_risk` | `question_2_9_addiction` | Addiction/perceived needs motivator | `YES` |
| `oasys_assessments_details_core_risk` | `question_2_9_v2_addiction` | v2 addiction/perceived needs motivator | `NO = No` / `YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_13_3_9_1` / `question_13_3_9_2` / `question_13_3_9_3` | Alcohol misuse affects risk/needs (grouped flags) | `YES` |
| `oasys_assessments_details_core_risk` | `question_13_3_10_1` / `question_13_3_10_2` / `question_13_3_10_3` | Drugs misuse affects risk/needs (grouped flags) | `YES` |
| *(ODS lookup)* | *(sheet)* `drug_lookup` | Drug code → drug name mapping used by coded questions (e.g. main drug used) | Lookup table |

### How to find more substance misuse variables
In `data_dictionary`:
- Filter **Table Name = `oasys_assessments_details_core_risk`** and search **Variable Name contains `question_8_`**
- Search **Variable Description** for: `drug`, `alcohol`, `inject`, `misuse`, `addiction`, `maintenance`, `treatment`

---

## 8) Offending

### Primary OASys tables to use
- **`oasys_assessments_details_core_risk`** — Offending history and offending behaviour sections are captured as `question_1_*` and `question_2_*`
- **`oasys_assessments_details_bcs`** — custody screening includes conviction timing and related offence history indicators (e.g., age at first conviction, court appearances)
- **`oasys_assessments_metadata`** — assessment-level metadata (useful for time-stamping, sentence/assessment context)

### Confirmed variables in the catalogue (offending history/behaviour examples)
| Table | Variable | What it captures (from the metadata description) | Values (optional) |
|---|---|---|---|
| `oasys_assessments_details_bcs` | `question_bcs24` | Number of court appearances at which convicted (description begins “Number of court appearances…”) | `0 - 99` |
| `oasys_assessments_details_bcs` | `question_bcs25` | Number of court appearances at which convicted (description begins “Number of court appearances…”) | `0 - 99` |
| `oasys_assessments_details_bcs` | `question_bcs28` | Age at first conviction | `0 - 99` |
| `oasys_assessments_details_core_risk` | `question_1_10` | Number of previous custodial sentences | `0 - 9` |
| `oasys_assessments_details_core_risk` | `question_1_10_1` | Weighted score for previous custodial sentences | `0/1/2` (see catalogue) |
| `oasys_assessments_details_core_risk` | `question_1_11` | Breaches indicator | `0 = No / 2 = Yes` |
| `oasys_assessments_details_core_risk` | `question_1_12` | Number of categories of offences/convictions | `0 - 9` |
| `oasys_assessments_details_core_risk` | `question_1_12_1` | Weighted score for categories of offences/convictions | (see catalogue) |
| `oasys_assessments_details_core_risk` | `question_1_29` | Date of current conviction | `YYYY-MM-DD` |
| `oasys_assessments_details_core_risk` | `question_2_11` | Accepts responsibility (description begins “accepts respons…”) | `NO = No / YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_2_13` | Escalation flag (description begins “escal…”) | `NO = No / YES = Yes` |
| `oasys_assessments_details_core_risk` | `question_2_14` | Pattern flag (description begins “part o…”) | `NO = No / YES = Yes` (plus missing codes where present) |
| `oasys_assessments_details_core_risk` | `question_2_2_weapon` | Offence involved a weapon | `YES` |
| `oasys_assessments_details_core_risk` | `question_2_3_physicalviol` | Offence involved physical violence | `YES` |
| `oasys_assessments_details_core_risk` | `question_2_3_directcont` | Offence involved direct victim contact | `YES` |
| `oasys_assessments_details_core_risk` | `question_2_3_repeatvict` | Repeat victimisation indicator | `YES` |
| `oasys_assessments_details_core_risk` | `question_2_3_resptovictim` | Response to victim indicator | `YES` |

### How to find more offending variables
In `data_dictionary`:
- Filter **Table Name = `oasys_assessments_details_core_risk`**
- Search **Variable Name contains `question_1_`** (offending history) and `question_2_` (offending behaviour)
- Search **Variable Description** for: `offence`, `offending`, `conviction`, `breach`, `custodial`, `sanction`, `weapon`, `violence`, `victim`, `escalation`, `pattern`

---
