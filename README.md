> **Published service.** Hosted by LMS, University of Patras.
> Method, example and runner: https://huggingface.co/EnerTEF/AI-Assisted-Production-Scheduling
> This repository is the technical specification.

# AI-Assisted Scheduling of Production towards Energy Efficiency Increase

**Technical Specifications**

**Contracting Authority:** LMS - Laboratory for Manufacturing Systems and Automation
**Version:** 1.0
**Last updated:** February 2026

---

## 1. Business Context & Definitions

This tender concerns the development and operation of an AI-assisted production scheduling system for industrial manufacturing environments. The system shall optimise the allocation and sequencing of production tasks across available manufacturing resources, with energy efficiency as a primary optimisation criterion alongside traditional time-related metrics. Industrial manufacturers, production planners and facility managers will use the service outputs to minimise energy consumption, reduce operational costs, improve throughput and achieve sustainability targets.

### Key Terms

- **Scheduling:** The job or activity of planning the times at which particular tasks will be done or events will happen.
- **Production Orders:** Work instructions specifying what needs to be manufactured, quantities, due dates and priorities.
- **Manufacturing Resources:** Available machines, equipment and tools for production operations.
- **Energy Efficiency:** Metric expressing the ratio of useful production output to energy consumed.

### 1.1 Contracting Authority Context

The contracting authority operates production facilities with multiple machines and processes. Manual or inefficient scheduling processes often lead to resource conflicts, downtime, overstaffing or underutilisation of assets. These inefficiencies increase operational costs, reduce productivity and introduce human error. Traditional scheduling systems often overlook energy efficiency. The contracted service shall automate and optimise the allocation of tasks and resources. Incorporating energy efficiency as a scheduling criterion shall enable smarter allocation of resources, reduce operational costs, support sustainability goals and help meet regulatory or ESG targets.

---

## 2. Objectives & Problem Statement

The contractor shall develop and deliver a production-ready AI-assisted scheduling service that generates optimised production schedules for industrial manufacturing facilities. The service shall expose a simple, authenticated REST API and remain available and responsive throughout operational hours. The service shall automate and optimise the allocation of tasks and resources, ensuring operations run smoothly and efficiently. By minimising idle time and improving throughput, the service shall support cost savings and better service delivery.

---

## 3. Data Description

The contracting authority shall provide the following data to the contractor:

### Production Orders Data
*(Provided by Contracting Authority, Indicatively here)*

| Variable | Variable name | Type | Measurement unit | Description | Allowed values / Examples |
|---|---|---|---|---|---|
| Order ID | `order_id` | String | - | Unique identifier for production order | ORD-2026-001 |
| Product Code | `product_code` | String | - | Product or part identifier | PART-A123 |
| Quantity | `quantity` | Integer | units | Number of units to produce | 100, 500, 1000 |
| Due Date | `due_date` | Date | YYYY-MM-DD | Delivery deadline for order | 2026-03-15 |
| Priority Level | `priority` | Integer | - | Order priority (1=highest) | 1, 2, 3 |
| Process Sequence | `process_seq` | Array | - | Required manufacturing operations in order | [cutting, milling, assembly] |

### Machine/Resource Data
*(Provided by Contracting Authority, Indicatively here)*

| Variable | Variable name | Type | Measurement unit | Description | Allowed values / Examples |
|---|---|---|---|---|---|
| Machine ID | `machine_id` | String | - | Unique machine identifier | MILL-01, LATHE-03 |
| Machine Type | `machine_type` | String | - | Equipment category | CNC Mill, Lathe, Assembly |
| Processing Time | `process_time` | Float | minutes | Time to complete operation | 15.5, 30.0, 45.0 |
| Energy Consumption | `energy_kwh` | Float | kWh | Energy per operation | 2.5, 5.0, 8.5 |
| Availability | `available` | Boolean | - | Machine operational status | true, false |
| Setup Time | `setup_time` | Float | minutes | Time for operation changeover | 10.0, 20.0, 30.0 |

---

## 4. Analytics, Scope & Update Frequency

### Temporal Scope

The service shall generate production schedules covering planning horizons from several hours to multiple days ahead, depending on the manufacturing environment and order lead times. Schedules shall be aligned to the production facility's operational time grid (typically hourly or shift-based intervals). The service shall provide schedule updates as new orders arrive or when operational conditions change.

### Update Frequency

Schedules shall be generated on demand via authenticated API requests (suggested mode). The contracting authority may request schedule generation at regular intervals (e.g. start of each shift, daily planning cycles) or triggered by specific events such as new order arrivals, machine breakdowns or priority changes. The service shall respond to schedule requests within the specified response time requirements.

### Output Format

For each request, the service shall return a structured response including:

- **Issue time & validity window:** Timestamp (UTC) when the schedule is generated, plus the start and end times the schedule covers (e.g. next 8 hours, next production day).
- **Time-indexed schedule output:** A time series of scheduled operations specifying which orders are assigned to which machines at which time intervals, including start times, end times and resource allocations.
- **Energy consumption forecast:** Predicted energy consumption profile over the scheduled period, showing expected power demand and total energy usage.

### Suggested Technical Specifications

- **Backend APIs:** Java SPRING
- **Database:** MySQL
- **User Interface:** Angular

---

## 5. Evaluation Protocols & Metrics

### 5.1 Data Usage & Operational Protocol

- The service shall generate schedules on demand for planning horizons as specified by the contracting authority.
- The service shall behave consistently: repeated requests for the same input data and configuration shall produce similar schedules.

### 5.2 Data Gaps and Exceptions (Desired)

- Periods with incomplete or invalid input data (e.g. missing machine specifications, corrupted order data) shall be flagged and excluded from schedule quality assessment.
- If critical data is missing, the service shall either generate a partial schedule with documented limitations or return an error with clear explanation of the missing information required.

### 5.3 Service Evaluation Metrics & KPIs

The delivered service shall be evaluated using the following quantitative metrics:

- **Schedule Quality vs Baseline:** The generated schedules shall demonstrate minimum 10% improvement in energy efficiency compared to a baseline scheduling approach (e.g. First-In-First-Out heuristic or existing manual scheduling practice), measured as reduction in total energy consumption for equivalent production output.
- **Computation Time:** Schedule generation shall complete within time comparable to the production cycle time, ensuring schedules are available when needed for operational decision-making.
- **Schedule Feasibility:** 100% of generated schedules shall satisfy hard constraints including due dates, machine capacity limits and operation precedence relationships.

---

## 6. Deliverables & Submissions

### 6.1 Required Reports

The contractor shall deliver three (3) reports during the service lifecycle:

- **Pre-Service Deliverable – Service Design & Setup Report:** Submitted prior to service start (Month 18), describing the proposed approach, methodology, system architecture, security measures and integration plan.
- **Intermediate Deliverable – Interim Performance & Operations Report:** Submitted at Month 21, summarising service operation to date, data coverage, preliminary results and performance against defined metrics.
- **Final Deliverable – Final Evaluation & Recommendations Report:** Submitted at Month 25, presenting final performance results, insights, identified improvements and recommendations.

### 6.2 Technical Specifications & Documentation

The contractor shall provide:

- **Service Interface Documentation:** Full documentation of APIs, data formats, authentication and access controls.
- **Configuration & Versioning Documentation:** Documentation of configuration parameters, model versioning and operational procedures.
