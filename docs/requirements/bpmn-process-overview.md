#### 2. Major Business Processes
### 2. Analysis of Major Business Processes and Organisational Responsibilities## 1. Overview of the Collaboration Structure

The BPMN model defines a multi-participant collaboration called `Collaboration_1`, centered around the main participant **"Bristol Regional Food Network"** (`Participant_Main`).

Internal operations are divided into four distinct organizational **lanes** within a single process (`Process_Main`):

- **Marketplace Platform:** Handles automated platform-level orchestration (publishing, validating, payment routing, inventory updates, and settlement).
- **Producer:** Responsible for product registration, seasonal listing, and order fulfillment.
- **Customer:** Interacts with the marketplace to browse, search, and place multi-vendor orders.
- **Marketplace Administrator:** Handles governance, specifically quality incidents and traceability.

Additionally, three external black-box participants integrate via message flows:

- **Certification Verification Service** (interacts with the Producer during product registration).
- **Payment Service (Sandbox)** (interacts with the Marketplace Platform for financial transactions).
- **Notification Service** (interacts with the Marketplace Platform for alerts).

### 2. Major Business Processes

The model captures two independent main process flows triggered by different starting events:

#### Process A: The Main Trading Cycle (`StartEvent_1` to `EndEvent_1`)

This end-to-end e-commerce and fulfillment lifecycle spans nine sequential steps across the Producer, Marketplace Platform, and Customer lanes:

1. **Marketplace Trading Cycle Begins (`StartEvent_1`):** Triggered on the platform.
2. **Register & List Products (`Task_P1` - Producer):** Producers register products with seasonal availability. This involves a external message exchange (`MessageFlow_1` and `MessageFlow_2`) with the **Certification Verification Service** to validate product credentials.
3. **Publish Validated Listings (`Task_PL1` - Platform):** The marketplace publishes the approved seasonal listings.
4. **Browse, Search & Place Order (`Task_C1` - Customer):** Customers browse the catalog and place a **multi-vendor order** spanning items from different local producers.
5. **Validate & Aggregate Order (`Task_PL2` - Platform):** The platform validates and groups the multi-vendor items for efficient fulfillment.
6. **Process Payment & Commission (`Task_PL3` - Platform):** The platform communicates with the external **Payment Service (Sandbox)** (`MessageFlow_3` and `MessageFlow_4`) to process the transaction while retaining a **5% platform commission**.
7. **Notify Producers & Update Inventory (`Task_PL4` - Platform):** The platform uses the external **Notification Service** (`MessageFlow_5` and `MessageFlow_6`) to alert producers and update stock levels.
8. **Prepare & Fulfil Orders (`Task_P2` - Producer):** Producers prepare the items and fulfill the customer order.
9. **Settle Payments (`Task_PL5` - Platform):** The platform distributes earnings to the respective producers minus the commission.
10. **Trading Cycle Complete (`EndEvent_1`).**

#### Process B: Quality Incident Management (`StartEvent_2` to `EndEvent_2`)

This is a governance and exception-handling subprocess managed entirely by the Marketplace Administrator:

1. **Quality Issue Reported (`StartEvent_2`):** Triggered when a food safety or quality complaint arises.
2. **Manage Quality Incident & Traceability (`Task_A1` - Administrator):** The administrator investigates the issue using supply chain traceability data.
3. **Incident Closed (`EndEvent_2`).**
