# **Home Credit — Loan Against Property (LAP) AI Voice Agent**

## **🎯 Project Objectives**

**Project Name:** Home Credit LAP AI Voice Agent
- **Platform:** Retell AI
- **Purpose:** Assess customers' preliminary eligibility for a Loan Against Property.
- **Maximum Loan Offer:** ₹75 lakh
- **Build an AI Voice Agent:** Configure the agent using Retell AI.
- **Verify Customer Identity:** Verify the customer before sharing offer details.
- **Collect Customer Information:** Gather the required eligibility details.
- **Validate Eligibility:** Apply the specified business rules.
- **Route Eligible Customers:** Transfer qualified customers to a senior loan expert.

## **📋 Eligibility Criteria**

- **Property Type:** Residential, commercial, and industrial properties are accepted; agricultural properties are not accepted.
- **Ownership:** Sole and joint ownership are accepted.
- **Property Documents:** Original property documents must be available.
- **Loan Amount:** Maximum offer of ₹75 lakh.
- **Occupation:** Salaried and self-employed customers are accepted.
- **Income Mode:** Income must primarily be received through a bank account.
- **Property Market Value:** Record the customer's estimated market value.
- **Loan Tenure:** Between 3 and 15 years, inclusive.

## ** 🏗️ AI Voice Agent Flowchart**

flowchart TD
    A([AI Voice Agent Starts]) --> B[Greeting and Introduction]
    B --> C{Verify Customer Identity?}
    C -- No --> D[End Call Politely]
    C -- Yes --> E[Explain LAP Offer]
    E --> F[Ask Eligibility Questions]
    F --> G[Collect Customer Answers]
    G --> H[Store Data in State / Memory]
    H --> I{Customer Has Diversion?}
    I -- Yes --> J{Type of Diversion}
    J -- Busy --> K[Capture Callback Preference]
    K --> D
    J -- Existing LAP --> L[Route to Loan Transfer Specialist]
    L --> D
    J -- EMI Reduction --> M[Route to EMI Specialist]
    M --> D
    J -- Other --> N[Handle Query and Resume]
    I -- No --> O{All Required Data Collected?}
    N --> O
    O -- No --> F
    O -- Yes --> P[Validate Eligibility Rules]
    P --> Q{Meets All Eligibility Criteria?}
    Q -- Yes --> R[Eligible]
    Q -- No --> S[Not Eligible]
    R --> T[Handoff to Senior Loan Expert]
    T --> U([End Call])
    S --> V[Explain Outcome Politely]
    V --> U
    style A fill:#1f4e78,color:#fff,stroke:#163a5a
    style C fill:#fff2cc,color:#000,stroke:#d6b656
    style I fill:#fff2cc,color:#000,stroke:#d6b656
    style O fill:#fff2cc,color:#000,stroke:#d6b656
    style Q fill:#fff2cc,color:#000,stroke:#d6b656
    style R fill:#d9ead3,color:#000,stroke:#6aa84f
    style S fill:#f4cccc,color:#000,stroke:#cc0000
    style T fill:#d9ead3,color:#000,stroke:#6aa84f
    style D fill:#f4cccc,color:#000,stroke:#cc0000
    style U fill:#eeeeee,color:#000,stroke:#666
```

## **🧪 Testing Scenarios**

- **Test Case 1:** Fully eligible customer.
- **Test Case 2:** Customer with agricultural property.
- **Test Case 3:** Customer receiving income only in cash.
- **Test Case 4:** Customer without original property documents.
- **Test Case 5:** Customer requesting a 2-year tenure.
- **Test Case 6:** Customer requesting a 20-year tenure.
- **Test Case 7:** Customer requesting ₹90 lakh.
- **Test Case 8:** Customer with jointly owned property.
- **Test Case 9:** Customer with an existing LAP.
- **Test Case 10:** Customer requesting EMI reduction.

## **✅ Completion Criteria**

- **Identity Verification:** Verify identity before disclosing offer details.
- **Eligibility Validation:** Apply the business rules correctly.
- **Conversation Handling:** Handle interruptions and corrections.
- **Correct Routing:** Route eligible customers appropriately.
- **Testing:** Document test cases and results.

## **🚀 Project outcome **
Develop a reliable AI voice agent that performs preliminary LAP eligibility assessments and routes eligible customers to the appropriate Home Credit loan specialist.
