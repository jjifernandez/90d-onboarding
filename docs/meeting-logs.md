# Meeting logs

Notes and action items from onboarding meetings. Newest entries go at the top.

## 2026-10-07: Joey / Juanjo 1:1

**When:** Wednesday, October 7, 2026, 12:00 PM CDT  
**Attendees:** Joey Rahman, Juan Jose Iguaran Fernandez (Juanjo)

### Meeting goals & context

- Juanjo proactively set up the 1:1 with two main objectives:
  1. Determine how to move forward with the shared behavioral operations repository after encountering AWS configuration and secrets blockers.
  2. Plan and prepare for the upcoming four-person alignment meeting (Joey, Juanjo, John, Derick) to define the ML problem.

### Behavioral operations pipeline and ML architecture

- **Repository path forward:** Joey confirmed the behavioral operations repository is still the intended path and will push for it. The immediate priority before writing code (Python/Terraform) or debugging secrets is securing alignment and buy-in on the architecture.
- **Data governance and permissions:** Addressed Carl's question regarding customer permissions. Joey clarified that no new data processors are being introduced; Localytics is already authorized to store and process data in AWS (`us-west-2`) and Snowflake.
- **Architectural specifications to document:**
  - **Storage & isolation:** Data resides in an S3 bucket in AWS Region `us-west-2`, distinct from Snowflake's existing storage bucket (kept in the same AWS production account for simplicity).
  - **Feature engineering compute:** Feature engineering runs on Snowflake compute against the production `fact_events` table using SQL; outputs are stored as Parquet files in the S3 data lake.
  - **No Lambda:** No AWS Lambda functions will be used; the SageMaker API manages training jobs directly.
  - **External tables:** Feature tables in S3 are registered as Snowflake external tables, allowing both Snowflake SQL queries and SageMaker training jobs to access the Parquet datasets directly.
  - **Model training & registry:** SageMaker provisions instances to execute training jobs (e.g., XGBoost) and manages its own model registry for artifacts (weights, biases, JSON metadata).
- **Deliverable:** Juanjo will write an architecture document with a detailed Mermaid diagram in a new Markdown file (Cursor / AI can be used). Target completion: **Friday, October 9, 2026**.

### Problem framing: Free-to-paid conversion

- **Target prediction:** Probability that a user converts from a free trial / license to a paid subscription.
- **Scope & parameters to define:**
  - Prediction horizons (e.g., 7-day, 10-day, or 30-day window).
  - Cohort definitions and trial duration thresholds (e.g., users in trial for a month vs. newer users).
- **Defended position:** Juanjo to draft 5–6 distinct problem descriptions, select the strongest recommendation, and defend it.
  - Slack the options to Joey before the group meeting for pre-review.
  - Come prepared with a concrete proposal rather than asking John or the customer to define the ML problem, as customers lack ML expertise to formulate technical parameters.

### Success metrics and model performance

- **Dream model definition:** Define what a successful model looks like in advance.
- **Evaluation metrics:** Specify performance metrics (e.g., precision and recall) and target benchmark scores representing high performance.
- **Out-of-Time (OOT) validation:** Adopt an OOT rolling-window validation approach (e.g., train on ~3 months of historical behavioral data, predict on the subsequent 7-day window).

### Group alignment meeting & presentation prep

- **Meeting scheduling:** Juanjo to schedule a four-person alignment sync with Joey Rahman, Juan Jose Iguaran Fernandez, John Dobrowolski, and Derick Thompson.
- **Presentation structure:** Morning NutraCheck data briefing went well. For the leadership meeting, do not present all exploratory slides; instead, extract a 4–5 slide "highlights reel" focused on CEO-relevant metrics (e.g., MAUs, app opens) followed by the ML proposal:
  1. Customer data summary (highlights reel: 4–5 slides on MAUs, app opens, engagement)
  2. Problem framing (recommended option from the 5–6 framed)
  3. Model performance metrics & success definition (precision/recall targets)
  4. Architecture diagram & data flow (Mermaid diagram with region, S3 bucket separation, approved processors)

### Next steps

- [ ] Draft architecture documentation with a Mermaid diagram in a new `.md` file detailing AWS `us-west-2`, S3 bucket separation from Snowflake, Snowflake compute feature engineering, external tables, and SageMaker training (Juanjo - target: Friday, Oct 9)
- [ ] Formulate 5–6 ML problem descriptions for free-to-paid conversion with specific horizons/thresholds and select a recommended option (Juanjo)
- [ ] Share problem framing options with Joey on Slack for pre-review ahead of the group meeting (Juanjo)
- [ ] Select 4–5 CEO-level highlight slides (MAUs, app opens) from NutraCheck data exploration (Juanjo)
- [ ] Schedule four-person alignment meeting with Joey, John, and Derick (Juanjo)
- [ ] Pre-review Juanjo's ML problem framing options on Slack (Joey)
- [ ] Assist Juanjo in securing team and leadership buy-in for the behavioral operations pipeline architecture (Joey)

## 2026-09-30: Juanjo / Joey

**When:** Wednesday, September 30, 2026, 3:30 PM CDT  
**Attendees:** Joey Rahman, Juan Jose Iguaran Fernandez (Juanjo)

### Product leadership departure and Predictions API ownership

- Juan (Head of Product) has left the company.
- Joey will now closely manage the Predictions API and work directly with Juanjo on its roadmap and execution.
  - Derick is available for data model questions as needed.
- Joey will work with John starting next week (after returning from PTO on Tuesday) to draft the Head of Product job description.

### Predictions API vision and use cases

- **Core vision:** Enable Localytics customers to make AI/ML-informed decisions to improve revenue, retention, or end-user engagement.
- **Rollout architecture:**
  - Build as a standalone API first.
  - Integrate into the existing dashboard and profiles system by enriching end-user profiles with churn probability, optimal send time windows, and current message fatigue levels.
  - Longer term: export prediction data into customer CRMs (in coordination with Yenifer Hernandez as FDE).
- **Concrete use cases discussed:**
  - **Send time window:** Determine optimal time of day / day of week for scheduled campaign delivery.
  - **Low-engagement targeting:** Identify chronically inactive users (who haven't engaged in months) and target them with re-engagement campaigns; message-fatigue risk is minimal for these users.
  - **Preferred channel prediction:** Predict whether push, inbox, SMS, or email yields higher conversion/ROI (e.g. for friend referral discounts).

### NutraCheck presentation prep

- Juanjo built a draft presentation deck using Claude based on NutraCheck data, structured in three parts:
  1. **Data structure:** Key tables, schema, joins, event attributes, and table sizes.
  2. **Users and profiles:** Monthly Active Users (MAUs) for iOS and Android, cross-app overlap, membership status, and customer profiles.
  3. **Event taxonomy:** 225 iOS events, 205 Android events, event categorization, and top migration queries.
- **Joey's feedback on the deck:**
  - Remove AI-specific content and focus on actionable analytics.
  - Frame it from an engineering-focused perspective: What is NutraCheck doing? What does their event data show? Is there anything notable about their audience/end users?
  - Include an RFM (Recency, Frequency, Monetary) analysis of typical end users.
- **Rescheduling:** Tuesday (Oct 6) is too packed; rescheduled presentation to **Wednesday, October 7, 2026**.

### AI tooling and Snowflake access rules

- Direct Claude access to Snowflake is strictly prohibited.
- Claude can be used to generate queries or format exported data, but cannot query Snowflake directly.
- All direct Snowflake queries via Cursor agent must use Snowflake's native **Cortex** tool. Joey shared the setup link for adding Cortex to the Cursor agent.

### Next steps

- [ ] Refine NutraCheck presentation deck: remove AI content, add engineering takeaways, and include RFM analysis (Juanjo)
- [ ] Add Cortex to Cursor agent for Snowflake queries instead of direct Claude access (Juanjo)
- [ ] Schedule NutraCheck presentation for Wednesday, October 7 (Juanjo / Joey)
- [ ] Draft Head of Product job description with John starting Tuesday (Joey)
- [ ] Closely manage Predictions API vision and execution with Juanjo (Joey)


