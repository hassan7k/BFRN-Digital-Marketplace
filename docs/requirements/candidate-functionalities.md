# Candidate Major Functionalities Scope & Analysis

**Module:** UFCFTR-30-3 - Distributed and Enterprise Software Development  
**Project:** Bristol Regional Food Network (BFRN) Digital Marketplace  

---

## 1. Executive Summary
Based on the strategic process analysis and high-level BPMN modeling, two core business functionalities have been identified for detailed operational modeling and Camunda process automation.

---

## 2. Functionality 1: Multi-Vendor Trading, Payment & Settlement Lifecycle

### 2.1 Description & Scope
This functionality manages the end-to-end customer order journey, spanning product listing validation, multi-vendor cart aggregation, payment processing, producer notifications, and automated commission distribution.

### 2.2 Key Participants & Lanes
* **Customer:** Browses, selects products across different local producers, and submits multi-orders.
* **Producer:** Receives order notifications, updates inventory, and fulfills goods.
* **Marketplace Platform:** Handles order validation, 5% commission calculation, and settlement.
* **External Services:** Certification Verification Service, Payment Service (Sandbox), Notification Service.

### 2.3 Process Flow & Requirements
1. **Producer Registration & Listing:** Product registration with seasonal availability and credential verification.
2. **Catalog Publishing:** Validated listings published on the platform.
3. **Multi-Vendor Checkout:** Customer places an order spanning items from multiple producers.
4. **Order Aggregation & Validation:** Grouping items by producer and verifying stock.
5. **Payment Execution:** Charging customer via Payment Service and deducting 5% commission.
6. **Fulfillment & Settlement:** Notifying producers and distributing earnings.

---

## 3. Functionality 2: Food Safety Quality Incident Management & Traceability

### 3.1 Description & Scope
This functionality provides governance and exception-handling capabilities when a food safety complaint or quality dispute arises, allowing the Administrator to freeze batch sales and resolve incidents.

### 3.2 Key Participants & Lanes
* **Customer:** Reports quality issues or food safety complaints.
* **Marketplace Administrator:** Investigates incidents, audits traceability data, and enforces compliance.
* **Producer:** Provides batch logs and receives incident alerts.

### 3.3 Process Flow & Requirements
1. **Incident Trigger:** Customer logs a formal quality complaint.
2. **Triage & Isolation:** Administrator isolates the affected batch and halts listed stock.
3. **Traceability Investigation:** Querying historical supply chain data and producer logs.
4. **Resolution Decision:** Issuing refunds, batch recalls, or compliance warnings.
