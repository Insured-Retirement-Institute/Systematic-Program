# Systematic Program Update Attribute Specification
This repository contains the schema definitions for Systematic Withdrawal Update and Systematic RMD (Required Minimum Distribution) Update transactions. These specifications support the modernization of In-Force Transactions (IFT) by transitioning from legacy XML/SOAP messaging to RESTful APIs. This aligns with the industry’s Digital First goals and prepares stakeholders for scalable, secure, and interoperable retirement policy management.

## Get started
To begin using this specification:

1. Clone the repository:
- Shellgit clone https://github.com/Insured-Retirement-Institute/systematicprogramupdate.git

2. Navigate to the project directory:
- Shellcd systematicprogramupdateShow more lines

3. Review the schema documentation:
- Understand the structure and required fields for both Systematic Withdrawal Update and Systematic RMD Update.
- Integrate the schema into your transaction processing systems.


4. Validate your data:

- Ensure all required fields are populated.
- Follow the data types and length constraints.

## Business Case
The financial services industry is rapidly evolving toward seamless, real-time, and lightweight digital experiences. Legacy XML/SOAP technology is approaching end-of-life and lacks the scalability, flexibility, and security required by today’s digital ecosystems. RESTful APIs, using JSON payloads and OAuth 2.0 authentication, are now the de facto standard.

### Problem Statement:
- End-of-Life Technology: SOAP is no longer supported; REST/JSON is prioritized by vendors and cloud providers.
- Security: Modern protocols (OAuth 2.0) are required.
- Scalability & Flexibility: REST APIs are lightweight, easier to parse, and integrate with microservices.
- Industry Alignment: Supports IRI Digital First goals for secure, interoperable technology.

### Objectives & Key Results:
- Transition all IFT processing from XML to RESTful API architecture.
- Reduce transaction payload size and processing time.
- Improve integration velocity across firms and carriers.
- Strengthen transaction security.
- Ensure long-term vendor and community support.

## User Stories, personna
- As a Policy Administrator, I want to validate all required fields before submitting an update so that I can avoid processing delays.
- As a System Integrator, I want to map the update schema to our internal data model so that we can automate the transaction flow.
- As a Financial Advisor, I want to confirm the payee’s bank and address details so that I can ensure accurate disbursement.

### 1. Policy Administrator
- Goals: Ensure accurate and timely processing of systematic withdrawal and RMD updates.
- Needs: Clear schema definitions, validation rules, and integration guidance.
- Pain Points: Manual data entry errors, inconsistent formats, lack of traceability.

### 2. System Integrator
- Goals: Implement update schema into backend systems and APIs.
- Needs: JSON schema formats, sample payloads, field-level documentation.
- Pain Points: Ambiguous field definitions, missing required attributes.

### 3. Financial Advisor

- Goals: Guide clients through systematic withdrawal and RMD update processes.
- Needs: Clear understanding of payment forms, tax implications, and beneficiary details.
- Pain Points: Confusing terminology, paper process.


## Schema Overview
The schema for systematic program update transactions is defined in the data model and includes the following key components for both Systematic Withdrawal Update and Systematic RMD Update:

### Root Attributes
- correlationId: Unique transaction ID (string, required)
- policyNumber: Unique policy number (string, required)
- arrangementId: Unique ID for the systematic program within the policy (string, required)
- effectiveDate: Transaction date (string, required, format: yyyy-mm-dd)
- actionIndicator: Transaction action (enum: N, O, C)
- associatedFirmId: Firm identifier (string, required)
- nsccParticipantId: NSCC participant identifier (string, required)
- cusip: Security identifier (string, optional)

### Systematic Program
- paymentForm: Type of payment (enum: DTCC, CREDITCARD, ACH, CHECK, WIRE, EXCHANGE)
- arrangementType: WITHDRAWAL or REQUIREDMINIMUMDISTRIBUTION
- amountType: AMOUNT, PERCENTAGE, MAX, FREEWITHDRAWALAMOUNT, WITHDRAWALUNTILBASIS, EARNINGSONLY, PRORATA
- netGrossIndicator: Net or Gross (enum: N, G)
- requestedAmount/requestedPercentage: Amount or percentage, as applicable
- frequency: Transaction frequency (enum: DAILY, EVERYTWOWEEKS, MONTHLY, SEMIANNUAL, QUARTERLY, ANNUAL, SINGLEPAYMENT)
- startDate, endDate, previousTransactionDate, nextTransactionDate: Date fields

### For Systematic RMD Update Only:

- rmdInfo: RMD-specific details (tax year, age at distribution, spouse DOB, requested amount, calculation method, prior year end value)

### Payee/Beneficiary Details

- partyId, firstName, middleName, lastName, organizationName
- bank: Bank details (account number, routing number, etc.)
- taxWithholdingInstructions: Array of tax withholding instructions

### Parties

- partyRole, partyId, firstName, middleName, lastName, organizationName
- paymentForm, allocationPercentage
- bank, address: Financial and contact details

### Producer

- producerNumber, npn, crdNumber

### Fund Allocation & Distributions

- allocationOption: PRORATA, DOLLAR, SPECIFYPERCENTAGE, SPECIFIEDFUNDS, etc.
- fundDistributions: Array of fund distribution objects

## OpenAPI Specs
Unified Swagger documentation for all endpoints is available in the `openapi-specs/` folder.

---

## Change Submissions and Reporting Issues

- Issues and bugs can be reported directly within the **Issues** tab of this repository.
- **Security issues** should be reported directly to Katherine Dease at **kdease@irionline.org**.
- Change requests should follow the **standards governance workflow** outlined on the main page.

---

## Code of Conduct

Please review and adhere to the **Code of Conduct** and **Style Guide** provided in the repository to ensure consistency and professionalism.

---

## How to Contribute

- Fork the repo and submit pull requests.
- Report issues via the **Issues** tab.
- Join working groups: **hpikus@irionline.org**.

---

## Business Owners

- **Carrier Business Owner:** digitalfirst@brighthousefinancial.com  
- **Distributor Business Owner:** [contact]  
- **Solution Provider Business Owner:** [contact]  
