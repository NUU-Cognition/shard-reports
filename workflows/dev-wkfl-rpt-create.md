> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

This workflow belongs to the Reports shard. Ensure you have the @init-rpt.md in context before continuing.

# Workflow: Create Report

Create a new report.

# Invocation

You can run this workflow as a shard invocation. The invocation is a durable record of the report: its steps and its output. The stages below do not change.

- Start the workflow with `flint shard invoke rpt create --input source="<the artifact or the topic>"`. The input `source` is optional. In a headless session, use [[dev-hwkfl-rpt-create]] (`--headless`): its review needs no person.
- Inside an open task, the report runs as a child of the task: the default parent is the current frame of the session. The `report` step of `wkfl-proj-do_task` gives the exact command.
- After Stage 1, set the output: `flint shard invocations set-output <id> report="(Report) NNN Title"`. The hint after each write prints the command with the id of the invocation. When the report closes, the parent gets this output.
- Mark each step when it is done: `flint shard step done <step> --evidence "<…>"`. The steps are `create` and `review`.
- After Stage 2, close the invocation: `flint shard invocations close <id> --outcome done`. Then the parent is the current frame again.
- When no invocation is open, follow the stages with no record.

# Input

- Report topic or title
- (Optional) Type of report (research, code review, concept explainer, etc.)
- (Optional) Initial content or context

# Actions

## Stage 1: Report Creation

- Get the next report number with `flint helper type newnumber Report`
- Create the report using @tmp-rpt-report template in `Mesh/Types/Reports/`
- Set status to `active`
- Set date-created to today's date
- Fill in the Summary and initial Content based on provided context
- Once created, progress to the next stage

## Stage 2: Report Review

- Present the report draft to the user
- Refine content based on user feedback
- Once user confirms the report is complete, workflow is done

# Output

- New report in `Mesh/Types/Reports/`
- Report visible in `(Dashboard) Reports.md`
