# DanaShift — AI resolution architecture

## Target workflow

```mermaid
%%{init: {"flowchart": {"htmlLabels": true, "nodeSpacing": 35, "rankSpacing": 45}, "themeVariables": {"fontFamily": "Arial, sans-serif", "fontSize": "14px"}}}%%
flowchart TD
    A["Customer request"] --> B["Protect personal data"]
    B --> C["Understand intent"]
    C --> D["Assess urgency"]
    D --> E["Extract context"]
    E --> F{"In scope?"}
    F -->|No| G["Offer assistance"]
    F -->|Yes| H{"Critical case?"}
    H -->|Yes| I["Escalate to specialist"]
    H -->|No| J["Retrieve knowledge"]
    I --> J
    J --> K["Diagnose issue"]
    K --> L{"Enough evidence?"}
    L -->|No| M["Clarify symptoms"]
    M --> B
    L -->|Yes| N["Propose solution"]
    N --> O{"Staff approval?"}
    O -->|Revise| K
    O -->|Approved| P["Authorized actions"]
    P --> Q["Verify outcome"]
    Q --> R{"Resolved?"}
    R -->|No| J
    R -->|Yes| S["Close case"]
    classDef core fill:#e4ecd9,stroke:#49644d,color:#182b22
    classDef review fill:#ffe7ce,stroke:#d67a36,color:#55331e
    class B,C,D,E,J,K,N core
    class I,O,Q review
```

## Proposed interaction sequence

```mermaid
sequenceDiagram
    participant U as Customer / Staff
    participant P as Privacy layer
    participant A as AI agent
    participant K as Approved knowledge
    participant H as Human reviewer
    participant T as Authorized tools
    U->>P: Report issue
    P->>A: Masked message and case context
    A->>A: Understand intent, urgency and entities
    alt Out of scope
        A-->>U: Explain scope or offer human support
    else Within scope
        opt Critical or sensitive
            A-->>H: Recommend immediate escalation
        end
        A->>K: Retrieve relevant evidence
        K-->>A: Documentation and prior cases
        loop Until sufficient context or escalation
            A-->>U: Ask targeted questions when needed
            U->>P: Additional details
            P->>A: Updated masked context
        end
        A->>A: Assess likely causes and draft resolution plan
        A-->>H: Evidence, recommendations and review flags
        alt Authorized action approved
            H->>T: Approve scoped action
            T-->>A: Execution result
            A-->>U: Reviewed guidance and follow-up
        else Revise or escalate
            H-->>A: Feedback or specialist handoff
        end
        A-->>H: Verify outcome before case closure
    end
```

## Implementation boundary

The notebook explores masking, classification, entity alignment, semantic search and evaluation. The browser prototype is rule-based and does not execute the target sequence. Model checkpoints, grounded reasoning, multi-turn case state, verified knowledge, authenticated adapters and authorization controls are future integration work.

Critical or uncertain cases require specialist review. Recommendations must be evidence-grounded; actions must be explicitly authorized and outcomes verified before marking cases resolved.
