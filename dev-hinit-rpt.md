# Reports Shard — Headless

You are running headless via Orbh. This file replaces `dev-init-rpt.md` for headless sessions. The report lifecycle (`active → consumed`), the dashboard, and the template are unchanged: read `dev-init-rpt.md` for them. Reports are created with the [[dev-tmp-rpt-report-v0.1]] template. This file says what is different when no person is at the terminal.

## Headless Workflows

Use these instead of the interactive `wkfl-*` counterparts. No step waits for a person.

| Workflow | File | Replaces | When to use |
|----------|------|----------|-------------|
| Create Report | `dev-hwkfl-rpt-create.md` | `dev-wkfl-rpt-create.md` | Create a report; the review is a self-check |

## Invocations

- `flint shard invoke rpt create --headless --input source="<the artifact or the topic>"` opens the headless workflow (`hwkfl-rpt-create.invocation.json`). The steps are `create` and `review`. The output is `report`.
- Inside an open headless task (`flint shard invoke proj do_task --headless`), the report opens as a child of the task. The `report` step of the task prints the exact command.
- Mark each step with `flint shard step done <step> --evidence "<…>"`. Set the output with `flint shard invocations set-output <id> report="(Report) NNN Title"`. Close the invocation with `flint shard invocations close <id> --outcome done`.

## Orbh Interface

Track each report that you create: `flint orbh artifact <id> "<report name>"`.
