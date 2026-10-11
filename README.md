# **Home Credit — Loan Against Property (LAP) AI Voice Agent**

## **🎯 Project Objectives**

**Project Name:** Home Credit LAP AI Voice Agent
- **Platform:** [Retell AI](https://www.retellai.com/)
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

## **🤖 Prompt Sales_Agent_Ai
 It demonstrates the use of AI to handle customer communication, respond to queries, and assist with sales-related tasks.
For the detailed implementation, prompts, and assignment documentation, please refer to the project files in the link below.
[Prompt Sales_Agent_Ai](https://github.com/bhavanaunaidu/Sales_Agent_ai_assignment-/blob/main/SalesAgents%20AI)

## **🧪 Testing Scenarios

- **Test Case 0:** Initalised state.
  Create an internal state like:
    a.property_type = UNKNOWN
    b.ownership_status = UNKNOWN
    c.documents_available = UNKNOWN
    d.loan_amount = UNKNOWN
    e.occupation = UNKNOWN
    f.income_mode = UNKNOWN
    g.market_value = UNKNOWN
    h.tenure = UNKNOWN
  
- **Test Case 1:** Fully eligible customer.
  A salaried customer approaches the bank for a ₹50 lakh loan against a residential property worth ₹1 crore. The property is solely owned by the customer, all original property documents are available, and the customer receives their salary through a bank account. The customer requests a 10-year loan tenure and meets all the eligibility criteria.
  [**Test Case 1 Output**](https://drive.google.com/drive/folders/1Ipope6jllwqaueqlWNo14q5DRX_FYK3A?usp=sharing)
- **Test Case 2:** Customer with agricultural property.
  Agricultural Property: A customer applies for a loan against agricultural land. During the initial conversation, the customer confirms that the property offered as collateral is agricultural. The agent identifies that the property type does not meet the product's eligibility requirements and disqualifies the customer immediately.
  [**Test Case 2 Output**](https://drive.google.com/drive/folders/1XAUlGqfAxQfQWzK_hSKbPXg8a25dCxm3?usp=sharing)
- **Test Case 3:** Customer receiving income only in cash.
  Cash Income: A self-employed customer applies for a loan against their residential property. When asked about their income source, the customer explains that most of their business income is received in cash. The agent identifies that the income source does not meet the product's verification requirements and disqualifies the customer immediately.
  [**Test Case 3 Output**](https://drive.google.com/drive/folders/1vAHJ5YTovZ2C8X_fX1A0xY31x4RWG0zd?usp=sharing)
- **Test Case 4:** Customer without original property documents.
  Missing Original Documents: A customer applies for a loan against their residential property but informs the agent that the original property documents are unavailable and only photocopies can be provided. The agent recognizes that original documents are mandatory for the loan product and immediately disqualifies the customer.
  [**Test Case 4 Output**](https://drive.google.com/drive/folders/1rLvdeXkV1yo0-0VUwlu9UflA-Oy8d1_K?usp=sharing)
- **Test Case 5:** Customer requesting a 2-year tenure.
  Tenure Too Short: A customer applies for a loan against their residential property and requests a repayment tenure of two years. Although the customer may meet the other eligibility criteria, the requested tenure falls outside the permitted range. The agent identifies the tenure mismatch and disqualifies the customer according to the configured business rules.
  [**Test Case 5 Output**](https://drive.google.com/drive/folders/1GneF5By5HyHiKF5Nqef-l_fsVnU4GC4h?usp=sharing)
- **Test Case 6:** Customer requesting a 20-year tenure.
  Tenure Too Long: A customer applies for a loan against their residential property and requests a repayment tenure of 20 years. The requested tenure exceeds the product's maximum permitted tenure of 10 years. The agent identifies the mismatch, explains the applicable tenure limit, and follows the configured disqualification process.
  [**Test Case 6 Output**](https://drive.google.com/drive/folders/1xiPS35zb2R3H0mmO1MRl5Od9ytyeUK6h?usp=sharing)
- **Test Case 7:** Customer requesting ₹90 lakh.
  Loan Amount Exceeds the Limit: A customer owns a residential property worth ₹1.5 crore and requests a loan of ₹90 lakh. The agent explains that the maximum loan amount available under the product is ₹75 lakh and asks whether the customer would like to proceed with a ₹75 lakh loan instead. If the customer agrees, the agent continues the qualification process with the revised amount.
  [**Test Case 7 Output**](https://drive.google.com/drive/folders/1jqL552el6xfI_i9GS75O5xmMp_wV4pGi?usp=sharing)
- **Test Case 8:** Customer with jointly owned property.
   Joint Ownership: A customer applies for a loan against a residential house jointly owned with their wife. The customer confirms that both names are associated with the property ownership. The agent records the ownership status as joint and continues the qualification process by asking the next unanswered eligibility question without disqualifying the customer solely because of joint ownership.
  [**Test Case 1 Output**](https://drive.google.com/drive/folders/1plrK6dnw4xiREaMChvUZLyt9ZCIChPpI?usp=sharing)
- **Test Case 9:** Customer with an existing LAP.
  Existing Loan Against the Property: A customer begins the application process for a loan against their residential property but reveals that an existing loan is already secured against the same property. The agent recognizes that the case requires a specialist assessment, transfers the customer to the designated specialist flow, and ends the standard qualification conversation.
  [**Test Case 9 Output**](https://drive.google.com/drive/folders/1ilXiT73-rcI4WxopQfxH8i0ts6qtXdru?usp=sharing)
- **Test Case 10:** Customer requesting EMI reduction.
  EMI Reduction Request: A customer initially expresses interest in a loan against their property but later clarifies that their actual requirement is to reduce the EMI on an existing loan. The agent recognizes the customer's changed intent, stops the standard loan qualification process, transfers the customer to the appropriate specialist, and ends the current flow.
  [**Test Case 10 Output**](https://drive.google.com/drive/folders/1ilXiT73-rcI4WxopQfxH8i0ts6qtXdru?usp=sharing)
- **Test Case 11:** Customer with an existing LAP.
  Out-of-Order Answers: During the initial conversation, a customer spontaneously explains that they own a residential house worth approximately ₹1.2 crore jointly with their wife, before the agent has asked separate questions about property type, market value, and ownership. The agent extracts and stores all three details in its internal state, avoids asking the customer to repeat the information, and proceeds by asking only the next required eligibility question that remains unanswered.
  [**Test Case 11 Output**](https://drive.google.com/drive/folders/1QwcCnKCZTROHuz2gJrYqQu8o2rM8XLU_?usp=sharing)
- **Test Case 12:** Customer requesting EMI reduction.
  Busy Customer: During the loan qualification conversation, the customer informs the agent that they are currently in a meeting and cannot continue. The agent politely acknowledges the situation and asks, “Certainly. What would be a convenient time for us to call you back?” The agent then ends the current conversation and follows the configured callback workflow if the customer provides a suitable time.
  [**Test Case 12 Output**](https://drive.google.com/drive/folders/1XyYrpNEmNYpzdpMpKve2fsLR0wKA4c_a?usp=sharing)

## **🚀 Project outcome **

Develop a reliable AI voice agent that performs preliminary LAP eligibility assessments and routes eligible customers to the appropriate Home Credit loan specialist.
- **Identity Verification:** Verify identity before disclosing offer details.
- **Eligibility Validation:** Apply the business rules correctly.
- **Conversation Handling:** Handle interruptions and corrections.
- **Correct Routing:** Route eligible customers appropriately.
- **Testing:** Document test cases and results.
