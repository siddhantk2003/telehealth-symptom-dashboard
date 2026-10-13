# Telehealth Symptom Text Mining Dashboard

## 1. Project Overview

Build a research-oriented web application that analyzes patient-doctor conversations using natural language processing (NLP) to identify, categorize, and visualize patient-reported symptoms.

**Project title:** Telehealth Symptom Text Mining Dashboard

**Project description:** Automated Text Mining Dashboard for Categorizing Patient Symptoms from Telehealth Chat Logs.

### Primary Objectives

- Process conversational healthcare text into structured representations.
- Develop and compare two distinct NLP approaches for symptom categorization.
- Visualize model performance, symptom distributions, and prediction results.
- Investigate classification errors and disagreements between models.
- Produce reproducible experiments and scientifically defensible findings.
- Build an interactive, accessible dashboard for exploring the results.

### Research Question

How do two different NLP approaches compare in their ability to identify and categorize patient-reported symptoms from patient-doctor conversations?

The research question and experimental design may be refined after dataset inspection.

### Scope and Limitations

This project is intended for academic research and educational demonstration.

It is not a diagnostic or treatment recommendation system. Model predictions must not be presented as confirmed diagnoses or used to make autonomous clinical decisions.

Prioritize research validity, reproducibility, interpretability, and maintainable code over unnecessary complexity.

---

## 2. Developer Context and Collaboration

The developer is learning Claude Code while building this project.

Act as both a software engineering collaborator and a technical mentor.

- Explain important architectural and research decisions in beginner-friendly language.
- Explain trade-offs rather than presenting recommendations without reasoning.
- Prefer small, verifiable implementation steps.
- Before substantial changes, describe the proposed approach and acceptance criteria.
- For small, well-defined tasks, avoid excessive planning and proceed efficiently.
- When debugging, explain the root cause and why the fix works.
- Distinguish verified facts, assumptions, recommendations, and unresolved decisions.
- Ask for clarification when an unresolved decision materially affects correctness, scope, or architecture.
- Do not implement unrelated features or generate the entire application in one step.
- Help the developer understand the code well enough to maintain and extend it independently.

---

## 3. Technology Stack

### Confirmed Decisions

- Frontend: React.
- Backend language: Python.
- NLP methodology: Hybrid rule-based and machine-learning approach.
- Research requirement: Implement and compare two distinct NLP algorithms.
- Dataset: Public patient-doctor conversation dataset selected by the developer.
- Project orientation: Research and evaluation.

### Provisional Technical Choices

These are recommendations pending repository and dataset inspection.

- Frontend tooling: Vite with React and TypeScript.
- Backend API: FastAPI.
- API communication: REST with JSON.
- Data processing: pandas and suitable Python NLP libraries.
- Traditional ML baseline: scikit-learn.
- Frontend testing: Vitest and React Testing Library.
- Backend testing: pytest.
- Visualization: A suitable React charting library.
- Storage: Dataset files and derived research artifacts initially, unless additional requirements justify a database.

Inspect existing project files and dependencies before selecting or introducing tools. Explain significant alternatives and trade-offs before making major architectural changes.

---

## 4. Dataset and Data Management

### Selected Dataset

**Name:** Patient Doctor Conversation Dataset — 50K Samples.

**Source:** https://www.kaggle.com/datasets/sureshbeekhani/patient-doctor-conversation-dataset-50k-samples

**Status:** Selected by the developer; contents, annotations, license, provenance, and research suitability remain to be verified.

Do not assume that the dataset contains 50,000 unique conversations, verified symptom labels, a particular schema, or sufficient information for supervised classification.

### Required Dataset Inspection

Before implementing the NLP pipeline:

1. Inspect the available files, formats, columns, data types, and row counts.
2. Determine whether records represent conversations, messages, or individual text segments.
3. Identify patient messages, doctor responses, and other relevant fields.
4. Determine whether symptom annotations or ground-truth labels exist.
5. Examine missing values, duplicates, class distributions, and text quality.
6. Investigate repeated or related records that could cause data leakage.
7. Review dataset documentation, licensing, provenance, and permitted uses.
8. Document limitations affecting research validity.

### Data Handling

- Preserve the original dataset and process separate working copies.
- Keep raw datasets and sensitive derived artifacts out of version control.
- Use appropriate `.gitignore` rules.
- Avoid printing entire conversations or exposing sensitive text in logs.
- Validate input files and handle malformed records explicitly.
- Document preprocessing choices and dataset versions.
- Never invent ground-truth labels.
- Distinguish provided annotations, manually assigned labels, rule-generated labels, and model predictions.
- Do not assume that removing names alone makes healthcare text anonymous.

Use only data whose licensing and privacy conditions permit the intended research.

---

## 5. Research Task and Symptom Taxonomy

The prediction target must be established after inspecting the dataset.

Determine:

- What constitutes one prediction: a conversation, a patient message, or a text segment.
- Whether the dataset contains usable symptom labels.
- Whether the task is single-label or multi-label classification.
- Which symptom categories are included and how they are defined.
- How ambiguous, missing, and unclassifiable examples are handled.

If ground-truth labels are unavailable, propose a defensible annotation strategy before claiming classification performance. Do not treat automatically generated labels as independently verified ground truth.

The symptom taxonomy and labeling protocol remain provisional until justified by the data and research objectives.

---

## 6. Comparative NLP Experiment

### Research Requirement

Implement and compare two distinct NLP algorithms under a consistent experimental protocol.

The comparison must be based on actual evaluation results, not assumed performance or illustrative values.

### Candidate Algorithm A: TF-IDF + Logistic Regression

- Convert text into numerical features using TF-IDF.
- Train a Logistic Regression classifier on the resulting features.
- Use this as the traditional machine-learning baseline.
- Evaluate suitable preprocessing and hyperparameter choices using training and validation data only.
- Document the configuration and limitations.

### Candidate Algorithm B: DistilBERT

- Investigate a suitable pretrained DistilBERT model for contextual text classification.
- Fine-tune it if the dataset, annotation quality, computational resources, and project timeline support the approach.
- Record the model configuration, training procedure, and computational requirements.
- Compare its results with the traditional baseline using the same evaluation protocol.

These are candidate algorithms, not immutable requirements. Validate their suitability after inspecting the dataset. If either is inappropriate, explain the alternatives and obtain agreement before replacing it.

### Role of the Rule-Based Component

The overall NLP pipeline must follow a hybrid approach.

- Develop documented symptom dictionaries, phrase patterns, or other justified rules where appropriate.
- Handle negation and contextual ambiguity where feasible.
- Test rules against representative positive, negative, and ambiguous examples.
- Define explicitly how rule-based and ML outputs interact.
- Avoid treating every symptom-related keyword as proof that a patient currently experiences that symptom.

The two required comparative algorithms are TF-IDF + Logistic Regression and DistilBERT, subject to feasibility validation. The rule-based component may support preprocessing, extraction, interpretation, or a separately evaluated baseline.

Do not combine the rule-based component with one model in a way that makes the two-algorithm comparison unfair or uninterpretable. Document whether the comparison evaluates standalone classifiers or complete hybrid pipelines.

### Experimental Fairness

- Use the same prediction target and compatible data splits for both approaches.
- Prevent test-set information from influencing training, preprocessing decisions, or model selection.
- Fit learned preprocessing steps using training data only.
- Prevent leakage between related conversations or patients when grouping information is available.
- Use stratification or grouped splitting as appropriate.
- Record random seeds, model configurations, and software versions.
- Use the same test examples and metric definitions for both approaches.
- Do not claim that one algorithm is superior unless measured results support the conclusion.

---

## 7. Evaluation Metrics and Research Integrity

Choose metrics based on the classification task and class distribution.

### Core Metrics

- Accuracy, when appropriate.
- Precision.
- Recall.
- F1 score.
- Macro-F1 and weighted-F1 where appropriate.
- Per-class precision, recall, and F1.
- Confusion matrix for single-label classification.
- Suitable multilabel metrics when records can have multiple labels.

Accuracy alone is insufficient when class imbalance or uneven performance across categories matters.

Explain metric definitions, averaging strategies, and limitations. Use appropriate baselines and report class distributions.

### Additional Comparisons

Where feasible, measure:

- Training duration.
- Inference latency.
- Model size or computational requirements.
- Prediction disagreement rates.
- Performance differences across symptom categories.

Measure these quantities using documented procedures rather than estimates presented as observed results.

### Research Integrity

- Never fabricate metrics, labels, citations, dataset properties, or experimental outcomes.
- Clearly distinguish actual results from illustrative examples.
- Do not claim statistical significance without appropriate analysis.
- Compare algorithms using consistent data splits and evaluation procedures.
- Document important failures, limitations, and unsuccessful experiments.
- Ensure that visualizations reflect actual computed results.
- Do not infer clinical effectiveness from classification benchmark performance.

---

## 8. Dashboard Requirements

Build an interactive research dashboard that presents actual outputs from the evaluation pipeline.

### A. Research Overview

Display:

- Dataset summary and provenance.
- Number of eligible records.
- Symptom category distribution.
- Selected algorithms and their configurations.
- Evaluation methodology and important limitations.

### B. Model Comparison

Provide side-by-side results for both algorithms.

Include applicable metrics such as accuracy, precision, recall, F1, macro-F1, and weighted-F1.

Clearly label metric definitions and averaging strategies. Use charts that make differences between algorithms easy to interpret without exaggerating small differences.

### C. Confusion Matrices and Per-Class Results

- Display confusion matrices for single-label classification.
- Display appropriate per-class or multilabel evaluation results.
- Highlight categories where performance differs substantially.
- Explain the meaning of the visualizations.

### D. Prediction Explorer

Where permitted by the dataset and research design, display:

- A text example or privacy-conscious representation.
- The ground-truth category, when available.
- Predictions from both algorithms.
- Correctness indicators.
- Confidence or score information when meaningfully supported.

Provide filters for exploring model agreement, disagreement, and category-specific errors.

Do not expose unnecessary identifying information or raw sensitive text.

### E. Computational Comparison

Where reliably measured, compare training time, inference latency, and relevant resource requirements.

Document the measurement setup so the comparison is interpretable.

### F. Research Methodology and Limitations

Explain the dataset, labeling approach, preprocessing, evaluation splits, metrics, model configurations, and important limitations.

All dashboard values must originate from actual dataset summaries, predictions, or evaluation artifacts. Do not display fabricated results or placeholder metrics as real findings.

---

## 9. Architecture and API

Keep the frontend, backend, data processing, and research evaluation components separate.

### Frontend

Responsible for:

- Dashboard layout and visualizations.
- Filters and user interactions.
- Model comparison and prediction exploration.
- Loading, error, and empty states.
- Displaying results from documented backend interfaces.

### Backend

Responsible for:

- Input validation.
- Dataset summaries and analysis results.
- Invoking the appropriate NLP components.
- Providing structured predictions and evaluation outputs.
- Returning consistent response schemas and safe error messages.

### NLP and Evaluation

Keep preprocessing, rule-based logic, model training, inference, and evaluation independently testable.

Separate offline training and experiment execution from ordinary dashboard requests wherever appropriate. Avoid training expensive models every time a dashboard page loads.

### API Principles

- Use FastAPI provisionally unless evidence justifies an alternative.
- Validate request and response structures.
- Use consistent JSON schemas and suitable HTTP status codes.
- Do not expose stack traces, filesystem details, or raw conversations through errors.
- Document endpoints when their contracts are established.
- Avoid unnecessary microservices, databases, and deployment infrastructure.

---

## 10. Privacy and Safety

- Prefer appropriately licensed public data and synthetic examples for testing.
- Never commit credentials, API keys, or sensitive data.
- Do not log raw patient conversations.
- Do not send healthcare text to external services without reviewing authorization, licensing, and privacy implications.
- Avoid unnecessary collection or display of identifiers.
- Use safe defaults for data access and file uploads.
- Do not expose private text through debugging endpoints.
- Do not generate diagnoses, prescriptions, or treatment recommendations.
- Present classifications as research outputs rather than clinical facts.
- Document relevant model and dataset limitations.

---

## 11. Coding Standards and Testing

### Coding Standards

- Follow existing repository conventions.
- Use descriptive names and focused functions.
- Separate presentation, API, NLP, and evaluation logic.
- Validate external inputs.
- Handle errors explicitly.
- Avoid duplicated logic and unnecessary abstractions.
- Add comments for non-obvious reasoning.
- Keep dependencies minimal and justified.
- Do not suppress errors or warnings without understanding their cause.

### Testing

- Add tests for new functionality and bug fixes.
- Test empty text, missing fields, malformed records, and unexpected inputs.
- Test symptom rules against positive, negative, and ambiguous examples.
- Test label mappings and hybrid integration behavior.
- Test API validation and error handling.
- Test frontend loading, error, empty, and successful states.
- Verify metric calculations with known examples.
- Use synthetic fixtures rather than real sensitive conversations for routine tests.

### Verification

After relevant changes:

1. Run appropriate tests.
2. Run applicable linting, formatting, and type checks.
3. Investigate failures rather than hiding them.
4. Report the checks actually executed and their results.
5. Identify checks that could not be run.
6. Never claim success without verification.

---

## 12. Git and Dependency Management

- Inspect Git status before editing, reverting, or committing files.
- Preserve unrelated user changes.
- Inspect existing files before overwriting them.
- Do not perform destructive Git operations without explicit authorization.
- Never commit secrets, raw datasets, sensitive text, or inappropriate generated artifacts.
- Review dependency manifests before installing packages.
- Prefer existing dependencies when they meet requirements.
- Explain significant dependency additions and their trade-offs.
- Avoid unrelated formatting changes.

---

## 13. Development Workflow

For substantial tasks:

1. Inspect relevant code, data, and documentation.
2. Identify requirements, assumptions, and dependencies.
3. Explain the proposed approach and important trade-offs.
4. Define a small implementation step and acceptance criteria.
5. Implement only the agreed scope.
6. Run relevant checks.
7. Review changes for correctness, privacy, and maintainability.
8. Summarize what changed, what was verified, and what remains unresolved.

For small, well-defined tasks, avoid unnecessary planning overhead.

When debugging, identify the root cause and explain why the fix works.

Do not rewrite unrelated modules or expand project scope without agreement.

---

## 14. Documentation

Maintain documentation that supports development and reproducibility.

- `README.md`: Project purpose, prerequisites, setup, usage, and development commands.
- `CLAUDE.md`: Persistent project instructions and important engineering constraints.
- `docs/`: Detailed architecture, dataset notes, research methodology, and experimental decisions where appropriate.

Document actual behavior and confirmed decisions. Avoid duplicating lengthy documentation across files.

---

## 15. Development Commands

Populate this section after the project is initialized and commands have been verified.

- Frontend installation:
- Frontend development:
- Frontend tests:
- Frontend lint and type checks:
- Backend environment setup:
- Backend development:
- Backend tests:
- Backend lint and type checks:
- Model training:
- Model evaluation:

Inspect manifests and configuration before recording commands. Do not invent scripts or assume dependencies are installed.

---

## 16. Provisional Decisions and Change Management

The following decisions remain unresolved until supported by dataset inspection, repository evidence, or research requirements:

- Dataset schema, unit of analysis, and annotation quality.
- Dataset license and suitability for the intended research.
- Symptom taxonomy and labeling protocol.
- Single-label versus multilabel classification.
- Final NLP libraries and model configurations.
- Rule-based and ML integration strategy.
- Final frontend charting library.
- Storage, deployment, and computational resource requirements.

When a decision is resolved:

1. Explain the evidence, alternatives, and trade-offs.
2. Recommend a justified choice.
3. Obtain agreement for material changes to scope or architecture.
4. Update this file and relevant documentation when the decision establishes a lasting project rule.

Do not treat unverified assumptions as confirmed requirements.

---

## 17. Definition of Done

A task is complete when its relevant acceptance criteria are satisfied.

Depending on the task:

- Requested behavior is implemented within the agreed scope.
- Relevant tests and checks have been run.
- Errors and limitations are disclosed.
- Documentation is updated where necessary.
- No unintended changes or sensitive files have been introduced.
- Research claims are supported by actual results.
- The developer understands the important implementation decisions.

The overall research comparison is complete when both algorithms have been implemented, evaluated fairly on appropriate common test data, compared using verified metrics, and presented through the dashboard with documented methodology and limitations.