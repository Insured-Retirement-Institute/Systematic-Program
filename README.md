# IRI Systematic Program API
### Systematic Withdrawal & Systematic RMD — Setup and Update

## Overview

The **IRI Systematic Program API** defines the standards for establishing and updating **Systematic Withdrawal** and **Systematic Required Minimum Distribution (RMD)** programs on in‑force annuity policies.  
This API supports the industry’s shift from legacy XML/SOAP interfaces to modern RESTful APIs that leverage JSON payloads and OAuth‑based authentication under IRI’s Digital‑First Architecture (DFA) initiative.

This repository provides a unified view of both **Setup** and **Update** workflows while maintaining consistency, interoperability, and seamless integration across carriers, distributors, and solution providers.

---

## Business Case

### Problem Statement
- Legacy XML/SOAP systems are approaching end‑of‑life and lack required modern security features.  
- Firms need real‑time, standards‑based digital servicing for establishing and modifying systematic programs.  
- Manual updates and paper‑based processes increase operational risk, delays, and rework.

### Objectives
- Modernize systematic withdrawal and RMD workflows using REST/JSON. 
- Transition all systematic withdrawal and RMD **setup** and **update** processing to RESTful API architecture. 
- Provide consistent structures for setup and update transactions across the industry.  
- Reduce processing complexity and integration overhead between carriers and partners.  
- Align with IRI Digital‑First goals for secure, scalable, interoperable data exchanges.
- Reduce operational risk and rework when program parameters change (amount, frequency, payee, funds, etc.).

### Key Features
- Unified schema patterns for Setup and Update  
- OpenAPI 3.1.x specifications with examples  
- Standardized error handling  
- Modular schema components  
- Industry‑wide interoperability through consistent Data Dictionary alignment  

---

## Supported Transactions

The Systematic Program specification includes **four** transaction types:

### 1. Systematic Withdrawal Program Setup
Creates a new systematic withdrawal arrangement for an active policy.  
**Typical scenarios:**  
- Scheduled income withdrawals  
- Periodic disbursements aligned with client needs  
- Withdrawal allocation across multiple funds or segments
- Coordinated disbursements across multiple funds and parties.  

### 2. Systematic Withdrawal Program Update
Modifies an existing systematic withdrawal arrangement identified by `arrangementId`.  
**Typical changes:**  
- Updating amount or percentage  
- Changing frequency or start/end dates  
- Adjusting payee, bank, or tax withholding instructions  
- Modifying fund allocation details
- Updating payee details, bank information, or tax withholding instructions.
- Modifying fund- or segment-level distribution allocations.  

---

### 3. Systematic RMD Program Setup
Establishes recurring Systematic RMD instructions to help policyholders meet regulatory RMD obligations. 
**Typical scenarios:**  
- Automating annual RMD distributions  
- Applying selected RMD calculation methods  
- Routing distributions with integrated withholding rules  

### 4. Systematic RMD Program Update
Updates an existing systematic RMD program.  
**Typical changes:**  
- Adjusting amount or requested percentage  
- Updating distribution scheduling  
- Revising payee or withholding details  
- Updating RMD‑specific fields (calculation method, prior year values)  

---

## Personas and User Stories

### Policy Administrator
- Ensures accurate setup and maintenance of systematic programs  
- Requires clear rules for required fields, frequency, amounts, and payee information  

### System Integrator
- Implements the unified setup/update API pattern across carriers  
- Needs consistent JSON schemas and well‑documented attributes  

### Financial Advisor
- Helps clients design withdrawal strategies and maintain RMD compliance  
- Needs confidence that carrier systems process transactions accurately and timely  

---

## High‑Level Schema Concepts

Shared concepts across Setup and Update APIs:

- **Root Attributes**  
  Effective date, firm identifiers, action indicator, CUSIP, allocation options  

- **Systematic Program**  
  - paymentForm (e.g., ACH, DTCC)  
  - arrangementType (WITHDRAWAL or REQUIREDMINIMUMDISTRIBUTION)  
  - amountType (AMOUNT, PERCENTAGE, MAX, etc.)  
  - net/gross indicator  
  - schedule: frequency, start/end dates, next transaction date  

- **Payee / Beneficiary**  
  Individual or entity identity, banking information, tax withholding instructions  

- **Parties**  
  Policy parties and role types (owner, annuitant, beneficiary)  

- **Producer**  
  Identifiers for writing or servicing producers  

- **Fund Distributions**  
  Optional fund‑level or segment‑level allocation instructions  

- **RMD‑Specific Data**  
  Tax year, RMD age, calculation method, spouse date of birth (optional), prior year‑end value  

These concepts ensure a unified approach to defining **new arrangements** (Setup) and **changes to existing ones** (Update).

---

## Response Model Overview

### Success Responses
- **Setup:** Returns **HTTP 201 Created**  
- **Update:** Returns **HTTP 202 Accepted**  
- `Location` header points to the request resource:  
/v1/policies/{policyNumber}/withdrawals/requests/{requestId}
- Body includes a request status object (`requestId`, `status`, `effectiveDate`, etc.)

### Request Status Retrieval
A `GET` endpoint returns lifecycle status with **HTTP 200 Success**.

---

## Standard Error Schema

Every error response—regardless of transaction type—includes:

- An HTTP status code in the **400–599** range.
- A structured and validated **error code**.
- A **timestamp** of when the error was generated.
- A developer‑focused **technical message** (`message`).
- A safe, user‑friendly **userMessage**.
- A **correlationId** for cross‑system tracing.
- Optional **field‑level** or **rule‑level** error collections.

### Key Fields

| Field                  | Description                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------|
| **httpStatus**         | Numeric HTTP status code (400–599) representing the type and severity of the failure.          |
| **code**               | Structured identifier in the enforced format: `domain.category.subcategory`.                    |
| **message**            | Technical diagnostic detail for developers, logs, or support teams.                            |
| **userMessage**        | End‑user‑friendly explanation, safe to show in portals or consumer‑facing applications.        |
| **correlationId**      | Carries forward the inbound request’s correlation ID header to enable end‑to‑end traceability. |
| **validationErrors**   | *(optional)* Array describing field‑level validation issues.                                    |
| **businessErrors**     | *(optional)* Array describing domain/business rule violations; each entry has its own code and message. |

### Purpose & Benefits

This standardized error structure ensures:

- A **predictable experience** across all APIs (synchronous and asynchronous).
- Clear differentiation between **developer diagnostics** and **user‑safe messages**.
- Enhanced **traceability** for carriers, distributors, and integrators.
- Support for granular **validation feedback** and complex business rule logic.
- Easier **monitoring, logging, and cross‑system troubleshooting**.


## OpenAPI Specs

Unified Swagger/OpenAPI documentation for all systematic program endpoints is available in the `openapi-specs/` folder.

---

## Change Submissions and Reporting Issues

- Issues and bugs can be reported directly within the **Issues** tab of this repository.
- **Security issues** should be reported directly to Katherine Dease at **kdease@irionline.org**.
- Change requests should follow the **standards governance workflow** outlined on the main page.

---

## Versioning

- Follow semantic versioning for specification updates.
- Document changes in commit messages and changelogs to support integrator adoption.
- Clearly label draft vs active versions in alignment with IRI DFA governance.

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
