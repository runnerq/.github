**RunnerQ** gives you durable workflows and queues as a library, backed by the Postgres you already run.

You write workflows as ordinary functions, and RunnerQ checkpoints each step in Postgres. If a process crashes mid-workflow, the workflow resumes from where it stopped and completed steps don't run again. RunnerQ has no orchestrator cluster or broker: you import the library, point it at Postgres and run more stateless worker processes when you need to scale.

Workflows can sleep for days or wait for a signal without holding a worker, because a paused workflow is just a row in Postgres.

## Get started

- **Go:** follow the [README](https://github.com/runnerq/runnerq-go#readme) and the [examples](https://github.com/runnerq/runnerq-go/tree/main/examples), which include crash-and-resume, durable sleep, human approval, fan-out and exactly-once webhooks.
- **TypeScript:** follow the [quick start](https://github.com/runnerq/runnerq-ts#quick-start). It needs Node.js 22+, an ESM app and PostgreSQL.

## Open Source Repositories

- [RunnerQ Go](https://github.com/runnerq/runnerq-go): durable workflows and queues for Go, backed by Postgres
- [RunnerQ TypeScript](https://github.com/runnerq/runnerq-ts): durable activities and workflows for Node.js, backed by PostgreSQL
- [RunnerQ Rust](https://github.com/runnerq/runnerq-rust): activity queue and worker system for Rust with pluggable storage backends (PostgreSQL, Redis), published as [`runner_q`](https://crates.io/crates/runner_q)
- [runnerq-spec](https://github.com/runnerq/runnerq-spec): the language-neutral contract every RunnerQ implementation agrees on, covering shared constants, golden test vectors and the Postgres schema

### RunnerQ Cloud storage adapters

- [cloud-storage-go](https://github.com/runnerq/cloud-storage-go): RunnerQ Cloud hosted storage for the Go SDK
- [cloud-storage-ts](https://github.com/runnerq/cloud-storage-ts): RunnerQ Cloud hosted storage for the TypeScript SDK

The Go, TypeScript, Rust and spec repositories are MIT licensed.
