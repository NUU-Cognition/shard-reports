# 0.2.1

- One workflow for each mode (NUU Orbh Task 748). The headless workflow `hwkfl-rpt-create` and the headless init `hinit-rpt` are merged into `wkfl-rpt-create` and `init-rpt`. The review stage has a `> [!headless]` callout: a headless session does a self-check with no person gate. One invocation file serves both modes, and the mode comes from the Orbh session. A headless task calls `flint shard invoke rpt create` with no `--headless`.
- This version needs a Flint CLI with shard invocations 0.3 (NUU Orbh Task 748).

# 0.2.0

- The workflow Create Report has an invocation file of the format `shard-invocation/0.2` (NUU Orbh Task 744). `flint shard invoke rpt create --input source="<the artifact or the topic>"` starts one. The steps are `create` and `review`. The output is `report`.
- Inside a task, the report opens as a child of the task (the default parent). The `report` step of the Projects workflows gives the command.
- A new headless workflow `hwkfl-rpt-create` has the same steps and its own invocation file. Its review is a self-check with no person gate. A headless task calls it with `flint shard invoke rpt create --headless`.
- A headless init `hinit-rpt` (new): `flint shard invoke rpt create --headless` and `flint shard hstart rpt` need it.
- This version needs a Flint CLI with shard invocations 0.2 (NUU Orbh Task 744).

# 0.1.4

- The dependency on the Flint shard accepts any version (`"@nuucognition/flint": ""`), so the shard works with Flint 0.3.x and with Flint 0.4.0 (NUU Flint Task 1129).

# 0.1.0

- Initial shard scaffold
