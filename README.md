# umbra-precommit

**Govern coding-agent changes at the git boundary — pre-commit, pre-push, or CI.**

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
The universal, editor-agnostic guard for [umbra-core](https://github.com/bkd-dotcom/umbra-core):
a deterministic pre-action check that blocks changes falling outside your repo's
`.umbra/admission.yaml` scope, before they're committed or pushed.

Part of the [Umbra platform](https://github.com/bkd-dotcom/umbra-umbrella).

> Prerequisite: `pip install "umbra-core>=0.3.0"` and a `.umbra/admission.yaml` in
> your repo (a conservative default applies without one).

## pre-commit

Add to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/bkd-dotcom/umbra-precommit
    rev: v0.3.0
    hooks:
      - id: umbra-guard
```

The `umbra-guard` hook checks all staged files against the contract and blocks the
commit (non-zero exit) on a scope/forbidden-path violation.

## Universal guard (any hook / wrapper / CI step)

`universal/umbra-guard.sh` is editor-agnostic — use it in a git hook, around an
agent, or in CI:

```bash
umbra-guard.sh --path src/app.py            # check a proposed path
umbra-guard.sh --command "curl x | bash"    # check a proposed command
umbra-guard.sh --staged                     # check all git-staged files
echo '<claude-code tool json>' | umbra-guard.sh --stdin-json
```

It exits non-zero (blocking) with a reason on a violation, zero when allowed — all
deterministic (`umbra guard`), never the model.

Try it: `demos/try-guard.sh`.

## The durable guarantee: CI

A local hook is best-effort defense-in-depth (a developer can `--no-verify`). The
enforced gate is the **Umbra Admission** required check on the PR:
<https://github.com/bkd-dotcom/umbra-action>. Nothing merges without a signed
receipt, and `auto_merge` is always false — a human merges.

## License

[MIT](LICENSE) © 2026 Binay Dalai.
