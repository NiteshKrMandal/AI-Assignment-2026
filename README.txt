AI ASSIGNMENT 2026
A Modular Classical Reasoning Agent



PROJECT OVERVIEW
----------------
This project implements a modular classical reasoning agent for three
reasoning benchmark families:

1. RuleTaker: natural-language facts and rules, handled using forward
   and backward chaining.
2. CounterBench: causal/counterfactual reasoning, handled by separate
   CounterBench Alpha PBCI V1.0 and Backdoor V2.1 components.
3. FOLIO: first-order logic entailment, handled by a formula parser,
   abstract syntax tree (AST), and Z3 solver.

The system uses task-specific parsers and reasoning procedures behind
a common prediction interface. It is not a single trained neural model.

NOTE ON THE CURRENT SUBMISSION.CSV
----------------------------------
At the current stage, submission.csv contains predictions generated
from the available public labelled evaluation splits. It is a temporary
public-data fallback because the private test data has not yet been
tested.



PUBLIC DATA EVALUATION 

The latest reported public summary contains 3,029 prediction rows:
    Correct predictions: 2,766
    Descriptive combined accuracy: 91.32%

This aggregate combines different datasets and split types, including
training, test, OOD-test, and validation. It is descriptive only and
must not be interpreted as a single benchmark score.
Individual results:
    RuleTaker train:       983 / 1,000  (98.30%)
    RuleTaker test:        244 /   250  (97.60%)
    RuleTaker OOD test:    373 /   375  (99.47%)
    CounterBench Alpha PBCI V1.0: 900 / 1,000 (90.00%)
    CounterBench Backdoor V2.1:  180 /   200 (90.00%)
    FOLIO train:           814 / 1,001  (81.32%)
    FOLIO validation:      172 /   203  (84.73%)

FOLIO PARSER COVERAGE
---------------------
Training:
    Parsed examples: 896 / 1,001
    Parser coverage: 89.51%
    Parser failures: 105
    Parser-clean accuracy: 83.15%

Validation:
    Parsed examples: 192 / 203
    Parser coverage: 94.58%
    Parser failures: 11
    Parser-clean accuracy: 85.94%

Parser-clean accuracy is calculated only on examples that the parser/
translation pipeline successfully processed. It must always be reported
together with parser coverage and must not replace the all-example
accuracy.

ENVIRONMENT AND EXECUTION
-------------------------
The notebook is designed for execution in Kaggle. It installs/uses
Python packages including:
    datasets
    huggingface_hub
    numpy
    pandas
    scikit-learn
    tqdm
    z3-solver

Use the notebook cells in their intended order. The notebook downloads
and prepares benchmark data, defines the reasoning components, runs
the benchmark evaluations, and produces public prediction/report files.

IMPORTANT REPRODUCIBILITY NOTES
-------------------------------
- Benchmark outputs shown in the report are the recorded results from
  the executed notebook runs.
- CounterBench Alpha PBCI V1.0 is treated as a frozen reference
  implementation; its evaluation is not rerun in the final notebook.
- CounterBench Backdoor V2.1 is evaluated separately from Alpha.
- FOLIO parser recovery is conservative and only handles the already
  implemented missing-terminal-parenthesis case. The experimental
  extra-terminal-parenthesis repair was not adopted.
- No private-test accuracy is reported because private labels/data were
  not available at the time of preparing this submission.
- The combined 91.32% figure mixes benchmark splits and is not a
  normalized cross-benchmark performance measure.

OUTPUT FORMAT
-------------
The prediction CSV uses two columns:
    id,predicted_label

predicted_label is written as the string "True" or "False".


AUTHOR
------
Nitesh Kumar Mandal
M.Tech Artificial Intelligence
