# Verification and Evaluation Plan

**Project:** AITU Strategy Monitoring System  
**Related document:** First pre-defense report, Section 9  
**Stage:** Planned verification — no execution results recorded

## 1. Purpose and Scope

The goal is to assess whether the implemented system meets its documented requirements for authentication, role-based permissions, KPI management, actual-result entry, validation, correct calculation, missing-value handling, filtering, reporting, and display of responsible departments.

The current interactive HTML prototype is not a deployed backend application. A working implementation will be required before authentication, persistence, permission enforcement, server performance, or end-to-end reporting can be tested.

## 2. Test Data

Use synthetic examples based on the **structure** of the AITU Development Strategy 2026–2030. Include annual targets and actual results for numeric, percentage, and milestone/status KPI types. Include missing target and missing actual values, and department assignments. Do not use real university results or confidential staff information without authorization.

Key handling rules:

- A missing value must not automatically be interpreted as zero.
- Numeric differences are computed only when the target and actual value are numeric and comparable.
- Milestone/status results are reported as statuses rather than numeric success percentages.
- Internal unique IDs must not rely on potentially repeated identifiers in the strategy document.
- Percentage validation must use the accepted range defined for the specific KPI; it should not assume all percentages have the same upper bound without confirmed business rules.

## 3. Functional Test Cases

The planned cases are listed in `test_cases.csv` and correspond to Table 9.1 in the report. Update the execution status and record evidence only when the corresponding test has actually been run.

`TC-10` covers change history and is conditional on implementation of the optional audit-history functionality; mark it `Not applicable` with a reason if the feature is excluded from the approved first implementation.

## 4. Evaluation Metrics

| Metric | Measurement | Provisional criterion |
|---|---|---|
| Functional test pass rate | Passed tests / executed tests × 100% | 100% of critical tests pass |
| Calculation accuracy | Compare outputs with independently computed expected values | All defined calculation cases pass |
| Data validation | Run valid and invalid input cases | All defined validation cases pass |
| Access control | Attempt operations under different roles | No unauthorized actions succeed |
| Response time | Measure common operations under the defined workload | At least 95% finish within 3 seconds |
| Task completion | Observe representative users completing selected workflows | At least 80% without assistance |

These targets are *provisional* and must be reviewed after requirements validation. The initial performance scenario assumes approximately **500 KPI records** and **10 concurrent users**, as described in Section 9 of the report.

## 5. Evaluation Procedure

1. **Prepare data:** create synthetic KPI records representing strategic directions, objectives, yearly targets and results. Include numeric, percentage, milestone, and missing-value cases.
2. **Verify functions:** run each applicable test case, compare actual with expected behavior, and record any defects.
3. **Evaluate performance and access control:** run timed scenarios in a specified environment after the application backend is implemented; try unauthorized actions using roles with known permissions.
4. **Evaluate usability:** ask representative participants to find a KPI, update a result, and generate a report. Obtain permission and document participant/task conditions. Record observed completion, duration and errors.

## 6. Spreadsheet Baseline

The baseline is a **controlled synthetic spreadsheet workflow**, not a claim about AITU's actual institutional monitoring process. Use the same KPI dataset and tasks for Excel (or equivalent) and for the developed application; see `baseline_tasks.csv`.

For each task, record operator, dataset, environment, task order, seconds to complete, whether the result is correct, and any errors. Try at least three repetitions per task when feasible. Note possible learning/order effects.

Compare median completion times using:

`Time improvement (%) = (median_baseline_seconds - median_system_seconds) / median_baseline_seconds * 100`

A **20% reduction** for selected reporting tasks is a proposed target, *not an achieved result*.

## 7. Evidence and Reporting

Record real results in a copy of `evaluation_results_template.csv`. Link relevant logs/screenshots or test run references when available. Report number of executed tests, passes, failures, exclusions, environment, dataset, and limitations. Do not label planned cases as passed before running them.
