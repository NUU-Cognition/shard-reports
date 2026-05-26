# Filename: Mesh/Types/Reports/(Report) XXX [Title].md

/* XXX is a 3-digit number. Get it with: flint helper type newnumber Report */

```markdown
---
id: [generate-uuid]
tags:
  - "#rpt/report"
status: [active|consumed]
date-created: [YYYY-MM-DD]
/* If Increments shard is installed: */
increment: "[[parent increment]]"
[agent]-sessions: /* replace [agent] with your agent type (claude, codex, etc.) */
template: "[[dev-tmp-rpt-report-v0.1]]"
authors: /* from .flint/identity.json; omit if no identity set */
  - "[[@Person Name]]"
---

# [Report Title]

## Summary

[Brief 1-3 sentence summary of the report's key findings or purpose]

## Content

[Main body of the report. Structure as needed for the topic - use headers, lists, code blocks, tables as appropriate]

### [Section 1]

[Content]

(continue as needed)

## Conclusions

[Key takeaways, recommendations, or next steps]

- [Conclusion or recommendation]
(continue)

## References

- [[Related documents]]
- [External links or sources]
(continue)
```

/* State Transitions:
   - active → consumed: Replace status
*/
