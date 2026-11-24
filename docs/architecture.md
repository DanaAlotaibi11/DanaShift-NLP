# Proposed architecture

```mermaid
sequenceDiagram
 participant U as Staff
 participant P as Privacy filter
 participant A as Agent
 participant K as Knowledge base
 participant T as Tools
 U->>P: Customer request
 P->>A: Masked text
 A->>A: Classify and extract entities
 alt In scope and sufficient confidence
 A->>K: Retrieve evidence
 K-->>A: Sources
 A->>T: Policy-approved actions
 T-->>A: Results
 else Out of scope or uncertain
 A->>A: Skip operational tools
 end
 A-->>U: JSON draft and review flags
```

The browser demo is a rule-based sandbox. Production integration requires trained model checkpoints, verified knowledge sources, authenticated tool adapters and authorization controls.
