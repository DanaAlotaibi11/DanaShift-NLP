# DanaShift — AI resolution architecture

## Target workflow

```mermaid
flowchart TD
    A["Customer message · Arabic / English"] --> B["Privacy masking"]
    B --> C["Contextual understanding · intent & urgency"]
    C --> D["Entity extraction & case context"]
    D --> E{"Within service scope?"}
    E -->|No| F["Explain scope · offer human assistance"]
    E -->|Yes| G{"Critical or sensitive?"}
    G -->|Yes| H["Recommend immediate specialist escalation"]
    G -->|No| I["Retrieve approved knowledge & previous cases"]
    H --> I
    I --> J["Reason over evidence · identify likely causes"]
    J --> K{"Enough context and evidence?"}
    K -->|No| L["Ask targeted follow-up questions"]
    L --> B
    K -->|Yes| M["Recommend a resolution plan"]
    M --> N["Human review & authorization"]
    N -->|Approved| O["Authorized tools · ticket / CRM / scheduling"]
    N -->|Revise| J
    O --> P["Verify outcome & follow up"]
    P --> Q{"Issue resolved?"}
    Q -->|Yes| R["Close case · record outcome"]
    Q -->|No| I
    classDef core fill:#e4ecd9,stroke:#49644d,color:#182b22
    classDef review fill:#ffe7ce,stroke:#d67a36,color:#55331e
    class B,C,D,I,J,M core
    class H,N,P review
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
