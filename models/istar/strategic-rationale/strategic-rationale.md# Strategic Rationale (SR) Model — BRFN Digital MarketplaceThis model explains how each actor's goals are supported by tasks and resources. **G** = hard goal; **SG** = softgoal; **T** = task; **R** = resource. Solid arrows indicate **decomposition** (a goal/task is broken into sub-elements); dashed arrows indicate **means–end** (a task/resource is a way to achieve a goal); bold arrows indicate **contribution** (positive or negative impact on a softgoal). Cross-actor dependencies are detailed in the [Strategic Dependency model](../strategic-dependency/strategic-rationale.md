# Strategic Rationale (SR) Model — BRFN Digital Marketplace

This model explains how each actor's goals are supported by tasks and resources. **G** = hard goal; **SG** = softgoal; **T** = task; **R** = resource. Solid arrows indicate **decomposition** (a goal/task is broken into sub-elements); dashed arrows indicate **means–end** (a task/resource is a way to achieve a goal); bold arrows indicate **contribution** (positive or negative impact on a softgoal). Cross-actor dependencies are detailed in the [Strategic Dependency model](../strategic-dependency/strategic-dependency.md).

```mermaid
flowchart LR
  subgraph PRODUCER[Producer]
    p_sell([G: Sell beyond farm gate])
    p_register[T: Register and list products]
    p_submit[T: Submit product details]
    p_season[T: Update seasonal availability]
    p_verify[T: Obtain certification verification]
    p_fulfil[T: Prepare and fulfil orders]
    p_trust{{SG: Be trusted by customers}}
    p_certR[(R: Certification result)]
    p_data[(R: Product and stock data)]
    p_sell -->|decomposed into| p_register
    p_sell -->|decomposed into| p_fulfil
    p_register -->|decomposed into| p_submit
    p_register -->|decomposed into| p_season
    p_register -->|decomposed into| p_verify
    p_certR -.->|means-end| p_trust
    p_data -.->|means-end| p_trust
  end

  subgraph CUSTOMER[Customer]
    c_local([G: Buy local produce conveniently])
    c_browse[T: Browse and search catalogue]
    c_checkout[T: Complete single multi-vendor checkout]
    c_responsibility([G: Know supplier responsibility])
    c_safe{{SG: Be confident food is safe}}
    c_origin[T: Check farm origin and harvest date]
    c_trace[T: Use product traceability information]
    c_local -->|decomposed into| c_browse
    c_local -->|decomposed into| c_checkout
    c_checkout ==>|positive| c_local
    c_origin -.->|means-end| c_safe
    c_trace -.->|means-end| c_safe
  end

  subgraph PLATFORM[Marketplace Platform]
    m_trusted([G: Operate a trusted marketplace])
    m_verified([G: Publish only verified listings])
    m_validate[T: Validate listing data]
    m_checkCert[T: Check certification]
    m_publish[T: Publish approved listing]
    m_orders([G: Aggregate multi-vendor orders correctly])
    m_stock[T: Validate stock and availability]
    m_split[T: Create producer-specific sub-orders]
    m_payment([G: Process payment securely])
    m_payTask[T: Submit payment and handle outcome]
    m_commission[T: Calculate and retain 5% commission]
    m_settle([G: Distribute weekly producer payments])
    m_audit[T: Record settlement and audit trail]
    m_trace([G: Maintain product-to-customer traceability])
    m_records[(R: Order, producer and product records)]
    m_reliable{{SG: Be reliable and trustworthy}}
    m_trusted -->|decomposed into| m_verified
    m_trusted -->|decomposed into| m_orders
    m_trusted -->|decomposed into| m_payment
    m_trusted -->|decomposed into| m_settle
    m_trusted -->|decomposed into| m_trace
    m_validate -->|decomposed into| m_checkCert
    m_validate -->|decomposed into| m_publish
    m_checkCert -.->|means-end| m_verified
    m_publish -.->|means-end| m_verified
    m_stock -->|decomposed into| m_split
    m_stock -.->|means-end| m_orders
    m_split -.->|means-end| m_orders
    m_payTask -.->|means-end| m_payment
    m_commission -.->|supports| m_settle
    m_audit -.->|means-end| m_settle
    m_records -.->|means-end| m_trace
    m_verified ==>|positive| m_reliable
    m_trace ==>|positive| m_reliable
    m_payment ==>|positive| m_reliable
    m_commission -.->|trade-off: cost to customer| m_reliable
  end

  subgraph ADMIN[Marketplace Administrator]
    a_respond([G: Respond to quality incidents])
    a_investigate[T: Investigate complaint]
    a_protect([G: Protect the public from unsafe stock])
    a_identify[T: Identify affected products, producers and orders]
    a_suspend[T: Suspend unsafe product]
    a_contact[T: Notify affected customers]
    a_close[T: Review and close incident with justification]
    a_accountable{{SG: Be impartial and accountable}}
    a_respond -->|decomposed into| a_investigate
    a_respond -->|decomposed into| a_protect
    a_protect -->|decomposed into| a_identify
    a_protect -->|decomposed into| a_suspend
    a_protect -->|decomposed into| a_contact
    a_respond -->|decomposed into| a_close
    a_identify -.->|means-end| a_protect
    a_close ==>|positive| a_accountable
    a_investigate ==>|positive| a_accountable
  end

  subgraph EXTERNAL[External services]
    x_cert([G: Verify certification accurately])
    x_pay([G: Process payments securely])
    x_notify([G: Deliver notifications and report outcome])
  end

  p_verify -.->|means-end| p_trust
  m_checkCert -.->|means-end| x_cert
  m_payTask -.->|means-end| x_pay
  a_contact -.->|means-end| x_notify

  classDef goal fill:#e7f0ff,stroke:#24527a,stroke-width:1.5px,color:#142b40
  classDef softgoal fill:#fff3dc,stroke:#9b6b16,stroke-width:1.5px,color:#52380b
  classDef task fill:#eaf6ed,stroke:#347345,stroke-width:1.2px,color:#183d22
  classDef resource fill:#f1eafe,stroke:#7650a5,stroke-width:1.2px,color:#35224a
  class p_sell,c_local,c_responsibility,m_trusted,m_verified,m_orders,m_payment,m_settle,m_trace,a_respond,a_protect,x_cert,x_pay,x_notify goal
  class p_trust,c_safe,m_reliable,a_accountable softgoal
  class p_register,p_submit,p_season,p_verify,p_fulfil,c_browse,c_checkout,c_origin,c_trace,m_validate,m_checkCert,m_publish,m_stock,m_split,m_payTask,m_commission,m_audit,a_investigate,a_identify,a_suspend,a_contact,a_close task
  class p_certR,p_data,m_records resource
```

## Rationale highlights

- **Producer:** Listing, keeping availability current, and fulfilling orders support selling beyond the farm gate; verified claims and reliable product data support customer trust.
- **Customer:** Catalogue search and one multi-vendor checkout support convenient local purchasing. Origin, harvest, and traceability information support confidence in food safety.
- **Marketplace Platform:** Verification, order aggregation, secure payment, weekly settlement, and traceability jointly support a trusted marketplace. The 5% commission supports the revenue model, with a potential affordability trade-off to monitor.
- **Marketplace Administrator:** Investigation, product suspension, customer contact, and documented closure support incident response and public protection while reinforcing accountability.
- **External services:** Certification, payment, and notification services provide capabilities used by the platform and administrator; their detailed dependencies appear in the SD model.
