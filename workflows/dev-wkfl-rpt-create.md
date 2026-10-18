> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

This workflow belongs to the Reports shard. Ensure you have the @init-rpt.md in context before continuing.

# Workflow: Create Report

Create a new report.

> [!headless]
> In a headless or subagent Orbh session, no person is at the terminal. Do each stage, and follow the `> [!headless]` callout in it. No step waits for a person: the review is a self-check, and the person reads the report later.

# Invocation

You can run this workflow as a shard invocation. The invocation is a durable record of the report: its steps and its output. The stages below do not change.

- Start the workflow with `flint shard invoke rpt create --input source="<the artifact or the topic>"`. The input `source` is optional.
- The mode comes from the Orbh session. A headless or subagent session runs in the headless mode and follows the `> [!headless]` callouts, with the same command. In a headless session, the hint of the step `review` names the self-check. `flint shard step` shows the current step and each step that the mode skipped.
- Inside an open task, the report runs as a child of the task: the default parent is the current frame of the session. The `report` step of `wkfl-proj-do_task` gives the exact command.
- In Stage 1, set the output, and then mark the step `create` done: `flint shard invocations set-output <id> report="(Report) NNN Title"`. Else the hints of the later steps print `{{output.report}}` and not the title. The hint after each write prints the command with the id of the invocation. When the report closes, the parent gets this output.
- Mark each step when it is done: `flint shard step done <step> --evidence "<…>"`. The steps are `create` and `review`.
- Outside an Orbh session (no `ORBH_SESSION_ID`), give `--invocation <id>` to `flint shard step`, for example `flint shard step done <step> --invocation <id> --evidence "<…>"`. The hint after each write prints the id.
- After Stage 2, close the invocation: `flint shard invocations close <id> --outcome done`. Then the parent is the current frame again.
- When no invocation is open, follow the stages with no record.

# Input

- Report topic or title
- (Optional) Type of report (research, code review, concept explainer, etc.)
- (Optional) Initial content or context

> [!headless]
> - The input can also be the artifact that the report is for.

# Actions

## Stage 1: Report Creation

- Get the next report number with `flint helper type newnumber Report`
- Create the report using @tmp-rpt-report template in `Mesh/Types/Reports/`
- Set status to `active`
- Set date-created to today's date
- Fill in the Summary and initial Content based on provided context
- Once created, progress to the next stage

> [!headless]
> - Fill in the Summary and the Content from the source and the context.
> - Track the report in the Orbh interface: `flint orbh artifact "Mesh/Types/Reports/(Report) NNN Title.md"`.

## Stage 2: Report Review

- Present the report draft to the user
- Refine content based on user feedback
- Once user confirms the report is complete, workflow is done

> [!headless]
> Check the report yourself. Do not wait for a person.
> - Read the full report again
> - Check that the Summary states the result in a few sentences
> - Check that each claim names its source: a file, a commit, a command and its output, or an artifact
> - Check that no placeholder or template comment stays in the text
> - Fix each problem that you find
> - Then the workflow is done. The person reviews the report later.

# Output

- New report in `Mesh/Types/Reports/`
- Report visible in `(Dashboard) Reports.md`

> [!headless]
> - The report is in `active` status
> - With an open invocation: the output `report` is set
