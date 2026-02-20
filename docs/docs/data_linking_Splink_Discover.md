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
