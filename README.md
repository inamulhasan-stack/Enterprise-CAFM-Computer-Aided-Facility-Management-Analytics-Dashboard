# 🏢 Enterprise CAFM — Computer-Aided Facility Management Analytics Suite

> **Domain:** Facilities Management (FM) | Computer-Aided Facility Management (CAFM)  
> **Platform:** Microsoft Power BI Desktop (Enterprise Suite)  
> **Dataset:** `CAFM_Master_Enterprise_Dataset_500.csv` (500 Master Service Requests)  
> **Author:** Inamul Hasan  

---

## 📌 Project Overview

This project delivers an enterprise-grade, five-page **CAFM Power BI Dashboard Suite** designed to provide deep operational, financial, and performance insights for executive decision-making across Dubai and UAE property portfolios. 

The dashboard models industry-standard FM metrics—including **SLA Compliance**, **First-Time Fix Rate (FTFR)**, **Technician Workload Balancing**, and **Maintenance Cost Analysis**—transforming raw work-order logs into actionable business intelligence.

---

## 📸 System Screenshots & Dashboard Suite Proofs

📍 Page 1: Executive Operations Overview

Visual Architecture & Layout:
Designed for C-suite and Operations Directors. The top KPI banner delivers an instant operational health check. The center left features a Ticket Status Donut Chart (Open, WIP, Pending, Closed percentages), paired on the right with a Property Volume vs. Total Maintenance Cost Combo Chart to isolate budget burn per asset. The bottom full-width chart monitors monthly creation vs. resolution velocities over time.

Key Metrics Displayed:
- Total Tickets: 500
- SLA Compliance: 38.97%
- Avg Resolution Duration: 7.58 Hours
- Active Backlog Work Orders: 210
- Total Portfolio Spend: 148,314 AED

![Executive Operations Overview](01_executive_operations_overview.png)

📍 Page 2: SLA & Priority Performance Analytics

Visual Architecture & Layout:
Focuses on SLA contract compliance and priority response times. Features a Target SLA Compliance Gauge Chart (0–100% scale with a 90% target benchmark needle) positioned next to a Priority Matrix Table detailing Low, Medium, High, and Critical target hours against actual execution speed. The bottom chart breaks down SLA status (Met, Breached, In-Progress) across all 10 maintenance categories.

Key Metrics Displayed:
- Critical SLA Met %: 41.94%
- First-Time Fix Rate (FTFR): 71.72%
- Repeat Call Rate: 28.28%
- Overdue Backlog: 0

![SLA & Priority Performance Analytics](02_sla_priority_performance.png)

📍 Page 3: Property Maintenance & Cost Deep-Dive

Visual Architecture & Layout:
Delivers total financial transparency across the facility portfolio. A horizontal Hard vs. Soft Services Stacked Bar Chart compares physical infrastructure spend (HVAC, Plumbing, BMS) against facility support spend (Cleaning, Pest Control) for every asset. A Scatter Plot Matrix maps ticket volume against total cost to isolate expensive property outliers (JVC Mulberry Suites), anchored by a Department Cost Bar Chart at the bottom.

Key Metrics Displayed:
- Average Cost per Ticket: 296.63 AED
- Hard Services Budget Burn: 117.09K AED
- Soft Services Budget Burn: 31.22K AED
- Highest Spend Property: JVC Mulberry Suites

![Property Maintenance & Cost Deep-Dive](03_property_maintenance_cost.png)

📍 Page 4: Resource, Technician & Helpdesk Efficiency

Visual Architecture & Layout:
Tailored for helpdesk supervisors and engineering resource managers. Features a top KPI band for technician workload statistics, followed by a Technician Combo Chart (Closed Ticket volumes as columns overlayed with individual SLA compliance lines). A comprehensive Technician Performance Matrix Table tracks individual metrics (Assigned Work orders, FTFR %, Overdue Backlog, Repeat Call %, SLA %, and Resolution Speed).

Key Metrics Displayed:
- Active Field Technicians: 7
- Average Tickets per Tech: 71.43
- Average CSAT Score: 4.20 / 5.00
- PPM Compliance Rate: 92.50%

![Resource, Technician & Helpdesk Efficiency](04_resource_technician_efficiency.png)

📍 Page 5: Key Findings & Executive Recommendations

Visual Architecture & Layout:
An executive strategic summary canvas that translates technical dashboard data into clear business advisory cards for management decision-making.

Strategic Insights & Action Items:
- Overall SLA Compliance Deficit: SLA compliance sits at 38.97%, significantly below the enterprise benchmark of 90%+.
  * Recommendation: Implement real-time automated helpdesk escalation alerts when tickets reach 50% of target SLA duration.
- Critical Ticket Response Paradox: Critical tickets reach an average repair time of 1.28 hours (well within the 2.0-hour target), yet only 41.94% meet overall SLA compliance due to initial helpdesk dispatch delays.
  * Recommendation: Redesign helpdesk dispatch protocols to auto-assign Critical tickets instantly, bypassing manual queues.
- Active Backlog Accumulation: 210 tickets (42%) remain trapped in active status (In Progress), creating high future breach risk.
  * Recommendation: Execute weekly backlog clearing sprints and temporarily reallocate floating engineering capacity.
- Resource Bottleneck & Workload Strain: Field technician Karthik Nair carries the highest workload (75 tickets) but suffers the lowest SLA compliance (27.66%) and longest resolution times (9.61 hours).
  * Recommendation: Rebalance automated ticket assignment rules evenly across field staff.

![Key Findings & Recommendations](05_key_findings_recommendations.png)

---

## ⚙️ Core Data Architecture & Custom DAX Measures

The project utilizes advanced Data Analysis Expressions (DAX) to deliver custom calculations, zero-handling (`COALESCE`), and domain-specific facility metrics:

### 1. SLA Compliance %
SLA Compliance % = DIVIDE(CALCULATE(COUNTROWS(CAFM), CAFM[SLA_Status] = "Met"), COUNTROWS(CAFM), 0) * 100

### 2. First-Time Fix Rate (FTFR %)
First-Time Fix Rate % = 
DIVIDE(
    CALCULATE(COUNTROWS(CAFM), CAFM[Status] = "Closed", CAFM[Actual_Resolution_Hours] <= (CAFM[Target_SLA_Hours] * 1.5)),
    CALCULATE(COUNTROWS(CAFM), CAFM[Status] = "Closed"), 
    0
) * 100

### 3. Repeat Call Rate %
Repeat Call Rate % = 100 - [First-Time Fix Rate %]

### 4. Overdue Backlog (Zero-Handling)
Overdue Backlog = 
COALESCE(
    CALCULATE(
        COUNT(CAFM[Ticket_ID]),
        CAFM[Status] IN {"Open", "Work in progress", "Pending"},
        CAFM[SLA_Status] = "Breached"
    ),
    0
)

---

## 💡 Key Executive Findings & Action Plan

1. **Overall SLA Deficit:** SLA compliance stands at **38.97%**, significantly below the 90%+ industry benchmark.  
   * *Action:* Implement automated escalation workflows and real-time supervisor alerts.
2. **Critical Response Paradox:** Critical tickets achieve an average resolution of **1.28 hours** against a 2-hour target, yet only **41.94%** meet overall SLA—indicating triage bottlenecks rather than repair speed.  
   * *Action:* Redesign helpdesk dispatch to auto-assign Critical tickets instantly.
3. **Backlog Accumulation:** **210 tickets (42%)** remain trapped in active backlog (`In Progress`).  
   * *Action:* Conduct weekly backlog-clearing sprints.
4. **Resource Bottleneck:** Technician **Karthik Nair** manages the heaviest workload (75 tickets) but suffers from the lowest SLA compliance (**27.66%**) and longest resolution times (**9.61 hours**).  
   * *Action:* Rebalance ticket distribution and provide targeted mentoring.

---
