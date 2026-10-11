# **Home Credit — Loan Against Property (LAP) AI Voice Agent**

## **🎯 Project Objectives**

**Project Name:** Home Credit LAP AI Voice Agent
- **Platform:** Retell AI [Open Retell AI](https://www.retellai.com/)
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

## ** 🏗️ AI Voice Agent Structure**

                    AI VOICE AGENT
                          │
          ┌───────────────┴───────────────┐
          │                               │
   Conversation Layer               Business Logic
          │                               │
 Greeting → Offer → Questions       Eligibility Rules
          │                               │
          └───────────────┬───────────────┘
                          │
                    State / Memory
                          │
            ┌─────────────┴─────────────┐
            │                           │
     Customer Answers             Diversions
            │                           │
            └─────────────┬─────────────┘
                          │
                     Final Decision
                          │
             ┌────────────┴────────────┐
             │                         │
          Eligible                 Not Eligible
             │                         │
        Human Handoff               End Call
        

## ** 🔄 Loan Against Property (LAP) Work-Flow **

START
  ↓
Greeting
  ↓
Verify Customer
  ↓
Customer Busy?
  ├── YES → Ask callback time → End
  └── NO
       ↓
Explain LAP Offer
       ↓
Check Existing Loan / EMI Transfer
  ├── YES → Transfer specialist message → End
  └── NO
       ↓
Eligibility Questions
       ↓
1. Property Type
       ↓
2. Ownership
       ↓
3. Original Documents
       ↓
4. Loan Amount
       ↓
5. Occupation + Income Mode
       ↓
6. Property Market Value
       ↓
7. Tenure
       ↓
Eligibility Decision
       ├── FAIL → Explain → End
       └── PASS
             ↓
       Senior Loan Expert Handoff
             ↓
           END

## **🧪 Testing Scenarios**

- **Test Case 0:** Initalised state.
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
