> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

This workflow belongs to the Reports shard. Ensure you have the @init-rpt.md in context before continuing.

# Headless Workflow: Create Report

Create a report autonomously via Orbh. No step waits for a person: the review is a self-check. The person reads the report later.

# Invocation

You can run this workflow as a shard invocation. The invocation is a durable record of the report: its steps and its output. The steps below do not change.

- Start the workflow with `flint shard invoke rpt create --headless --input source="<the artifact or the topic>"`. The input `source` is optional.
- Inside an open headless task, the report runs as a child of the task: the default parent is the current frame of the session. The `report` step of `hwkfl-proj-do_task` gives the exact command.
- After step 1, set the output: `flint shard invocations set-output <id> report="(Report) NNN Title"`. The hint gives the id. When the report closes, the parent gets this output.
- Mark each step when it is done: `flint shard step done <step> --evidence "<…>"`. The steps are `create` and `review`.
- Outside an Orbh session (no `ORBH_SESSION_ID`), give `--invocation <id>` to `flint shard step`, for example `flint shard step done <step> --invocation <id> --evidence "<…>"`. The hint after each write prints the id.
- After step 2, close the invocation: `flint shard invocations close <id> --outcome done`. Then the parent is the current frame again.
- When no invocation is open, follow the steps with no record.

# Input

- Report topic or title, or the artifact that the report is for
- (Optional) Type of report (research, code review, concept explainer, etc.)
- (Optional) Initial content or context

# Actions

## 1. Create

- Get the next report number with `flint helper type newnumber Report`
- Create the report using @tmp-rpt-report template in `Mesh/Types/Reports/`
- Set status to `active`
- Set date-created to today's date
- Fill in the Summary and the Content from the source and the context
- Track the report in the Orbh interface:
  ```bash
  flint orbh artifact <id> "<report name>"
  ```

## 2. Review

Check the report yourself. Do not wait for a person.

- Read the full report again
- Check that the Summary states the result in a few sentences
- Check that each claim names its source: a file, a commit, a command and its output, or an artifact
- Check that no placeholder or template comment stays in the text
- Fix each problem that you find
- Then the workflow is done. The person reviews the report later.

# Output

- New report in `Mesh/Types/Reports/`, in `active` status
- With an open invocation: the output `report` is set
