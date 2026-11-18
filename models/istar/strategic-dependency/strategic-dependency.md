# Strategic Dependency (SD) Model — BRFN Digital Marketplace

This model summarizes the strategic dependencies between the Bristol Regional Food Network (BRFN) marketplace stakeholders. Each labeled link reads **depender → dependee**: the depender relies on the dependee to provide the stated dependum. Dependency categories are marked **Task**, **Goal**, or **Softgoal**.

```mermaid
flowchart LR
  subgraph PROD[Producer]
    producer[Producer]
  end
  subgraph CUST[Customer]
    customer[Customer]
  end
  subgraph PLATFORM[Marketplace Platform]
    platform[Marketplace Platform]
  end
  subgraph ADMIN[Marketplace Administrator]
    admin[Marketplace Administrator]
  end
  subgraph CERT[Certification Verification Service]
    cert[Certification Verification Service]
  end
  subgraph PAY[Payment Service]
    payment[Payment Service - Sandbox]
  end
  subgraph NOTIFY[Notification Service]
    notify[Notification Service]
  end
  subgraph REG[Regulator - implicit]
    regulator[Regulatory obligations]
  end

  producer -->|Task: certification verified| cert
  producer -->|Goal: orders visible at least 48 hours ahead| platform
  producer -->|Goal: weekly settlement with audit trail| platform
  customer -->|Task: accurate stock and availability| platform
  customer -->|Softgoal: safe, traceable food| platform
  customer -->|Goal: clear supplier responsibility| platform
  platform -->|Task: accurate product and stock data| producer
  platform -->|Task: payment authorization or decline| payment
  platform -->|Task: message delivery and outcome| notify
  platform -->|Task: certification verification result| cert
  admin -->|Task: retrievable traceability records| platform
  admin -->|Task: affected customers contacted| notify
  admin -->|Task: incident information supplied| producer
  platform -->|Softgoal: compliance with privacy and financial rules| regulator

  classDef stakeholder fill:#e8f1fb,stroke:#24527a,stroke-width:1.5px,color:#142b40
  classDef system fill:#eaf6ed,stroke:#347345,stroke-width:1.5px,color:#183d22
  classDef external fill:#fff3dc,stroke:#9b6b16,stroke-width:1.5px,color:#52380b
  class producer,customer,admin stakeholder
  class platform system
  class cert,payment,notify,regulator external
```

## Dependency catalogue

| Depender | Dependee | Dependum | Type |
|---|---|---|---|
| Producer | Certification Verification Service | Certification verified | Task |
| Producer | Marketplace Platform | Orders visible at least 48 hours ahead | Goal |
| Producer | Marketplace Platform | Weekly settlement with audit trail | Goal |
| Customer | Marketplace Platform | Accurate stock and availability information | Task |
| Customer | Marketplace Platform | Safe, traceable food | Softgoal |
| Customer | Marketplace Platform | Clear per-supplier responsibility | Goal |
| Marketplace Platform | Producer | Accurate product and stock data | Task |
| Marketplace Platform | Payment Service | Payment authorized or declined | Task |
| Marketplace Platform | Notification Service | Messages delivered with outcome | Task |
| Marketplace Platform | Certification Verification Service | Verification result | Task |
| Marketplace Administrator | Marketplace Platform | Traceability records retrievable | Task |
| Marketplace Administrator | Notification Service | Affected customers contacted | Task |
| Marketplace Administrator | Producer | Incident information supplied | Task |
| Marketplace Platform | Regulator (implicit) | Privacy and financial-services compliance | Softgoal |

**Legend:** A **Task** dependency relies on an activity or result being delivered; a **Goal** dependency relies on an outcome; a **Softgoal** dependency relies on a quality or constraint whose satisfaction is qualitative.
