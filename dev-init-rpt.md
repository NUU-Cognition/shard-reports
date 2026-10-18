# Reports Shard

Create and organize reports - research findings, code reviews, concept explainers, or any structured write-up.

## Report Lifecycle

```
active → consumed
```

| Status | Meaning |
|--------|---------|
| `active` | Report is current and relevant |
| `consumed` | Report has been read/used, kept for reference |

## Dashboards

| Dashboard | Purpose | Maintained By |
|-----------|---------|---------------|
| `(Dashboard) Reports.md` | Shows all reports by status | DataviewJS |

## Templates

| Template | File | Purpose |
|----------|------|---------|
| Report | `dev-tmp-rpt-report.md` | Standard report format |

## Workflows

| Workflow | File | Purpose |
|----------|------|---------|
| Create Report | `dev-wkfl-rpt-create.md` | Create a new report |

## Invocations

- `flint shard invoke rpt create --input source="<the artifact or the topic>"` opens the workflow Create Report (`wkfl-rpt-create.invocation.json`, format `shard-invocation/0.3`). The steps are `create` and `review`. The output is `report`.
- Inside an open task (`flint shard invoke proj do_task`), the report opens as a child of the task. The `report` step of the task prints the exact command.
- Mark each step with `flint shard step done <step> --evidence "<…>"`. Set the output with `flint shard invocations set-output <id> report="(Report) NNN Title"`. Close the invocation with `flint shard invocations close <id> --outcome done`.
- The mode comes from the Orbh session: a headless or subagent session runs in the headless mode, with the same command. The workflow has `> [!headless]` callouts, and the step `review` has a hint for each mode.

# Headless

A headless or subagent Orbh session has no person at the terminal. It loads this init with `flint shard start rpt`, as an interactive session does. The report lifecycle (`active → consumed`), the dashboard, and the template do not change. Follow the `> [!headless]` callouts of the workflow: the review is a self-check, and no step waits for a person.

## Orbh Interface

Track each report that you create: `flint orbh artifact "Mesh/Types/Reports/(Report) NNN Title.md"`.

## Result Delivery

- Inside a task, the task returns the result of the session. Give the title of the report to the task: the output `report`.
- A session that only makes the report ends with `flint orbh session return --finish "<result>"`. Put the title of the report and its summary in the result.
