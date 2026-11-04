# Traceability Matrix — BRFN Digital Marketplace

**Status:** In progress. Camunda column records planned elements only — no
licences available to the group yet.

## How to read this document

| Column | Meaning |
|---|---|
| **Stakeholder goal / dependency** | The need being satisfied, from the case study and (once available) the i* models |
| **Strategic BPMN task** | Activity in the strategic model |
| **Operational BPMN task(s)** | Detailed activities in the operational models |
| **Planned Camunda element** | Intended BPMN element type and process variables. Design only, not built. |


---

## 1. Traceability table

### 1.1 Product listing and catalogue management

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Producer (low technical capability) can list products without training | Register & list products with seasonal availability (`Task_P1`) | Submit product listing form | User task + Camunda Form |
| Producer needs seasonal availability to be updateable | Register & list products with seasonal availability (`Task_P1`) | Update seasonal availability | User task + Camunda Form |
| Consumers must be able to trust organic claims | Register & list products with seasonal availability (`Task_P1`) | Request certification verification | Service task → message flow to Certification Verification Service |
| Platform must not publish unverified claims | Publish validated listings (`Task_PL1`) | Validate listing data | Exclusive gateway + validation service task |
| | | Handle verification service unavailable | Boundary error event + retry path |
| | | Publish approved listing | Service task |

### 1.2 Multi-vendor ordering

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Customer wants a single checkout across multiple producers | Browse, search & place multi-vendor order (`Task_C1`) | Browse and search catalogue | User task + Camunda Form |
| | | Review basket and confirm order | User task + Camunda Form |
| Customer must not be charged for unavailable stock | Validate & aggregate multi-vendor order (`Task_PL2`) | Validate item availability | Service task |
| | | Decide: all items available? | Exclusive gateway |
| | | Amend order (unavailable items) | User task + Camunda Form (loop back) |
| Customer needs clear per-supplier responsibility | Validate & aggregate multi-vendor order (`Task_PL2`) | Identify producers in basket | Service task |
| | | Determine delivery/collection per producer | Service task |
| Platform must split one basket into producer orders | Validate & aggregate multi-vendor order (`Task_PL2`) | Create marketplace order | Service task |
| | | Create producer-specific sub-orders | Multi-instance service task |
| TBD — pending i* model | TBD | TBD | TBD |

### 1.3 Payment, commission and settlement

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Platform earns 5% commission on every order | Process payment & calculate 5% commission (`Task_PL3`) | Calculate amount per producer | Service task + variable `producerAmounts` |
| | | Calculate 5% commission | Service task + variable `commissionAmount` |
| Customer needs secure payment | Process payment & calculate 5% commission (`Task_PL3`) | Submit payment | Service task → message flow to Payment Service (Sandbox) |
| Customer must be able to retry a declined payment | Process payment & calculate 5% commission (`Task_PL3`) | Decide: payment outcome? | Exclusive gateway (approved / declined / unavailable) |
| | | Retry payment | User task + Camunda Form + boundary timer event |
| | | Handle payment service unavailable | Boundary error event + retry path |
| Producer needs weekly settlement with audit trail | Settle producer payments & commission (`Task_PL5`) | Record settlement per producer | Service task + data store |
| | | Produce audit trail | Data object / service task |
| TBD — pending i* model | TBD | TBD | TBD |

### 1.4 Fulfilment and notification

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Producer needs 48-hour minimum lead time to prepare | Notify producers & update inventory (`Task_PL4`) | Dispatch producer notification | Service task → message flow to Notification Service |
| Producer needs accurate stock visibility | Notify producers & update inventory (`Task_PL4`) | Update inventory quantities | Service task |
| Customer needs order confirmation | Notify producers & update inventory (`Task_PL4`) | Notify customer of confirmation | Service task → Notification Service |
| Producer fulfils the order | Prepare & fulfil orders (`Task_P2`) | Prepare and dispatch order | User task (Producer) |
| System must handle notification failure | Notify producers & update inventory (`Task_PL4`) | Handle notification failure | Boundary error event + alternative channel / manual follow-up |
| TBD — pending i* model | TBD | TBD | TBD |

### 1.5 Quality incident and traceability

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Customer can report a food safety or quality concern | Manage quality incident & traceability (`Task_A1`) | Submit incident report | User task + Camunda Form |
| Administrator needs full traceability of affected stock | Manage quality incident & traceability (`Task_A1`) | Identify affected product and producer | Service task |
| | | Retrieve affected customer orders | Service task / data query |
| Producer must be able to respond to an incident | Manage quality incident & traceability (`Task_A1`) | Request information from producer | User task (Producer) + notification |
| Public must be protected from unsafe stock | Manage quality incident & traceability (`Task_A1`) | Suspend product from sale | Service task |
| Affected customers must be contacted | Manage quality incident & traceability (`Task_A1`) | Notify affected customers | Multi-instance service task → Notification Service |
| Failed notifications must be identified and followed up | Manage quality incident & traceability (`Task_A1`) | Record notification result | Service task |
| | | Handle failed notification | Boundary error event + manual follow-up task |
| Incident must be closed by an authorised person | Manage quality incident & traceability (`Task_A1`) | Review and close incident | User task (Administrator) + gateway (close / escalate) |
| TBD — pending i* model | TBD | TBD | TBD |

---
