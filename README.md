flowchart TD
    A["AI VOICE AGENT"]

    A --> B["Conversation Layer"]
    A --> C["Business Logic"]

    B --> D["Greeting → Offer → Questions"]
    C --> E["Eligibility Rules"]

    D --> F["State / Memory"]
    E --> F

    F --> G["Customer Answers"]
    F --> H["Diversions"]

    G --> I{"Final Decision"}
    H --> J["Handle Diversion"]

    I -->|Eligible| K["Human Handoff"]
    I -->|Not Eligible| L["End Call"]

    J --> M["Specialist Transfer / Callback / End"]

    style A fill:#1f4e79,color:#ffffff,stroke:#163a5c
    style B fill:#d9eaf7,color:#000000,stroke:#1f4e79
    style C fill:#d9eaf7,color:#000000,stroke:#1f4e79
    style F fill:#fff2cc,color:#000000,stroke:#d6b656
    style I fill:#e1d5e7,color:#000000,stroke:#9673a6
    style K fill:#d5e8d4,color:#000000,stroke:#82b366
    style L fill:#f8cecc,color:#000000,stroke:#b85450
    style M fill:#ffe6cc,color:#000000,stroke:#d79b00
