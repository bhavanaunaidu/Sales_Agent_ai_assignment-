AI Voice Agent for Home Credit Loan Against Property (LAP)

1. Abstract
This project presents the design and testing of an AI voice agent that makes outbound calls on behalf of Home Credit to existing customers. The agent introduces a Loan Against Property (LAP) offer of up to ₹75 lakh and carries out a preliminary eligibility check through natural conversation. It verifies the customer's identity, handles busy or uninterested customers, detects existing-loan and EMI-reduction requests, and collects seven eligibility items. It remembers answers given out of order, accepts corrections, and disqualifies customers immediately when a mandatory rule fails. Customers who pass every check are handed over to a senior loan expert.
2. Introduction
Banks and non-banking financial companies make thousands of outbound calls every day to find customers who may be interested in a loan. Most of these early calls are repetitive. A human agent asks the same set of questions, records the answers, and decides whether the customer is worth passing to a senior executive. This is costly and inconsistent.
Conversational AI can take over this first-level screening. A voice agent can call at scale, ask the same questions every time, apply the same eligibility rules without bias, and pass only qualified leads to human experts. This project applies that idea to one product: Loan Against Property (LAP).
What is a Loan Against Property? A LAP is a secured loan in which the borrower pledges a property (residential, commercial or industrial) as collateral and receives funds, usually repaid in monthly instalments (EMIs) over several years.
3. Problem Statement
To build a voice agent that can:
1.	Call an existing customer, confirm identity, and check whether they can talk.
2.	Present the LAP offer of up to ₹75 lakh in a professional, non-pushy way.
3.	Detect customers who already have a property loan or want a lower EMI, and route them to a loan-transfer specialist.
4.	Collect and validate seven eligibility items in a natural conversation.
5.	Remember everything the customer says, even when answers come out of order.
6.	Disqualify ineligible customers at once and politely.
7.	Hand over eligible customers to a senior loan expert only after every check is complete.
4. Objectives
•	Design a robust, reusable system prompt for a telephone voice agent.
•	Define clear conversation stages and a step-by-step processing order.
•	Maintain an internal state so no question is asked twice.
•	Prevent the agent from inventing interest rates, fees or policies.
•	Create a test plan that covers normal, edge and failure cases.
•	Record evidence (call recordings, transcripts, results) to prove that the agent works.
5. Scope and Assumptions
In scope: outbound qualification calls in English or Hindi, identity verification, eligibility screening, transfer routing, callback capture, and handoff.
Out of scope: final credit approval, interest-rate quotation, document collection, and actual loan disbursement. The agent is a preliminary qualification assistant only and never promises approval.
Assumptions:
•	The platform supplies dynamic variables such as the customer name and current time.
•	The platform provides end-call and transfer actions.
•	Product facts come from an approved knowledge base. The agent must not invent any.
6. Tools and Technologies
The agent runs on Retell AI as a single-prompt agent, and the AI speaks first. Retell provides telephony, speech-to-text, the language model and text-to-speech. A knowledge base supplies approved product notes.
Setting	Value
Platform	Retell AI (single prompt agent)
Begin message	AI speaks first, greeting by time of day
Voice	Professional Indian-English female voice
Language	English (Hindi tested separately)
Interruption sensitivity	0.6
Response wait time	750 ms, dynamic
Reminder	After 10 seconds, 2 times
Denoising	Remove noise
Transcription mode	Optimize for accuracy
Boosted keywords	lakh, crore, EMI, LAP, residential, commercial, industrial, agricultural
End call on silence	25 seconds
Max call duration	10 minutes
Function	End Call
Post-call extraction	12 fields (property type, ownership, documents, loan amount, occupation, income mode, market value, tenure, call outcome, and more)
Dynamic variable values used in the test calls: company_name = Home Credit, customer_name = Bhavana (or Shiva), agent_name = Zara, agent_gender = Female, language_to_speak = English. The date, day and time were set to the real values before each call.
7. System Design
7.1 High-Level Architecture
The agent works in a loop on every customer turn:
1.	Speech-to-text converts the customer's voice into text.
2.	The language model, guided by the system prompt, reads the text and the conversation history.
3.	The model updates its internal state and decides what to say.
4.	Text-to-speech converts the reply into a natural voice.
5.	Platform actions (end call, transfer) are triggered when the conversation reaches a terminal outcome.
7.2 Dynamic Variables
The prompt uses placeholders that the platform fills in at call time:
Variable	Meaning
{{company_name}}	Name of the lender (Home Credit)
{{customer_name}}	Name of the person being called
{{agent_name}} and {{agent_gender}}	Identity of the agent, used for consistent tone and correct Hindi grammar
{{current_date}}, {{current_day}}, {{current_time}}	Used for callback scheduling
{{language_to_speak}}	English or Hindi
{{additional_context_from_rag}}	Approved product knowledge
{{conversation_history}} and {{customer_utterance}}	Dialogue so far and the latest reply
7.3 Internal State Management
The prompt tells the agent to keep a silent mental notebook and never read it out. The notebook holds the following.
Group	What is tracked
Identity and timing	Customer verified, busy or free, callback time if given
Eligibility answers	Property type, ownership, original documents, loan amount, occupation, income mode, market value, tenure (work and income count as two separate facts)
Flags	Existing loan on the property, call ended or about to end
Five habits keep the notebook reliable:
•	The latest clear statement wins. "Ten years, no, make it twelve" is stored as twelve.
•	Only clear answers count. "The papers are somewhere at home, I think" triggers one confirming question.
•	The agent does not read between the lines. A monthly salary figure does not say whether income is bank or cash, so the agent asks.
•	Spoken amounts are converted correctly: one lakh is 1,00,000 and one crore is 1,00,00,000.
•	Facts given early count, and the notebook is checked before every question, so nothing is asked twice, including property value and tenure.
Because the state is updated after every reply, the agent can use information given at any time and never repeats a question already answered.
7.4 Mandatory Processing Order
Before every reply the agent runs a silent six-step check, which is never spoken aloud.
1.	What facts did the customer just give, including ones I did not ask for?
2.	Does any of it break a requirement? If yes, end the call politely.
3.	Did they mention an existing loan or a lower EMI? If yes, give the transfer message and end.
4.	Which of the seven answers are still missing? Take the earliest one.
5.	Did they ask a question? Answer it in one sentence first.
6.	Reply with a short acknowledgement and one question, with no list and nothing repeated.
The prompt also uses these techniques: a clear role and objective, more than a dozen worked examples (few-shot), a list of things to avoid, written-out edge cases (busy customer, wrong person, interruptions, corrections, repeated questions) and a fixed closing flow so every call ends cleanly.


8. Conversation Flow
The call moves through four stages.
Stage A: Greeting and verification. The agent asks for the customer by name. If the person is the wrong contact, the agent apologises and discloses nothing about the offer. If the customer is busy, the agent stops the pitch, asks for a convenient callback time, and ends the call.
Stage B: Presenting the offer. Only after verification and confirmation that the customer can talk, the agent introduces the LAP offer of up to ₹75 lakh and asks permission to ask a few questions.
Stage C: Existing loan or lower EMI. The agent never asks about existing loans, because that is not one of the seven questions. If at any point the customer says there is already a loan on the property, or asks to lower or move an existing EMI, the agent stops the questions, says that a loan-transfer specialist will contact them shortly, and ends the call. A loan on something else, such as a car, does not trigger this.
Stage D: Seven eligibility items. The agent collects the items listed in the next section.
9. Eligibility Criteria
#	Item	Accepted	Immediate outcome if it fails
1	Property type	Residential, commercial, industrial	Agricultural property: disqualify
2	Ownership	Sole or joint	Both are accepted
3	Original documents	Available for verification	Clearly unavailable: disqualify
4	Requested loan amount	Greater than zero, up to ₹75 lakh	Above ₹75 lakh: offer the ₹75 lakh maximum; if declined, end politely
5	Occupation and income mode	Salaried or self-employed, with income received through a bank	Cash income: disqualify
6	Property market value	Any estimate is recorded	No minimum is imposed
7	Repayment tenure	3 to 15 years, inclusive	Outside this range: disqualify unless the customer accepts a valid tenure
Notes on special handling:
•	Joint ownership is never a reason to reject a customer.
•	Being self-employed is never a reason to reject a customer.
•	If the customer earns from both bank and cash sources, the agent asks which income applies to the proposed loan instead of guessing.
•	Uncertain answers (for example, "I think the papers are somewhere at home") are treated as unknown, and the agent asks a clarifying question.
10. Handling Real Conversations
Real customers do not answer neatly, so the prompt includes specific rules for natural behaviour.
Out-of-order answers. If the customer says, "It's a residential house, jointly owned with my wife, worth around ₹1 crore. I need about ₹40 lakh," the agent stores four facts at once and moves on to the next missing item (original documents).
Corrections. The latest clear answer wins. If the customer says "It's residential. Sorry, I mean it's agricultural," the agent disqualifies immediately. If the customer contradicts themselves without saying which answer is correct, the agent asks for clarification.
Interruptions and side questions. The agent answers briefly using approved information, records any new facts, and returns to the first unanswered item.
Interest rate and fee questions. The agent never invents numbers. For the interest rate it says that the senior loan expert will explain it after the preliminary check.
Customer refusal. The agent respects the decision, does not pressure the customer, and ends the call politely.
11. Safety and Responsible AI Measures
•	No invented facts: rates, fees, timelines and policies come only from the approved knowledge base.
•	Privacy: the offer and account details are never disclosed to an unverified person.
•	No false promises: the agent never promises approval or disbursement, and describes the expert callback as expected, not guaranteed, unless the workflow confirms it.
•	No pressure: the customer is never pushed to take a loan.
•	Uncertainty is not a pass: silence or unclear answers are never treated as eligibility.
•	Single question per turn: this avoids confusing the customer and keeps the call natural.
12. Final Handoff Gate
The agent may hand over a customer to a senior loan expert only when all of these are true:
1.	The identity has been verified.
2.	The customer has agreed to continue.
3.	No loan-transfer condition has been triggered.
4.	All seven checklist items are clearly answered.
5.	Every applicable criterion passes.
6.	No unresolved contradiction affects eligibility.
7.	No disqualification flag is active.
Only then does the agent say that the responses appear to meet the basic criteria, that a senior expert will explain the exact interest rate and next steps, and that final approval depends on the lender's verification.
13. Testing and Results
I prepared fifteen test scenarios covering normal, edge and failure cases.
Test	Scenario	Expected result	Observed result	Audio	Result
1	Perfect eligible customer	Handoff to senior loan expert	All seven questions asked once, then the callback message and the call ended	Yes	Pass
2	Agricultural property	Disqualified, call ends	Disqualified right after the property type answer, no more questions	Yes	Pass
3	Cash income	Disqualified, call ends	"Mostly in cash" led to disqualification; value and tenure were not asked	Yes	Pass
4	Missing original documents	Disqualified, call ends	Photocopies only led to immediate disqualification	Yes	Pass
5	Tenure too short (2 years)	Disqualified, call ends	Disqualified after the tenure answer	Yes	Pass
6	Tenure too long (20 years)	Disqualified, call ends	Disqualified after the tenure answer	Transcript only	Pass
7	Loan amount 90 lakh	Limit explained, asks to proceed with 75 lakh	Limit explained, customer accepted 75 lakh, call continued to handoff	Yes	Pass
8	Joint ownership	Accepted, call continues	Joint ownership accepted, call ended with the callback message	Transcript only	Pass
9	Existing loan	Transfer specialist message, call ends	Transfer message given as soon as the loan was mentioned	Yes	Pass
10	EMI reduction	Transfer specialist message, call ends	Transfer message given right after the greeting	Yes	Pass
11	Out-of-order answers	Next question is the first missing item	Type, ownership and value captured; next question was documents; value never asked again	Yes	Pass
12	Busy customer	Asks callback time, call ends	No pitch; 6 pm callback confirmed; call ended	Yes	Pass
13	Contradiction (residential, then agricultural)	Final answer used, disqualified	Agricultural used, disqualified	Transcript only	Pass
14	Many answers in one sentence	All captured, none asked again	Facts captured across turns and nothing repeated; documents confirmed once after a speech error	Yes	Pass
15	Interruption (which documents?)	Short answer, then back to the question	Short answer, then the same question asked again; call continued	Transcript only	Pass
16	Vague answer about documents	Clarifying question, not counted as yes	Not yet run	Pending	Pending
Results: All 15 completed scenarios matched the expected outcome. Points worth noting from the transcripts:
•	Audio exists for 11 of the 15 calls. Tests 6, 8, 13 and 15 have simulation transcripts only because the free usage limit ran out; the audio will be added.
•	Speech recognition sometimes misheard the customer (the first reply in Tests 11 and 12, and "voucher documents" in Test 14). The agent asked again or confirmed instead of guessing.
•	In Test 7 one agent sentence was split by an interruption, but the call continued correctly.
•	In Test 10 the customer only asked to reduce an EMI, and the agent said there was already a loan on the property. This is a reasonable inference, but the customer did not say it.
•	Scenario 16 still needs a run and a transcript.
14. Scenarios and Results
A.	Test 1 – Perfect Eligible Customer: 
In this scenario, the customer meets all the predefined eligibility criteria for a Loan Against Property. The customer owns a residential property solely, has the original property documents available, is salaried, receives income through a bank, requires a loan amount of ₹50 lakh, owns a property valued at ₹1 crore, and requests a tenure of 10 years. The AI Voice Agent should capture all the details accurately, validate them against the eligibility rules, and mark the customer as QUALIFIED. The agent should then initiate the specialist handoff for further processing. The expected result is successful qualification and handoff.
RESULT: Test 1 – Perfect Eligible Customer

B.	Test 2 – Agricultural Property:
 In this scenario, the customer informs the AI Voice Agent that the property intended for the loan is agricultural land. Since agricultural property is excluded under the configured eligibility criteria, the agent should identify the property type and immediately disqualify the customer. It should politely explain that the property does not meet the requirements for the offer and end the call without asking further qualification questions. The expected result is immediate disqualification.
RESULT: Test 2 – Agricultural Property

C.	Test 3 – Cash-Based Income:
 In this scenario, the customer is self-employed and explains that their income is received in cash. The AI Voice Agent should identify the employment type and income source, compare them against the configured eligibility rules, and disqualify the customer if cash-based income is not accepted. The agent should communicate the decision politely and end the qualification process. The expected result is immediate disqualification based on the specified income rule.
RESULT: Test 3 – Cash-Based Income

D.	Test 4 – Original Property Documents Unavailable:
 In this scenario, the customer confirms that the property is residential but states that the original property documents are unavailable. Since the availability of original documents is a mandatory requirement under the given criteria, the AI Voice Agent should record the response, identify the unmet requirement, and stop the qualification process. The agent should explain the requirement courteously and end the call. The expected result is immediate disqualification due to missing original documents.
RESULT: Test 4 – Original Property Documents Unavailable

E.	Test 5 – Tenure Too Short: 
In this scenario, the customer requests a loan amount of ₹30 lakh but wishes to repay the loan within two years. The AI Voice Agent should capture the requested tenure and compare it with the minimum tenure permitted under the approved LAP policy. If two years is below the permitted minimum, the agent should disqualify the customer, explain that the requested tenure falls outside the eligible range, and end the call. The expected result is disqualification due to a tenure that is too short.
RESULT: Test 5 – Tenure Too Short: 

F.	Test 6 – Tenure Too Long: 
In this scenario, the customer requests a Loan Against Property with a repayment tenure of 20 years. The AI Voice Agent should record the requested tenure and validate it against the maximum tenure permitted by the approved policy. If 20 years exceeds the maximum limit, the agent should politely inform the customer that the requested tenure does not meet the eligibility criteria and discontinue the qualification process. The expected result is disqualification due to a tenure that is too long.
RESULT: Test 6 – Tenure Too Long
G.	Test 7 – Loan Amount Exceeds the Maximum Limit:
 In this scenario, the customer requests a loan amount of ₹90 lakh against their property, while the maximum loan amount permitted under the offer is ₹75 lakh. The AI Voice Agent should clearly explain the maximum limit and ask whether the customer is willing to proceed with a request for ₹75 lakh, subject to eligibility. If the customer agrees, the agent should continue with the remaining qualification questions. If the customer declines, the agent should record the response and end the call politely. The expected result is successful loan-amount negotiation with customer consent before proceeding.
RESULT: Test 7 – Loan Amount Exceeds the Maximum Limit:

H.	Test 8 – Joint Property Ownership:
 In this scenario, the customer informs the AI Voice Agent that the residential property is jointly owned by the customer and their wife. The agent should correctly record the ownership type as joint and should not disqualify the customer solely because of joint ownership. It should continue asking the remaining mandatory qualification questions, including whether the original property documents are available. Any additional co-owner consent or documentation requirements should be handled according to the approved policy. The expected result is continuation of the qualification process.
RESULT: Test 8 – Joint Property Ownership

I.	Test 9 – Existing Loan Against the Property: 
In this scenario, the customer informs the AI Voice Agent that they already have a loan against the same property. The agent should recognize that the customer's requirement relates to an existing Loan Against Property rather than a new loan application. It should stop the standard qualification flow, explain that the appropriate specialist can provide further assistance, and initiate the transfer to the designated specialist queue. The expected result is successful routing to the existing-loan specialist and termination of the automated qualification flow after handoff.
RESULT: Test 9 – Existing Loan Against the Property

J.	Test 10 – Customer Wants to Reduce Existing EMI:
 In this scenario, the customer explains that their primary requirement is to reduce the EMI on an existing loan rather than apply for a new Loan Against Property. The AI Voice Agent should recognize the customer's intent, classify the request as an existing-loan EMI reduction enquiry, and stop asking new-loan eligibility questions. It should politely inform the customer that the appropriate specialist will assist them and initiate the relevant transfer. The expected result is correct intent recognition and transfer to the loan servicing specialist.
RESULT: Test 10 – Customer Wants to Reduce Existing EMI


K.	Test 11 – Customer Provides Answers Out of Order:
 In this scenario, the customer provides several details in a single response, stating that the property is a residential house worth approximately ₹1.2 crore and is jointly owned with their wife. The AI Voice Agent should extract and store all three details correctly: property type as residential, market value as ₹1.2 crore, and ownership as joint. Instead of repeating the questions already answered, the agent should identify the next missing mandatory field and ask only that question, such as whether the original property documents are available. The expected result is accurate data extraction, correct internal state management, and a smooth continuation of the conversation.
RESULT:Test 11 – Customer Provides Answers Out of Order:

L.	Test 12 – Customer Is Busy:
 In this scenario, the customer informs the AI Voice Agent that they are attending a meeting and cannot speak at that moment. The agent should acknowledge the customer's situation politely and ask for a convenient callback time. If the customer requests a callback the following day at 11:00 AM, the agent should record the requested date and time and initiate the callback scheduling process if the system supports it. It should thank the customer and end the current call without continuing the eligibility questions. The expected result is appropriate handling of an unavailable customer and accurate callback recording.
M.	RESULT: Test 12 – Customer Is Busy
15. Implementation Steps
1.	Create the agent. Create a single-prompt agent in Retell AI and set the AI to speak first, greeting by time of day.
2.	Add the prompt and variables. Paste the system prompt and set the dynamic variables (company, customer, agent name, gender, language, date, day and time).
3.	Set voice and call settings. Choose a professional Indian-English female voice and apply the settings listed in section 6.
4.	Connect actions. Add the End Call function and a 12-field post-call extraction (property type, ownership, documents, loan amount, occupation, income mode, market value, tenure, call outcome and more).
5.	Test. Run batch simulation tests in Retell, then real recorded web calls for each scenario.
6.	Fix and re-test. Turn each failure into a prompt fix, for example not mentioning the offer to a wrong person and never re-asking an answered question.
7.	Save evidence. Keep the audio links and transcripts for the submission.
16. Limitations
•	The agent keeps its notebook by reading the conversation, not in a database, so it can occasionally slip.
•	Only the End Call function is connected. The specialist transfer and the expert callback are promised in words and are not yet linked to a real transfer or CRM.
•	Speech recognition errors, accents and noise can cause names, amounts and tenures to be misheard. The agent re-asks, but it cannot remove the error.
•	Product answers depend on the knowledge base. With no notes, the agent refers the customer to the senior loan expert.
•	Test evidence is incomplete: four calls have no audio because of the free usage limit, and scenario 16 has not been run.
•	The agent screens eligibility only. Credit decisions need human verification.
17. Future Scope
•	Store the qualification state in structured variables or a database, rather than relying on the model alone.
•	Integrate with a CRM so qualified leads and callback times are saved automatically.
•	Add more Indian languages and automatic language detection.
•	Add sentiment detection to hand over frustrated customers to a human agent.
•	Build a dashboard for call analytics, such as qualification rate, drop-off points and common objections.
•	Automate regression testing so every prompt change is checked against all fifteen scenarios.
18. Conclusion
This project shows that a well-structured system prompt can turn a general language model into a dependable first-level loan screening assistant. The key ideas are a clear internal state, a fixed processing order, strict rules for disqualification, and safeguards against invented information. The agent speaks naturally, remembers what the customer says, and passes only fully qualified customers to human experts. With platform-level end-call, transfer and CRM integration, this design can be extended into a production-ready solution.

