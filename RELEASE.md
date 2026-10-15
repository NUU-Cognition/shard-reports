# 0.2.0

- The workflow Create Report has an invocation file of the format `shard-invocation/0.2` (NUU Orbh Task 744). `flint shard invoke rpt create --input source="<the artifact or the topic>"` starts one. The steps are `create` and `review`. The output is `report`.
- Inside a task, the report opens as a child of the task (the default parent). The `report` step of the Projects workflows gives the command.
- This version needs a Flint CLI with shard invocations 0.2 (NUU Orbh Task 744).

# 0.1.4

- The dependency on the Flint shard accepts any version (`"@nuucognition/flint": ""`), so the shard works with Flint 0.3.x and with Flint 0.4.0 (NUU Flint Task 1129).

# 0.1.0

- Initial shard scaffold
