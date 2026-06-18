# Compliance Audit Benchmark (CAB)

A benchmark for measuring legal compliance in Large Language Models (LLMs) through causal, counterfactual evaluation of high-stakes decision-making scenarios.

This repo is part of the [XAI Privacy project](https://github.com/xai-privacy).

## Overview

The Compliance Audit Benchmark (CAB) tests whether LLMs make decisions that adhere to privacy and AI laws by ensuring they do not rely on legally prohibited or irrelevant attributes. Each scenario is grounded in primary law sources and regulatory guidance, featuring:

- **Binary decision tasks** with clear legal outcomes
- **Objective eligibility criteria** defining what factors _should_ influence decisions
- **Prohibited considerations** specifying what factors _must not_ influence decisions
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

# Existing Benchmarks

Each link contains information about an existing benchmark in the legal and casuality domains (mostly legal). Some benchmarks are within both, but most are either in one or the other.

Swiss Judgment Prediction (SJP) - https://arxiv.org/abs/2402.17013. An LJP dataset extended with expert-written rationales. For 108 cases, a model's predicted outcame and reasoning can be checked against a legal expert. The paper itself introduces an evaluation method called Lower Court Insertion, which intervenes on the case input by inserting the lower court's identity and measures how much that single factor shifts the model's prediction (testing how much of the model's desicion is driven by a legally irrelevant factor.)

LexGLUE - https://github.com/coastalcph/lex-glue. A legal-centered benchmark comprising of legal NLU tasks, such as case classification, contract clause classification, multi-label EU law classification. 
Sources/cases are drawn from the US, EU, and Council of Europe legal sources.

LegalBench - https://arxiv.org/abs/2308.11462 (also tracked live at https://www.vals.ai/benchmarks/legal_bench). A collection of 162 legal tasks spanning 6 different types of reasoning, measuring either
skills relevant to the practice of law or skills that legal experts find interesting.

CaseHOLD - https://arxiv.org/abs/2104.08671. A benchmark introduced as a way to show the effectiveness of domain pretraining. It contains ~53,000 multiple choice questions where the model has to pick the correct holding statement given citing context. Included in LexGLUE as a component task

CUAD (Contract Understanding Atticus Dataset) - https://github.com/TheAtticusProject/cuad. A contract review benchmark of 510 commercial legal contracts with 13,000+ expert annotations. Used to evaluate model's performance in extracting and highlighting specific clauses in contracts.

MAUD (Merger Agreement Understanding Dataset) - https://www.atticusprojectai.org/datasets/. Similar to CUAD in it's tasks but centered around Merger Agreements.

ACORD (Atticus Clause Retrieval Dataset) - https://www.atticusprojectai.org/datasets/. A contract clause retrival benchmark with 126,000+ query-clause pairs. Used to evaluate retrival of relevant contract language, given a natural language prompt.

LEXam - https://huggingface.co/datasets/LEXam-Benchmark/LEXam. A legal reasoning benchmark built from actual Swiss law exam questions, with both MCQ and open ended questions.

Legal LLM Benchmark - https://github.com/Marvin-Cypher/LLM-for-LLM. A benchmark for evaluating 12 different LLMs across 163 real world legal tasks. It specifically highlights scenarios where models would refuse to answer legal questions when phrased adversarially.

Corr2Cause — https://arxiv.org/abs/2306.05836. A 200,000+ example benchmark that tests whether models can correctly infer valid causal relationships from purely correlational statements.

CausalBench — https://huggingface.co/datasets/CCLV/CausalBench. A benchmark spanning textual, mathematical, and coding domains that tests for causal understanding from four angles: cause-to-effect, effect-to-cause, and both with intervention.

CRAB (Causal Reasoning Assessment Benchmark) - https://arxiv.org/abs/2311.04284. A benchmark of ~2,700 fine grained, contextually annotated real-world event pairs used to test causal discovery, responsibility assessment, and multi-document causal reasoning.

e-CARE (Explainable CAusal REasoning) - https://github.com/Waste-Wood/e-CARE. A human-annotated dataset with 21,000+ causal reasoning questions, each paired with a natural-language explanation of the causal relationship. Used to test both causal prediction and explanation generation.

Some existing benchmarks in the legal domain are ommited as they are too similar to ones listed here. Many benchmarks exist in either legal or causal domain, but the SJP is one of the only benchmarks that encorperates both.
























## License

[MIT License](https://github.com/xai-privacy/compliance-audit-benchmark?tab=MIT-1-ov-file#readme)
