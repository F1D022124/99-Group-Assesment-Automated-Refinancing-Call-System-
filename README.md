# Automated Mortgage Refinancing Call System

An automated mortgage refinancing qualification workflow built with n8n and AI.

## Project Overview

This project demonstrates an end-to-end workflow for qualifying mortgage customers who may be interested in refinancing (mortgage takeover).

The system retrieves customer information, checks refinancing eligibility, prepares customer data, uses an AI-based call simulation to classify the customer's response, stores the result, and notifies the sales team for follow-up.

## Workflow

The workflow follows these steps:

1. **Get Customer Data**
   - Retrieves customer records from Google Sheets.
   - Customer information includes name, phone number, bank, current interest rate, and remaining mortgage tenor.

2. **Eligibility Check**
   - An IF node separates eligible and non-eligible customers.
   - Deterministic business logic is kept separate from the AI component.

3. **Prepare Customer Data**
   - Formats the relevant customer information for the AI call stage.

4. **AI Call Simulation**
   - Simulates an outbound mortgage refinancing conversation.
   - The AI produces:
     - Call status
     - Customer response
     - Call summary
     - Recommendation
     - Next action

5. **Save Refinancing Result**
   - Stores the completed interaction and recommendation in Google Sheets.

6. **Notify Sales Team**
   - Sends a follow-up email when sales action is required.

## AI Usage

The AI component is used for the conversational and classification part of the workflow.

The AI is instructed to act as a professional mortgage refinancing call agent and identify whether a customer is interested in refinancing, while avoiding financial promises or guaranteed savings.

The AI prompt is available in:

`prompts/refinancing-call-prompt.txt`

## Real Voice API Attempt

The initial implementation attempted to integrate a real outbound voice call using Bland AI.

During testing, the available trial environment returned API/calling limitations, including HTTP 429 rate-limit restrictions and international calling restrictions.

Instead of leaving the workflow incomplete, the final demonstrable version uses an AI call simulation while keeping the same downstream workflow structure.

This allowed the customer qualification, result storage, and sales follow-up process to be tested end-to-end.

## Production Improvements

For a production implementation, I would:

- Replace the AI simulation with a real voice agent such as Bland or another supported provider.
- Add retry and rate-limit handling.
- Add call recording and call monitoring.
- Add stronger customer consent and compliance controls.
- Add scalable scheduling for approximately 100 customer calls per day.
- Add monitoring and reporting for call outcomes.
- Connect qualified leads to a CRM or sales pipeline.

## Technologies

- n8n — workflow automation
- Google Sheets — customer data and result storage
- LLM — AI call simulation and customer response classification
- Gmail — sales-team notification
- Bland AI — attempted real voice integration

## Project Files

```text
/
├── README.md
├── workflows/
│   └── automated-refinancing-workflow.json
└── prompts/
    └── refinancing-call-prompt.txt
