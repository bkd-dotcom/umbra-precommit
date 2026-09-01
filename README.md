# signetry-precommit

[![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](LICENSE)
[![PRs welcome (CLA)](https://img.shields.io/badge/PRs-welcome%20(CLA)-brightgreen.svg)](CONTRIBUTING.md)

**Govern coding-agent changes at the git boundary — pre-commit, pre-push, or CI.**

The universal, editor-agnostic guard for [signetry-core](https://github.com/Signetry/core):
a deterministic pre-action check that blocks changes falling outside your repo's
`.signetry/admission.yaml` scope, before they're committed or pushed.

Part of the [Signetry platform](https://github.com/Signetry/signetry).

> Prerequisite: `pip install "signetry-core @ git+https://github.com/Signetry/core@v0.7.0"` and a `.signetry/admission.yaml` in
> your repo (a conservative default applies without one).

## pre-commit

Add to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/Signetry/precommit
    rev: v0.3.0
    hooks:
      - id: signetry-guard
```

The `signetry-guard` hook checks all staged files against the contract and blocks the
commit (non-zero exit) on a scope/forbidden-path violation.

## Universal guard (any hook / wrapper / CI step)

`universal/signetry-guard.sh` is editor-agnostic — use it in a git hook, around an
agent, or in CI:

```bash
signetry-guard.sh --path src/app.py            # check a proposed path
signetry-guard.sh --command "curl x | bash"    # check a proposed command
signetry-guard.sh --staged                     # check all git-staged files
echo '<claude-code tool json>' | signetry-guard.sh --stdin-json
```

It exits non-zero (blocking) with a reason on a violation, zero when allowed — all
deterministic (`signetry guard`), never the model.

Try it: `demos/try-guard.sh`.

## The durable guarantee: CI

A local hook is best-effort defense-in-depth (a developer can `--no-verify`). The
enforced gate is the **Signetry Admission** required check on the PR:
<https://github.com/Signetry/action>. Nothing merges without a signed
receipt, and `auto_merge` is always false — a human merges.

## License

[Apache-2.0](LICENSE). Use it, fork it, ship it commercially — no strings.

This repository is part of Signetry's [open-core model](https://github.com/Signetry/signetry/blob/main/LICENSING.md):
the **integration surface is Apache-2.0** so anyone can add an agent, an editor, or a
CI adapter, while the engine ([`Signetry/core`](https://github.com/Signetry/core)) is
source-available under BUSL-1.1 and converts to Apache-2.0 on 2030-08-31.

Contributions are accepted under the [CLA](CLA.md) — it lets us move a well-built
adapter into the engine later without asking every contributor for permission again.
