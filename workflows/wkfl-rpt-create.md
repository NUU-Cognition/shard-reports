This workflow belongs to the Reports shard. Ensure you have the @init-rpt.md in context before continuing.

# Workflow: Create Report

Create a new report.

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
