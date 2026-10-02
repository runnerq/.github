**RunnerQ** is durable execution as a library. Import it into your app, point it at Postgres and write workflows as ordinary functions. RunnerQ handles the queueing, retries, checkpoints and crash recovery, with no orchestrator cluster or broker to run.

## How it works

- **A workflow is just a function.** Orchestration is normal control flow (loops, conditionals, error handling) rather than a DSL or a DAG.
- **Steps are checkpointed.** Each step's result is stored in the backend. When a process crashes, the workflow resumes where it stopped, and completed steps return their stored results instead of running again.
- **Workflows pause for free.** A workflow can sleep for days or wait for a signal without holding a worker, because a paused workflow is just stored state.
- **You scale by adding workers.** Workers are stateless processes that claim work from the backend.

## Pluggable storage backends

RunnerQ persists everything through a storage interface that each SDK exports:

- **PostgreSQL** is the built-in backend in every SDK.
- **Your own backend:** implement the storage interface (`storage.Storage` in Go, the `runnerq/storage` contract in TypeScript, the `Storage` trait in Rust). Go ships a conformance suite, `storage/storagetest`, which runs every behaviour the engine relies on against your backend. If your backend passes it, the engine works on it exactly as it does on Postgres.
- **RunnerQ Cloud hosted storage:** the [cloud-storage-go](https://github.com/runnerq/cloud-storage-go) and [cloud-storage-ts](https://github.com/runnerq/cloud-storage-ts) adapters plug in the same way. Your workers still run your handlers locally, and storage and coordination go to RunnerQ Cloud.

## Get started

- **Go:** start with the [README](https://github.com/runnerq/runnerq-go#readme). The [examples](https://github.com/runnerq/runnerq-go/tree/main/examples) cover crash-and-resume, durable sleep, human approval, fan-out and exactly-once webhooks.
- **TypeScript:** follow the [quick start](https://github.com/runnerq/runnerq-ts#quick-start). It needs Node.js 22+, an ESM app and PostgreSQL.
- **Rust:** add [`runner_q`](https://crates.io/crates/runner_q) and follow the [README](https://github.com/runnerq/runnerq-rust#readme).

## Open Source Repositories

| Repository | What it is |
|---|---|
| [runnerq-go](https://github.com/runnerq/runnerq-go) | Durable Go functions, with pluggable storage |
| [runnerq-ts](https://github.com/runnerq/runnerq-ts) | Durable TypeScript functions, with pluggable storage |
| [runnerq-rust](https://github.com/runnerq/runnerq-rust) | Activity queue and worker system for Rust |
| [runnerq-spec](https://github.com/runnerq/runnerq-spec) | The language-neutral contract every RunnerQ implementation follows: shared constants, golden test vectors and the Postgres schema |
| [cloud-storage-go](https://github.com/runnerq/cloud-storage-go) | RunnerQ Cloud storage backend for the Go SDK |
| [cloud-storage-ts](https://github.com/runnerq/cloud-storage-ts) | RunnerQ Cloud storage backend for the TypeScript SDK |

The SDKs and the spec are MIT licensed.
