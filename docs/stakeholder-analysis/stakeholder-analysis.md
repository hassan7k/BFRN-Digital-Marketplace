# Stakeholder Analysis

Underpins the i* Strategic Dependency (SD) and Strategic Rationale (SR) models.
Records the actors, their goals, softgoals and dependencies.

## 1. Actors

| Actor | Type | Description |
|---|---|---|
| Producer | Role | Local food producer listing and fulfilling products. Varying technical capability |
| Customer | Role | Individual, community group or restaurant buying from the marketplace |
| Marketplace Platform | System | The digital marketplace itself — validation, aggregation, payment, notification, settlement |
| Marketplace Administrator | Role | Governance, incident handling, compliance oversight |
| Certification Verification Service | External system | Verifies organic certification claims |
| Payment Service | External system | Sandbox payment processing and settlement |
| Notification Service | External system | Sends alerts to producers, customers and administrators |

## 2. Goals per actor

### Producer

| Goal | Type | Notes |
|---|---|---|
| Sell produce beyond farm gate and farmers' markets | Hard goal | Core motivation for joining the network |
| List products without technical training | Hard goal | 15 hrs/week currently spent on manual comms |
| Update seasonal availability frequently | Hard goal | Seasonal stock changes; must not require tech skill |
| See incoming orders at least 48 hours ahead | Hard goal | Preparation lead time |
| Receive weekly payment settlement | Hard goal | Cash flow |
| Have an audit trail for tax and accounting | Hard goal | Legal/accounting requirement |
| Be trusted by customers | Softgoal | Depends on certification, traceability, transparency |

### Customer

| Goal | Type | Notes |
|---|---|---|
| Buy local produce conveniently | Hard goal | Core need; farm opening hours are the barrier |
| Browse by category and search | Hard goal | Vegetables, dairy, bakery, preserves, seasonal |
| See harvest date, farm origin, seasonal availability | Hard goal | Differentiator vs supermarkets |
| Check out once across multiple producers | Hard goal | Single-vendor and multi-vendor both required |
| Know which producer is responsible for what | Hard goal | Delivery, collection, quality responsibility |
| Be confident food is safe | Softgoal | Traceability, allergen warnings, best-before |

### Marketplace Platform

| Goal | Type | Notes |
|---|---|---|
| Validate and publish only verified listings | Hard goal | Trust and regulatory |
| Aggregate multi-vendor orders correctly | Hard goal | Core value proposition |
| Process payment securely | Hard goal | Compliance with financial services regulations |
| Calculate and retain 5% commission | Hard goal | Revenue model |
| Distribute payments to producers | Hard goal | Weekly cycle |
| Maintain traceability records linking customer, product, producer | Hard goal | Legal — food safety |
| Be reliable and trustworthy | Softgoal | Reputation with all parties |

### Marketplace Administrator

| Goal | Type | Notes |
|---|---|---|
| Respond to food safety and quality incidents | Hard goal | Legal obligation |
| Identify affected products, producers and customers quickly | Hard goal | Depends on traceability records |
| Suspend unsafe products from sale | Hard goal | Public protection |
| Close incidents with documented justification | Hard goal | Audit and compliance |
| Be impartial and accountable | Softgoal | Governance |

### External services

| Actor | Goal |
|---|---|
| Certification Verification Service | Provide accurate organic certification verification |
| Payment Service | Process payments securely and return a reliable result |
| Notification Service | Deliver messages and report delivery outcome |

## 3. Dependencies

| Depender | Dependee | Dependum | Type |
|---|---|---|---|
| Producer | Certification Verification Service | Certification verified | Task dependency |
| Producer | Marketplace Platform | Orders visible ≥48 hrs ahead | Task dependency |
| Producer | Marketplace Platform | Weekly settlement with audit trail | Task dependency |
| Customer | Marketplace Platform | Accurate stock and availability information | Task dependency |
| Customer | Marketplace Platform | Safe, traceable food | Softgoal dependency |
| Customer | Marketplace Platform | Clear per-supplier responsibility | Goal dependency |
| Marketplace Platform | Producer | Accurate product and stock data | Task dependency |
| Marketplace Platform | Payment Service | Payment authorised or declined | Task dependency |
| Marketplace Platform | Notification Service | Messages delivered | Task dependency |
| Marketplace Platform | Certification Verification Service | Verification result | Task dependency |
| Marketplace Administrator | Marketplace Platform | Traceability records retrievable | Task dependency |
| Marketplace Administrator | Notification Service | Affected customers contacted | Task dependency |
| Marketplace Administrator | Producer | Incident information supplied | Task dependency |
| Marketplace Platform | Regulator (implicit) | Compliance with data protection and financial services rules | Softgoal dependency |

## 4. Tensions and competing goals

| Tension | Actors | Implication for design |
|---|---|---|
| Producer wants minimal admin; platform needs accurate data | Producer ↔ Platform | Listing forms must be short but mandatory fields enforced |
| Customer wants fast checkout; platform must verify stock | Customer ↔ Platform | Availability check must be automatic, not manual |
| Administrator needs rapid contact; customers expect privacy | Administrator ↔ Customer | Contact details stored with controlled access and audit |
| Producer wants weekly payment; customer may dispute quality | Producer ↔ Customer ↔ Platform | Settlement must support holds or reversals on open incidents |
| Producers vary in technical skill | Producer ↔ Platform | Interfaces must work for email-only users as well as social-media users |

## 5. Link to strategic BPMN

| Strategic task | Serves which goals |
|---|---|
| Register & list products (`Task_P1`) | Producer: sell beyond farm gate, list without training, update availability |
| Publish validated listings (`Task_PL1`) | Platform: validate listings; Customer: trust |
| Browse, search & place multi-vendor order (`Task_C1`) | Customer: convenient local purchase, single checkout |
| Validate & aggregate multi-vendor order (`Task_PL2`) | Platform: correct aggregation; Customer: clear responsibility |
| Process payment & calculate commission (`Task_PL3`) | Platform: revenue, secure payment; Customer: secure transaction |
| Notify producers & update inventory (`Task_PL4`) | Producer: 48-hr lead time; Platform: accuracy |
| Prepare & fulfil orders (`Task_P2`) | Producer: fulfilment; Customer: receipt |
| Settle producer payments (`Task_PL5`) | Producer: weekly settlement, audit trail |
| Manage quality incident (`Task_A1`) | Administrator: incident response; Customer: safety |