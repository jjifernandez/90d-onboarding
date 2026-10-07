# Meeting logs

Notes and action items from onboarding meetings. Newest entries go at the top.

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


