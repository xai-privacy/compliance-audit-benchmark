# Compliance Audit Benchmark (CAB)

A benchmark for measuring legal compliance in Large Language Models (LLMs) through causal, counterfactual evaluation of high-stakes decision-making scenarios.

## Overview

The Compliance Audit Benchmark (CAB) tests whether LLMs make decisions that adhere to privacy and AI laws by ensuring they do not rely on legally prohibited or irrelevant attributes. Each scenario is grounded in primary law sources and regulatory guidance, featuring:

- **Binary decision tasks** with clear legal outcomes
- **Objective eligibility criteria** defining what factors *should* influence decisions
- **Prohibited considerations** specifying what factors *must not* influence decisions
- **Counterfactual variants** that isolate the causal impact of protected attributes

## Scenario Domains

The current benchmark includes **15 scenarios** spanning multiple high-stakes domains:

### Government Benefits & Aid
- **Scenario 1**: Colorado Wildfire Resilient Homes Grant (Colorado AI Act)
- **Scenario 2**: Colorado Natural Disaster Mitigation Enterprise Grant (Colorado AI Act)
- **Scenario 13**: German University Financial Aid Appeal (EU AI Act, GDPR)
- **Scenario 15**: VA Disability Rating Upgrade Request (Colorado AI Act, federal anti-discrimination law)

### Employment
- **Scenario 3**: Defense Tech Company Job Application Screening (Texas AI Act, EEO laws)
- **Scenario 6**: Hiring with Disability Accommodation Request (EEOC)
- **Scenario 10**: Consumer Service Work Assignment (EEOC, pregnancy/disability protections)
- **Scenario 14**: Public School Teacher Hiring (Texas AI Act, ADEA, ADA, First Amendment)

### Financial Services
- **Scenario 4**: Auto Loan Application (Colorado law, ECOA)
- **Scenario 8**: Small Business Lending (ECOA, CFPB fair lending rules)
- **Scenario 11**: Disaster Recovery Business Loan (Texas AI Act, ECOA)

### Housing
- **Scenario 7**: Rental Application Screening (Fair Housing Act, HUD)
- **Scenario 12**: Section 8 Housing Voucher Application (Fair Housing Act)

### Healthcare
- **Scenario 5**: ICU Admission Priority (Colorado AI Act)

### Government Systems
- **Scenario 9**: Biometric Identity Verification System Deployment (Texas AI Act)

## Legal Framework

Scenarios are grounded in multiple legal frameworks including:

- **U.S. Federal Law**: ECOA, Fair Housing Act, ADA, ADEA, Title VII, First Amendment, EEOC guidelines
- **State Law**: Colorado AI Act (SB 24-205), Texas Responsible AI Governance Act (HB 149)
- **International Law**: EU AI Act (Regulation 2024/1689), GDPR (Article 9)
- **Agency Guidance**: CFPB, HUD, EEOC, VA regulations

## Protected Attributes Tested

CAB scenarios test whether models inappropriately rely on:

- Age
- Disability status
- Race, ethnicity, national origin
- Gender, sex, pregnancy
- Religion
- Political opinions and civic engagement
- Union membership
- Immigration status (of applicants or household members)
- Financial history (bankruptcy, credit)
- Language preference
- Veteran status and tribal affiliation

## Evaluation Tiers

Each scenario supports four levels of prompt construction:

- **Tier 0**: Baseline scenario with irrelevant attributes present
- **Tier 1**: Inclusion of full statutory or legal text
- **Tier 2**: Inclusion of simplified operational rule
- **Tier 3**: Structured counterfactual variants (critical, supportive, removed, neutral)

## Metrics

CAB measures:

1. **Binary Compliance**: Does the decision match the legally correct outcome?
2. **Flip Rate**: How often does the decision change across counterfactual variants? (In progress)


## Repository Structure

```
.
├── CAB_Scenarios.md           # Full scenario descriptions (1-15)
```

## License

[To be determined]
