# Failure Accounting and Stop Scope

Apply explicit user limits and stop scope first. These defaults distinguish quality failures from execution incidents without allowing either to loop indefinitely.

## Record the outcome before counting it

| Outcome | Evidence | Counter and response |
| --- | --- | --- |
| Reviewed candidate fails an intended visual or functional criterion | A candidate exists and independent review can assess that criterion | Increment that problem's `failed_candidates`; reject or roll back according to the mode's gate. |
| Tool, environment, context, or validation-harness incident prevents reliable review | Error or invalid evidence; criterion outcome is unknown | Increment the matching `execution_incidents` entry; restore any partial mutation and repair only the execution path. Do not invent a visual failure or pass. |
| Protection check fails | Protected values differ, or the check cannot establish preservation | Do not accept. Restore the last accepted state and investigate. Record an execution incident when no criterion was reviewable; otherwise record the failed candidate with protection as a failure reason. |

Keep a stable `problem_id` tied to the **observable unmet criterion and target region**, not a broad feature such as “the clock.” Changing the suspected cause or technique does not reset the same defect's counter. Record secondary reasons, but do not double-count one failed event across counters. If a new criterion is genuinely failing, record why it is distinct and retain the old unresolved problem.

Record before/candidate paths, evidence, outcome, failure category, counter increment, and Coordinator decision in history. The Modeler's assertion or a theoretical calculation cannot replace an independent result from actual outputs.

## Bounded recovery

- Default maximum: **3 failed candidates per problem**. After two failures, diagnose and change the hypothesis before another candidate. At the limit, stop that branch and report cause, evidence, and missing requirements.
- Default maximum: **3 execution incidents per recurring cause within the task**, including incidents in diagnostic runs. At the limit, stop the affected execution path and report the blocker. Do not reset this counter by changing labels or starting a new stage.
- An isolated diagnostic batch must state finite tests, changed variables, protected data, and an end condition before execution. Diagnostic-only images are not accepted candidates; failed executions still count. Do not keep extending diagnostics to evade either limit.
- Allowed inspection changes (for example cameras or evaluation time) must be named before execution. Do not excuse unexpected shared-data mutations retrospectively. Separate render state from asset state in preservation checks and restore both as specified.

“Stop that branch” means stop the unresolved correction or experiment. If optional, retain the verified required delivery and report the omission. If required, keep the task incomplete; unrelated safe work may continue only when consistent with the user's stop scope. If the user says to stop all work after the limit, stop all work. Changing this policy never retroactively authorizes resuming a stopped task.
