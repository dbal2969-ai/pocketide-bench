# pocketide-bench

PocketIDE's live benchmark, run on GitHub's free runners. Public repositories get them free and without a minute limit
(4 CPUs, 16 GB of RAM, enough for Ollama with a 4B-8B model on the CPU); the app's own repositories are private and get
2 CPUs and 8 GB from a monthly allowance.

Only the workflow is here. The app's code stays private: each job checks it out with a read-only token.

## Secrets (Settings → Secrets and variables → Actions → New repository secret)

| Secret | What |
|---|---|
| `SOURCE_TOKEN` | Fine-grained token, read-only: Contents on `test-coder2.3` and `test-coder2.2` (required) |
| `NEON_DATABASE_URL` | The Neon connection string; results land in `bench_runs` / `bench_results` |
| `POCKETIDE_BENCH_KEY_OPENROUTER` | OpenRouter key |
| `POCKETIDE_BENCH_KEY_OLLAMACLOUD` | Ollama Cloud key |
| `POCKETIDE_BENCH_KEY_KILO` | Kilo key |
| others | `POCKETIDE_BENCH_KEY_<PROVIDER>` as in the app's own benchmark workflow |

Secrets are never shown in logs and are not given to pull requests from forks.

## Running

Actions → Benchmark (live models, free runners) → Run workflow. Examples:

- Cloud model: models `openrouter:ibm-granite/granite-4.2-8b`, suite `all`, repeat `3`.
- Local model on the runner's CPU: ollama `qwen3.5:4b`, models `ollama:qwen3.5:4b`, task_seconds `2400`.
- Small model mode on a cloud model: small `1`.

Logs of a public repository are public: they show task names, pass/fail and timings, never the keys.
Artifacts (reports, transcripts) are kept 3 days; the results stay in Neon.
