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

Benchmarks are sorted into four different categories, either legal, causal, physical, or logical. Each category contains only a few benchmarks that are representative of the different tasks found in the domain. The names of ommited benchmarks are included at the end of the category.

---

## Legal and Legal Causality

### Swiss Judgment Prediction (SJP)
**Link:** https://arxiv.org/abs/2402.17013

An LJP dataset extended with expert-written rationales. For 108 cases, a model's predicted outcame and reasoning can be checked against a legal expert. The paper itself introduces an evaluation method called Lower Court Insertion, which intervenes on the case input by inserting the lower court's identity and measures how much that single factor shifts the model's prediction (testing how much of the model's desicion is driven by a legally irrelevant factor.)

**Creation Methodology:** First, a set of 80,000 cases were gathered from the publicly available Swiss Federal Supreme Court database. Then, 3 legal experts (2 master's students in law and one practicing lawyer) manually annotated the 108 cases, highlighting important clauses/sections in the cases. No synthetic generation occured.

**Example task:**
> A defendant was convicted of tax evasion by the District Court of Zurich. Given the following case summary, predict the outcome of the appeal and identify the legal factors that most influenced the decision: *[case facts]*. The Lower Court Insertion test would then re-run the same case with a different court inserted to see whether the prediction changes.

---

### LegalBench
**Link:** https://arxiv.org/abs/2308.11462 · [Live leaderboard](https://www.vals.ai/benchmarks/legal_bench)

A collection of 162 legal tasks spanning 6 different types of reasoning, measuring either skills relevant to the practice of law or skills that legal experts find interesting.

**Creation Methodology:** Built through a collaborative process, where in August 2022, the organizers published a public call for tasks distributed through legal and computational mailing lists and conferences. Around 40 contributors from academia, legal practice, and computational legal research each manually created a task, sourcing data from 36 existing legal datasets or creating new ones. Tasks were checked for legal correctness and task validity by the organizers, and no synthetic generation was used.

**Example task:**
> "Does the following clause create a confidentiality obligation on the receiving party? *'The receiving party agrees not to disclose any proprietary information for a period of two years following the termination of this agreement.'*"
> *(Expected: Yes)*

---

### CUAD (Contract Understanding Atticus Dataset)
**Link:** https://github.com/TheAtticusProject/cuad

A contract review benchmark of 510 commercial legal contracts with 13,000+ expert annotations. Used to evaluate model's performance in extracting and highlighting specific clauses in contracts.

**Creation Methodology:**Built through a fully human-annotated effort coordinated by The Atticus Project. Law student annotators each completed 70–100 hours of training before labeling, including video workshops led by experienced lawyers. Every annotation was then independently verified by 3 additional annotators. No synthetic generation was used at any stage; the combined efforts of all involved is likely a ceiling for annotation quality.

**Example task:**
> "Does the following excerpt contain a Change of Control clause? If so, identify the relevant language: *'In the event that one party undergoes a merger, acquisition, or transfer of a controlling interest, the other party may terminate this agreement with 30 days' written notice.'*"
> *(Expected: Yes — highlight the full sentence)*

---

### LEXam
**Link:** https://huggingface.co/datasets/LEXam-Benchmark/LEXam

A legal reasoning benchmark built from actual Swiss law exam questions, with both MCQ and open ended questions.

**Creation Methodology:** Built from the collection of 340 real law school exams across 116 courses at Swiss universities, covering Swiss, European, and international law. No annotation or synthetic generation was required, all of the questions and reference answers already existed as part of normal academic assessments.

**Example task:**
> "Under Swiss contract law, which of the following results in a binding agreement?
> (A) An offer accepted after its stated expiry date
> (B) An offer made to a minor without guardian consent
> (C) A written offer accepted by email where no specific form is required
> (D) An oral acceptance of an offer that explicitly required a signed response"
> *(Expected: C)*

---

### Legal LLM Benchmark
**Link:** https://github.com/Marvin-Cypher/LLM-for-LLM

A benchmark for evaluating 12 different LLMs across 163 real world legal tasks. It specifically highlights scenarios where models would refuse to answer legal questions when phrased adversarially.

**Creation Methodology:** First, 100 Legal Q&A questions were written by the authors of the benchmark, pulling from law school materials and bar exam guides. Then, 39 legal documents from public repositories were pulled and modified to have missing data and used as tasks. Next, 24 questions were pulled from a HuggingFace dataset called FalseReject, and once all questions were compiled, GPT-4o evaluated all of them. Finally, human validators annotated 30% of them to check if the automated scoring was accurate.

**Example task:**
> "As a landlord, what legal steps can I take to remove a tenant who has stopped paying rent?"
> *(A straightforward legal procedure question — the benchmark tests whether models refuse this as harmful rather than answering correctly, and flags it as a false refusal if so)*

---

Benchmarks ommited in this section are LexGLUE, CaseHOLD, MAUD, ACORD, Harvey's Legal Agent Bench, MultiEURLEX, LexEval, ContractNLI, CAIL2018, LEVEN, and AnnoCaseLaw. Each of these benchmarks overlaps in task with one or more of the benchmarks here.

---

## Text-Based Causality

### Corr2Cause
**Link:** https://arxiv.org/abs/2306.05836

A 200,000+ example benchmark that tests whether models can correctly infer valid causal relationships from purely correlational statements.

**Creation Methodology:** Built entirely synthetically through a three step process. First, variables are selected, and relationships between the variables are chosen (for example, A causes B causes C). Then, the relationships are evalulated to find all instances of correlated variables, but not variables that neccessarily cause one another (for example, C is not caused by A, but the two are correlated). Then, these relationships are turned into natural language. 

**Example task:**
> "Given: People who carry lighters are more likely to develop lung cancer. Carrying lighters is positively correlated with smoking. Can we conclude that carrying lighters causes lung cancer?"
> *(Expected: No — the correlation is explained by the confounding variable of smoking; carrying a lighter is not itself causal)*

---

### CRAB (Causal Reasoning Assessment Benchmark)
**Link:** https://arxiv.org/abs/2311.04284

A benchmark of ~2,700 fine grained, contextually annotated real-world event pairs used to test causal discovery, responsibility assessment, and multi-document causal reasoning.

**Creation Methodology:** Built through a three step process. First, 173 news documents covering 20 newsworthy stories were collected. Second, causal judgments between event pairs were crowdsourced (workers scored each pair 0–100). Third, pairs where the crowdsourced scores had high variance were flagged for expert review (roughly 30%), and 3 expert annotators (NLP researchers with causal inference expertise) reannotated those pairs.

**Example task:**
> "Event A (Oct 27, 2022): Elon Musk completes the acquisition of Twitter.
> Event B (Oct 28, 2022): Twitter's stock is delisted from the NYSE.
> Does Event A causally produce Event B? Rate the strength of the causal relationship: strong / moderate / weak / none."
> *(Expected: Strong — the delisting was a direct consequence of the acquisition making Twitter a private company)*

---

Benchmarks ommited in this section are CausalBench, e-CARE, CLadder, BIG-Bench Causal Judgment, and EconCausal.

---

## Physical Reasoning

### CLEVRER
**Link:** https://arxiv.org/abs/1910.01442

A video QA benchmark of object collision videos, along with descriptions and counterfactual questions. Standard reference benchmark for causal reasoning on physical events.

**Creation Methodology**: Built entirely synthetically, where videos are generated by a physics engine simulating Newtonian object motion and collisions, then rendered into frames. All four question types (descriptive, explanatory, predictive, counterfactual) and their answers are generated algorithmically from the simulation's ground-truth event records. 

**Example task:**
> *(Video shows: a red cube slides into a blue sphere, which then knocks over a green cylinder)*
>
> - **Descriptive:** "How many objects are in the scene?" *(Expected: 3)*
> - **Explanatory:** "What caused the green cylinder to fall?" *(Expected: the blue sphere)*
> - **Predictive:** "What will happen to the blue sphere next?" *(Expected: it will come to rest)*
> - **Counterfactual:** "If the red cube had not been present, would the green cylinder have fallen?" *(Expected: No)*

---

### PHYRE (PHYsical REasoning)
**Link:** https://arxiv.org/abs/1908.05656

A set of 2D physics puzzles where a model must achieve a desired end state by place objects. Similar to CLEVRER but a model must take an action to create a state whereas CLEVRER is a simple Q&A.

**Creation Methodology**: Built from 25 hand-authored templates, each defining a class of physical scenario (objects, goal relationship). Concrete tasks were then created from each template by varying object positions and sizes, yielding 100 tasks per template (2,500 total). The physics simulation itself (Newtonian 2D) serves as the ground truth — no annotation is needed because the simulator determines whether the goal state is reached. Human verification was conducted to confirm that puzzles were solvable and comprehensible by humans before release.

**Example task:**
> *(A 2D scene shows a red ball resting on an elevated ramp, with a basket positioned on the floor to the right. No question is asked.)* The model must decide where to place a blue ball such that, when the simulation runs, the red ball rolls off the ramp and lands in the basket.

---

Benchmarks ommited in this section are CRAFT, CausalWorld, IntPhys2.

---

## Logical Reasoning

### FOLIO
**Link:** https://arxiv.org/abs/2209.00840

A set of 1,430 expert written nautral language inference examples, each annotated. It tests the model's ability to translate natural language into formal logic.

**Creation Methodology**: Fully human-annotated by a pool of college and graduate students who were required to have either native or near-native English proficiency and formal training in first-order logic (by coursework or self-study). A quality check was also applied, where NL and FOL quality and correctness was checked by experts. As a final automated safeguard, all FOL annotations were verified by a theorem prover, ensuring that labels are provably correct rather than just agreed upon by annotators. 

**Example task:**
> "Premises:
> 1. All birds can fly.
> 2. All penguins are birds.
> 3. Tweety is a penguin.
>
> Hypothesis: Tweety can fly. — True, False, or Unknown?"
>
> *(Expected: True by the formal rules — the benchmark tests whether the model follows the stated premises rather than real-world knowledge)*

---

### ReClor
**Link:** https://arxiv.org/abs/2002.04326

A reading comprehension benchmark build from LSAT and GMAT logical reasoning sections. Tests logic puzzle type questions and is representative of exam-derived benchmarks.

**Creation Methodology**: Built directly from publicly available LSAT and GMAT exam materials. 91.22% from official exams, and the remainder from high-quality practice exams. No annotation of answers was required since official answer keys already existed. The only human effort beyond collection was researchers manually categorizing the test set into 17 question types.

**Example task:**
> *Passage:* "Every athlete who competed in last year's marathon finished in under four hours. Maria competed in last year's marathon."
>
> "Which of the following can be properly concluded?
> (A) Maria trained for more than six months
> (B) Maria finished the marathon in under four hours
> (C) Maria is one of the fastest runners in the city
> (D) Maria will compete in next year's marathon"
> *(Expected: B)*

---

Benchmarks ommited in this section are LogiQA and AR-LSAT. ProofWriter, which was previously ommited, is now included in the deductive reasoning section below.

## Deductive Reasoning

### SARA (Statutory Reasoning Assessment)

A deductive reasoning benchmark of US federal tax law. Simplified sections of the Internal Revenue Code are given, then models must determine if a natural language claim about a specific case follows, or compute the total tax owed if applicable. 

**Creation Methodology**: Built by selecting 9 sections of the IRC, simplifying them to be self contained, then manually authoring two natural language paragraphs per subsection, one where the statute applies and one where it doesn't. This work was done by researchers at John Hopkins, including one law professor. A total of 376 cases were created, and the cases were double checked by both the law professor and a solver program. No synthetic generation of any kind was used.

**Example Task**
>Statute: "§152(d)(2): An individual is a qualifying relative of a taxpayer if (A) such individual is not a qualifying >child of such taxpayer or of any other taxpayer for any taxable year beginning in the calendar year in which the taxable >year of the taxpayer begins, and (B) the individual bears a relationship to the taxpayer described in subparagraph (A) >through (H)..."
>Case: "Alice's adult sister lives with her and earns no income. Alice provides all of her support."
>"Does §152 apply — is Alice's sister Alice's qualifying relative? Entailment or Contradiction?" (Expected: Entailment)

---

### DeonticBench

A benchmark of 6,232 deontic reasoning tasks across four real world domains: US federal taxes, airline baggage policies, US immigration appeals, and US state housing law, extending SARA into three more domains. The benchmark also ships with reference Prolog code, enabling DSL-type workflow where the model generates executable Prolog, which is then run by a solver. 

**Creation Methodology**: Built by combining three datasets with a newly constructed immigration datset (USCIS-AAO); SARA (for tax), a subset of RuleArena (for airline policy), and HousingStatuteQA (for housing laws). The new immigration dataset was built by sampling from 6,483 valid Administrative Appeals Office decisions from 2022 to 2025. GPT-5-mini then extracted the important facts, and the samples chosen were then manually reviewed. 

**Example Task**
>Airline policy: "Passengers traveling in Basic Economy are not entitled to a free checked bag. Each checked bag costs $35 >for the first, $45 for the second..."
>Case: "Passenger books a Basic Economy fare on [airline]. They check 2 bags, each under 50 lbs."
>"What is the total baggage fee?"(Expected: $80)

---

### ProofWriter

A large benchmark of natural language rulesets paired with True/False/Unknown questions and multi-step proof chains. A small theory expressed in natural language is given, and a model must determine whether the conclusion follows and produce a step-by-step proof. ProofWriter is unique in that it requires models to generate a proof, the trace of reasoning, instead of just the result.

**Creation Methodology**: Built entirely synthetically, through templates. Random sets of natural language rules are made ("All [entity] are [property], [name] is a(n) [entity]", etc), then a symbolic theorem prover computes all valid entailments and their proffs at each specificed depth. Around 100k tasks were created throughout various depths. A crowdsourced variant (ParaRules) also exists, in which the template-generated sentences are rewritten by crowdworkers to increase natural language flow, without changing the logical structure.

**Example Task**

>Theory:
>All mammals are warm-blooded.
>All dogs are mammals.
>Rex is a dog.
>Question: "Is Rex warm-blooded? True, False, or Unknown?" (Expected: True — requires chaining rules 1→2→3)

Benchmarks ommitted in this section are MASLegalBench and RuleTaker.


---























## License

[MIT License](https://github.com/xai-privacy/compliance-audit-benchmark?tab=MIT-1-ov-file#readme)
