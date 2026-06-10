# 👥 Corporate Human Resources Analytics & Workforce Planning Dashboard

![Dashboard Preview](dashboard_preview.png)

---

## 🚨 1. The Business Problem & Origin Story
An enterprise human resource department managing a large workforce lacks centralized, dynamic visibility into key corporate talent metrics. Leadership is struggling with three main visibility blind spots: uncoordinated succession planning (who is due for a promotion vs. overdue), unmonitored overtime burnout risks, and an unmapped retirement pipeline. Relying on static monthly reporting makes it impossible to proactively address staffing shortages or balance organizational diversity quotas.

To solve this, **I engineered a relational HR dataset from scratch using Microsoft Excel, ingested it into an SQL Server database to perform preliminary data transformation queries, and modeled the pipeline into Power BI Desktop** to create a fully interactive corporate human resource command center.

---

## 🎯 2. What Is Expected? (Strategic KPI Metrics)
The control center is engineered with high-contrast, large-format indicators providing executive leadership with an instantaneous summary of workforce status:

*   **Total Headcount Tracking (Current Value: 1,470):** Establishes the operational personnel baseline across all regions.
*   **Gender Diversity Matrix (Current Value: 60% Male / 40% Female):** Tracks internal diversity benchmarks dynamically against corporate inclusion targets.
*   **Succession Pipeline (72 Due for Promotion / 1,398 Not Due):** Highlights internal advancement pipelines to prevent stagnation and maintain healthy career path trajectories.
*   **Retirement Risk Profiling (1,465 Active / 5 Should Retire):** Isolates imminent retirement events (age 60 and over) to proactively manage succession planning before critical institutional knowledge leaves the organization.

---

## 🛠️ 3. Action Taken: What I Did & How
I established a clean star-schema configuration and developed explicit analytical measures using **DAX (Data Analysis Expressions)** to ensure rapid filtering calculations across multiple dimensions:

### 💻 Primary DAX Formulas Implemented

#### A. Total Headcount Base Measure
Calculates active employee density across all organizational tiers.
```dax
Total Emp = COUNTROWS('HR Analytics Data')
```

#### B. Subsection Succession Profiling
Determines the raw count and proportion of staff matching strict enterprise promotion criteria.
```dax
Due for Promotion = CALCULATE([Total Emp], 'HR Analytics Data'[Promotion Status] = "due for promotion")

% Due for promotion = DIVIDE([Due for Promotion], [Total Emp], 0)
```

#### C. Retirement & Attrition Pipeline
Identifies senior personnel reaching the mandatory retirement threshold (Age >= 60).
```dax
Count Must Retire = CALCULATE(COUNT('HR Analytics Data'[Retirement status]), 'HR Analytics Data'[Retirement status] = "Must retire")

% Must Retire = DIVIDE([Count Must Retire], [Total Emp], 0)
```

#### D. Workplace Burnout & Sentiment Metrics
Aggregates high-impact sentiment factors, tracking high-satisfaction rates (score >= 3) alongside intensive overtime assignments.
```dax
% Satisfaction = DIVIDE(CALCULATE(COUNT('HR Analytics Data'[JobSatisfaction]), 'HR Analytics Data'[JobSatisfaction] >= 3), COUNT('HR Analytics Data'[JobSatisfaction]), 0)

% Overtime = DIVIDE(CALCULATE(COUNT('HR Analytics Data'[OverTime]), 'HR Analytics Data'[OverTime] = "Yes"), COUNT('HR Analytics Data'[OverTime]), 0)
```

---

## 🎛️ 4. Dynamic Data Filtering & Slicing
To allow HR partners to pivot instantly between disparate operational requirements, the dashboard utilizes a modular, high-impact control layer:

*   **Job Roles Master Filter:** A universal dropdown containing **9 distinct job classifications**. Clicking any role immediately re-filters all metrics across the screen, adapting the seniority chart, service years distribution, and distance-from-work profile for that segment.
*   **Segmented Service Clusters:** Bar charts grouping staff by exact tenure (ranging from 1 year up to 10 years) to analyze localized retention.
*   **Job Level Tiering:** A structural bar chart breaking down headcount from Entry Level (Level 1) to Senior Executive (Level 5) to instantly isolate organizational hierarchy blocks.

---

## 💡 5. Executive Outcomes: Driving Insightful Decisions
This model transforms HR management from an administrative support team into a proactive strategic partner:

*   **Preventing Burnout Flight Risks:** By filtering for highly demanding roles, leadership can cross-reference the **28.30% Overtime Rate** against the **61.29% Job Satisfaction Score**. If satisfaction drops while overtime climbs, HR can intervene with wellness initiatives or expand hiring budgets to prevent costly voluntary turnover.
*   **Targeted Training Interventions:** Rather than launching expensive, company-wide training programs, executives can look at the **Job Levels chart (543 Level 1 / 534 Level 2)** and direct professional development budgets explicitly to lower tiers where career stagnation typically causes the highest attrition.
*   **Targeted Succession Planning:** The dashboard calls out exactly **5 individuals** who have reached mandatory retirement age (`0.34%` of the workforce). Instead of waiting for an unannounced departure, management can look at the **72 employees due for promotion** to immediately choose, train, and place internal candidates into those open leadership roles.

---

## ♿ Inclusive Design & Accessibility Features
*   **Visual-Strain Reduction:** Built on a clean, soft-grey layout (`#F3F2F1`) with prominent white card enclosures, reducing sensory strain during deep-dive analytical reviews.
*   **Oversized Typography:** Data indicators use crisp **36pt Bold** values, paired with high-contrast **True Black (`#000000`)** textual category headers to maximize screen scannability.
