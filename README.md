# sap-internal

---

# **SPC - Service Provider Cockpit (SPC) – Process Guide**

---

## **Overview:**

The Service Provider Cockpit (SPC) is used for handling and processing SAP tickets (incidents, requests) assigned to the Managed Cloud Delivery (MCD) team. Tickets can be accessed via **My Launchpad**.

---

## **1. MONITORING – Initial Ticket Handling**

### **Ticket Identification**

* **Access:** From **My Launchpad**
* **Filter:** Use top filter bar to refine tickets.

  * **Subcontractor ID (NTT ID for SAP):** ACE14753
  * **Processing Queue:** MCD DB L2 – Arindham Bhattacharyya

### **Process Steps:**

1. **Open Ticket:** Only focus on *new and open* tickets.

2. **Review Ticket Description:** Understand the request and check **scheduled time**.

3. **Update Subject Line:**

   * Click **Edit**
   * Format: `TBS_<DD.MM.YYYY>_<Time>_<TimeZone>_<Activity Name>`
   * Example: `TBS_15.08.2025_7:30 AM_India_HanaDb Upgrade`
   * `TBS` stands for “To Be Scheduled”
   * Once updated, status changes from **New** → **In Process**

4. **If Data Is Missing/Incorrect:**

   * Click **Ask Customer** to send it back
   * Status changes to **Waiting**

5. **Acknowledgment:**

   * For automatic processes: **Auto ACK**
   * If manual: Use **template** and click **Info to Requester**
     Must be sent **within Initial Response Time (IRT)** – 30 minutes from when the ticket was created.

6. **Check Scope of Activity:**

   * Validate if ticket belongs to our team
   * Refer to **Scope of Activities – HEC Delivery (Wiki Page)**

---

## **2. TQS – Technical Qualifier & Scheduler**

### **Ticket Validation:**

* Check:

  * **Scheduled Start** & **Estimated End Time**
  * **DMM Qualified (Minimized Downtime):** Yes/No

### **Tabs to Review:**

* General
* Classification
* Participants
* References
* Changes
* Customers
* Subcontractors
* Affected
* Objects
* Attachments
* Statistics

---

## **Service Execution (SE) Object:**

### **References Tab:**

* If automation/semi-automation: **Service Execution Object** is available
* Click SE ID to open details

### **Service Definition Includes:**

* Service Definition ID
* Preparation Duration (Uptime)
* Execution Duration (Downtime/Uptime)
* Post-Processing Duration (Uptime)
* Total Duration
* Planning Window
* Rollback Duration

### **Schedule Timings:**

* **Planned Schedule:**

  * Preparation Start
  * Execution Start
  * Execution End
* **Actual Schedule:**

  * Same fields as above

---

## **Pre-Checks:**

* Check for any **errors or required actions**
* Review **bottom tasks** and their **logs**

---

## **Tabs Inside Service Execution:**

### **1. Parameter Tab:**

* Shows values/details mentioned in the ticket

### **2. Workflow Execution:**

* its an end to end automation of service request life cycle phase or Step-by-step ticket processing
* **ACK:** Auto
* **Risk Assessment (Prod):**

  * Click **More → Risk Assessment**
  * Click **Edit → Complete with No Risk Identified**

### **3. COS (Confirmation of Schedule):**

* Sent automatically to customer after scheduling
* **COS Timelines – Based on SLA:**

  * ≤ 4.5 hrs: Immediate
  * > 4 hrs & ≤2 days: within 4 hrs
  * > 2 days & ≤5 days: within 24 hrs
  * > 5 days & ≤10 days: within 48 hrs
  * > 10 days: within 72 hrs

### **4. Risk Acknowledgement:**

* Go to **Risk Assessment → Edit → Risk Ack**
* Must be done by a **senior (not the same person doing the risk assessment)**

---

## **Phases in Execution:**

1. **Preparation Phase:**

   * Preparation Start
   * Preparation End
2. **Execution Phase:**

   * Execution Start
   * Post Processing Start
   * Post Processing End

---

## **Risk Assessment:**

* Check potential risks
* Use **Issue Tracker** (search by CID)
* Weekly calls may be used to discuss risk scenarios

---

## **External System ID:**

* Combination of **SID (System ID)** and **CID (Customer ID)**

---

## **LAMA Configuration:**

* Errors in prechecks require attention
* Use troubleshooting documentation
* For automation errors – separate support team involved

---

## **Manual Activity – Creating SE Object:**

### **Steps:**

1. Click **Follow-Up → SE**
2. Fill **Teams** field
3. In **General** tab:

   * Enter **Service Definition ID** (available in Scope List Wiki)
   * Check for **Process Check**

     * If not present: perform **manual prechecks at OS level**
     * Manually fill **Planned Schedule**

---

## **TQS Phase Completion:**

* After all validations & scheduling, update subject line:

  * Change prefix from `TBS` → `DB`
  * Indicates end of TQS phase

---

## **HANA Release Information**

### **Latest Releases:**

* **N (Current):**

  * Release Date: 18 Apr 2025
  * Version: SAP HANA 2.0 SPS08 Rev 083.00
* **N-1 (Previous):**

  * Release Date: 31 Jan 2025
  * Version: SAP HANA 2.0 SPS07 Rev 079.02

### **Next Planned Standard Release:**

* **Date:** 29 Aug 2025
* **N:** SAP HANA 2.0 SPS08 Rev 086.00
* **N-1:** SAP HANA 2.0 SPS07 Rev 079.05

### **Recommended OS Versions:**

* **N:** SLES for SAP Applications 15 SP5 and above
* **N-1:** SLES for SAP Applications 15 SP4 and above

---

## **Patch & Server Management:**

* **OS Patch:** Done by **Server Management Team**
* Create **Internal Ticket (SR)** for them

---

## **Additional Notes:**

* **Returning Ticket to Customer:**

  * Click **Ask Customer**
  * Status changes from **New/In Process** to **Waiting**

* **Child Tickets:**

  * Visible under **References tab**

---

---

# **SRDashboard: Structured Documentation**

The **SRDashboard** is a centralized tool with multiple **widgets** to monitor and manage ticket and service request (SR) processing, downtimes, customer communications, escalations, and queue statuses across production and non-production systems.

---

## **1. Processing Queues**

These are internal processing code labels used to identify ticket queues:

* `MCD`
* `DB`
* `L2`
* `ECS SR DELIVERY DB NCT`
* `ECS SR DELIVERY GXP DB`

These queues hold service requests or tickets for different levels or types of support (e.g., DB-level issues, L2 support, ECS delivery).

---

## **2. Extended Activities**

### **Uncleared Maintenance Flag**

* **Definition**: If there's a downtime extension and the flag was not cleared after the activity, it appears here.
* **Purpose**: Highlights maintenance activities that were extended but not properly closed out.
* **Widget Options**:

  * PROD
  * NON-PROD

### **Maintenance Flag**

* **Definition**: During service execution, a checkbox "Downtime/Uptime Reservation Required" is ticked to inform both the customer and support that this DT (Downtime) slot is reserved.
* **Where to Check**: Bottom of the **Related Downtime/Uptime tab** in the **Service Execution (SE)** screen.
* **Purpose**: Ensures both visibility and resource allocation for DT/UT periods.

### **Downtime vs Uptime**

* **Downtime**: System is stopped for an activity. **Note**: No work is performed during this time — it's purely for system reservation or protection.
* **Uptime**: Activities or changes are made **without stopping the system**.

---

## **3. Overrun Phases**

This widget monitors **delayed or incomplete scheduled activities**.

* **Triggered When**: Planned schedules are not completed within the expected timeframe.
* **Phases Tracked**:

  * **Preparation**
  * **Execution**
  * **Post Processing**

Each phase is monitored for its start and completion time. Delays here could impact service commitments or SLAs.

---

## **4. Ticket Management Widgets**

### **Ticket Backlog**

* **Definition**: Tickets lying in queues that have **not been picked up** or handled yet.
* **Purpose**: Helps track workload and unassigned service requests.

---

### **Reopened Tickets**

* **Definition**: Tickets that were **closed** but then **reopened by the client**, usually due to:

  * Incomplete resolution
  * Handling error
  * Dissatisfaction with service
* **Widget Options**:

  * PROD
  * NON-PROD

---

### **Ageing Tickets**

* **Definition**: Tickets that are in the queue **without any action or service execution**.

* **Metric**: Time-based display shows:

  * `< 1 day`
  * `1-3 days`
  * `3-5 days`
  * `> 5 days`

* **Widget Options**:

  * **SR Ticket**
  * **CSR Ticket** *(Customer Service Request)*

---

## **5. Scheduled Services**

### **To Be Started Phases**

* **Definition**: Activities scheduled to start soon.
* **Timing Categories**:

  * Starting within **0–30 minutes**
  * Starting within **30–60 minutes**
* **Visibility**: Primarily used by the **executor** to track what needs to begin shortly.
* **Widget Options**:

  * **Preparation**
  * **Execution**

---

### **Last Check Processes**

* **Definition**: Tickets with scheduled services that have **issues during the last validation or checkpoint**.
* **Widget Options**:

  * **Error**: Indicates issues in system readiness.
  * **Action Required**: Requires human intervention or decision before proceeding.

---

### **Delayed Services**

* **Definition**: Any **scheduled process that has not started or completed on time**.
* **Purpose**: Flags for project and operational managers to investigate the root cause of delays.

---

## **6. Ongoing Services (Execution Monitoring)**

There are **four widgets** under ongoing services, tracking live ticket execution status:

### **Ongoing Services Widget**

* **Tracks**: Execution status of tickets

* **Status Options**:

  * **Error**
  * **Action Required**
  * **Aborted**
  * **On Hold**
  * **In Process**
  * **Automatic Repeat**

* **Execution Types**:

  * **Self-Services**: End-to-end automatic execution; monitoring only.
  * **Non Self-Services**: Requires **manual steps** during execution.
  * **Unattended Services / Assisted Services**:

    * No predefined templates or service definitions.
    * Common templates are manually selected for **non-standard activities**.

---

## **7. Critical Customer KPIs**

### **Critical Customer KPI Widgets**

* Special widgets that track **VIP or priority customer tickets** separately.
* Helps in faster response and escalated handling.

---

## **8. Communication & Update Widgets**

### **Update Frequency Widget**

* Tracks how frequently updates are provided to customers via the **"Info to Requestor"** button.
* **Update Time Categories**:

  * **Expired** (No recent update)
  * **<= 15 minutes**
  * **<= 30 minutes**
  * **<= 120 minutes**

---

### **Escalation Widgets**

* Shows all issues or tickets that have been **escalated by the customer**.
* Reasons for escalation:

  * No timely updates
  * Issue not resolved
  * Request mishandled
* **Purpose**: Enables immediate visibility to high-risk or customer-sensitive issues.

---


---

# **KPI & SLA: Structured Documentation**

KPI and SLA tracking helps ensure service quality, timely handling, and customer satisfaction. The RAG (Red, Amber, Green) system is used for **performance calibration** and escalation management across the following three key phases:

---

## 🔵 **1. Monitoring Phase**

### **IRT (Initial Response Time)**

* **SLA Target**: Respond **within 30 minutes** of ticket arrival.
* **Purpose**: Acknowledges the ticket and initiates communication with the customer.
* **KPI Type**: Timeliness of response.

---

### **Escalation**

* **Customer-Triggered**: A customer can escalate if:

  * They don’t receive timely updates
  * Planned changes are unclear
  * They require additional steps or clarification
* **RAG Indicator**:

  * **Red**: IRT missed + escalation occurred
  * **Amber**: Late response but recovered
  * **Green**: On-time response, no escalation

---

## 🟡 **2. TQS Phase (Ticket Quality System)**

### **COS (Customer Operational Start Time)**

* **Definition**: Measured from the time ticket enters our queue until **execution begins**

* **Reference**: COS timeline as defined in the **COS Wiki**

* **Timeliness Bands**:

  | Ticket Age         | Response SLA    |
  | ------------------ | --------------- |
  | ≤ 4 hours 30 mins  | Immediate       |
  | > 4 hours ≤ 2 days | Within 4 hours  |
  | > 2 days ≤ 5 days  | Within 24 hours |
  | > 5 days ≤ 10 days | Within 48 hours |
  | > 10 days          | Within 72 hours |

* **KPI**: Measures our responsiveness relative to ticket age and expectations.

---

### **Escalation**

* **Same Rule as Monitoring Phase**

  * Escalation can happen if timelines are not respected or poor communication is observed.

---

### **Process Deviation (PD)**

* **Definition**: When standard operational processes are not followed.
* **Examples**:

  * Skipping required validations
  * Incorrect ticket categorization
  * Handling outside documented workflows
* **Impact**: Tracked as a negative performance indicator.

---

## 🔴 **3. Execution Phase (Activity + Post-Processing)**

### **Scheduled Adherence (SA)**

* **Definition**: Whether execution started and completed within the **scheduled window**.
* **Violation Example**: Any delay in the execution start or end.
* **Requirement**: Provide proper justification using a separate **template message**.
* **Note**: **Downtime Extension** is **not considered a KPI or SLA breach**, but may affect SA.

---

### **Escalation**

* Again, **customer-triggered**, based on poor handling, delays, or missing communication.

---

### **DT Extension (Downtime Extension)**

* **Note**: Not a KPI or SLA directly.
* **Definition**: Extension of system downtime beyond the reserved window.
* **Managed Separately**: Seen in Scheduled Adherence metrics but tracked independently.

---

### **Handling Error**

* **Definition**: Error committed by the executor during execution.
* **Trigger**: Any mistake that causes **more than 5 minutes** delay (or operational disruption).
* **Examples**:

  * Selecting wrong templates
  * Failing to validate system readiness
  * Executing in wrong sequence

---

### **Process Deviation (PD)**

* **Same as earlier**: Not adhering to defined SOPs, templates, validations.

---

### **First Time Right (FTR)**

* **Definition**: Ticket is resolved and closed satisfactorily **on the first attempt**.
* **Violation**: If the ticket is **reopened by the customer due to executor error**, it fails FTR.
* **KPI Impact**: Impacts quality score.

---

### **ZO Team (Zero Outage Team)**

* **Goal**: Prevent outages through careful planning, monitoring, and execution.
* **Role**:

  * Monitor for deviations
  * Ensure system protection during changes
  * Flag critical issues before they affect production

---

## 🔷 **RAG: Delivery Performance Calibration**

* Used across all phases (Monitoring, TQS, Execution) to **calibrate service delivery quality**.
* **Red**: SLA missed, escalations involved, quality breach
* **Amber**: Slight delay or minor deviation, recovered without escalation
* **Green**: All SLAs met, no issues or escalations

---

## ✅ Summary Table

| Metric                  | Phase      | Target/Threshold       | KPI Type          |
| ----------------------- | ---------- | ---------------------- | ----------------- |
| **IRT**                 | Monitoring | ≤ 30 mins              | Response SLA      |
| **COS**                 | TQS        | Based on ticket age    | Execution SLA     |
| **Escalation**          | All        | Triggered by customer  | Performance Risk  |
| **Scheduled Adherence** | Execution  | On-time execution      | Delivery KPI      |
| **Downtime Extension**  | Execution  | Managed via SA         | Not a KPI         |
| **Handling Error**      | Execution  | > 5 mins mistake       | Quality Deviation |
| **Process Deviation**   | All        | Any SOP miss           | Process KPI       |
| **FTR**                 | Execution  | No reopens by customer | Quality KPI       |

---
