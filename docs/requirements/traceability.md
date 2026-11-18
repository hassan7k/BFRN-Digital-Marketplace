# Traceability Matrix — BRFN Digital Marketplace

## 1. Traceability table

### 1.1 Product listing and catalogue management

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Marketplace Platform → Producer (Accurate product and stock data) | Register & list products with seasonal availability (`Task_P1`) | Proposed: submit listing, validate required fields and return incomplete entries for correction. | Producer form and required-field validation |
| Producer → Certification Verification Service (Certification verified)<br>Marketplace Platform → Certification Verification Service (Verification result) | Publish validated listings (`Task_PL1`) | Proposed: verify a claimed certificate, then publish an approved listing. | Verification service task and approval gateway |
| Customer → Marketplace Platform (Accurate stock and availability information)<br>Marketplace Platform → Producer (Accurate product and stock data) | Register & list products with seasonal availability (`Task_P1`) → Publish validated listings (`Task_PL1`) | Check stock inventory for each producer (`Activity_0n4ondn`) — The checkout check is modelled. Listing updates, automatic withdrawal and seasonal reactivation are proposed. | Stock update form and seasonal availability rule |

### 1.2 Multi-vendor ordering

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Customer wants to review one basket across producers. | Browse, search & place multi-vendor order (`Task_C1`) | Browse BRFN Marketplace (`Activity_0ijwhsq`) → Select products (`Activity_0qb2g8m`) → Review order (`Activity_1ty89yw`) → Submit order (`Activity_0zufe2t`) | Basket review and confirmation form |
| Customer → Marketplace Platform (Accurate stock and availability information) | Validate & aggregate multi-vendor order (`Task_PL2`) | Check stock inventory for each producer (`Activity_0n4ondn`) → Are all ordered items available? (`Gateway_10pijaq`) → Notify customer of unavailable items (`Activity_0xdlw17`) — The unavailable branch ends at a proceed-or-cancel event. An amendment and recheck loop is proposed. | Stock-check service task, availability gateway and amendment loop |
| Customer → Marketplace Platform (Clear per-supplier responsibility) | Validate & aggregate multi-vendor order (`Task_PL2`) | Group items per producer (`Activity_12m71zm`) — Grouping exists. Per-producer delivery or collection selection is proposed. | Delivery or collection selection per producer |
| Customer → Marketplace Platform (Clear per-supplier responsibility)<br>Marketplace Administrator → Marketplace Platform (Traceability records retrievable) | Validate & aggregate multi-vendor order (`Task_PL2`) | Create specific sub-orders by producers (`Activity_1hmwjle`) — Producer sub-orders are explicit. A parent marketplace order record is proposed. | Order creation service task and linked producer sub-orders |

### 1.3 Payment, commission and settlement

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Marketplace Platform → Payment Service (Payment authorised or declined) | Process payment & calculate 5% commission (`Task_PL3`) | Request payment (`Activity_1tdzd31`) → Payment success? (`Gateway_1h82gpe`) → Record payment failure (`Activity_1hocuks`) — Failure is recorded and the draft ends the order. Declined-payment retry and temporary outage handling are proposed. | Sandbox payment task, outcome gateway and retry path |
| Producer → Marketplace Platform (Weekly settlement with audit trail) · Platform retains 5% commission. | Process payment & calculate 5% commission (`Task_PL3`) | Calculate order total (`Activity_09wnlgy`) → Calculate commission for marketplace (`Activity_1wvd9da`) → Calculate producer settlement amounts (`Activity_1clu9o4`) — The diagram names the calculations. The rate comes from the case study. | Commission calculation service task (5%) |
| Producer → Marketplace Platform (Weekly settlement with audit trail) | Settle producer payments & commission (`Task_PL5`) | Calculate producer settlement amounts (`Activity_1clu9o4`) → Process producer settlements (`Activity_005i2j3`) — Settlement is modelled. Weekly scheduling and an audit record are proposed. | Weekly timer, settlement service task and audit record |
| Marketplace Platform → Regulator (implicit) (compliance with data protection and financial services rules) | Settle producer payments & commission (`Task_PL5`) | Process producer settlements (`Activity_005i2j3`). Proposed control: restrict access to settlement records. | Role-based access and settlement audit record |

### 1.4 Fulfilment and notification

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Producer → Marketplace Platform (Orders visible ≥48 hrs ahead)<br>Customer → Marketplace Platform (Accurate stock and availability information)<br>Marketplace Platform → Notification Service (Messages delivered) | Notify producers & update inventory (`Task_PL4`) | Record payment success (`Activity_049lzo0`) → Send customer order and payment confirmation notification (`Activity_0rezzss`) → Send producer order and settlement notification (`Activity_0sh4jkv`) — Confirmation messages exist. A stock decrement and a 48-hour lead-time check are proposed. | 48-hour lead-time rule, stock update and notification service tasks |
| Customer → Marketplace Platform (Clear per-supplier responsibility) | Prepare & fulfil orders (`Task_P2`) | Can producer fulfill order? (`Gateway_02c5g9m`) → Prepare order (`Activity_1yrzc3d`) → Can all producers fulfill request? (`Gateway_11vx0ou`) → Handle unavailable items and determine cancellation/refund (`Activity_0do0ew0`) — These elements cover the producer decision, preparation and marketplace exception. | Producer response task and cancellation or refund gateway |

### 1.5 Quality incident and traceability

| Stakeholder goal / dependency | Strategic BPMN task | Operational BPMN task(s) | Planned Camunda element |
|---|---|---|---|
| Customer → Marketplace Platform (Safe, traceable food) | Manage quality incident & traceability (`Task_A1`) | Proposed: Log the report and identify the affected product. | Incident report form and incident ID |
| Marketplace Administrator → Marketplace Platform (Traceability records retrievable) | Manage quality incident & traceability (`Task_A1`) | Proposed: Look up the producer and match affected products or batches to order lines. | Order-line lookup by product or batch |
| Marketplace Administrator → Producer (Incident information supplied) | Manage quality incident & traceability (`Task_A1`) | Proposed: Request producer information, assess the evidence and route to closure review or escalation. | Producer response form and risk assessment gateway |
| Customer → Marketplace Platform (Safe, traceable food) | Manage quality incident & traceability (`Task_A1`) | Proposed: Suspend the affected product where appropriate after risk is confirmed. | Product suspension service task |
| Marketplace Platform → Notification Service (Messages delivered)<br>Marketplace Administrator → Notification Service (Affected customers contacted) | Manage quality incident & traceability (`Task_A1`) | Proposed: Notify each affected customer and record each delivery outcome. | Notification task per customer and delivery-status record |
| Marketplace Administrator → Notification Service (Affected customers contacted) | Manage quality incident & traceability (`Task_A1`) | Proposed: Route failed deliveries to an alternative channel or manual follow-up. | Failure gateway and manual follow-up task |
| Customer → Marketplace Platform (Safe, traceable food) | Manage quality incident & traceability (`Task_A1`) | Proposed: Review the evidence, then close with reasons or request further action. | Authorised review task and closure decision gateway |
