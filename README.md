# signetry-precommit

> **Copyright (c) 2026 Binay Dalai. All rights reserved.**
> This repository is strictly for viewing and contributing to the original project. You may not use, copy, modify, distribute, or commercialize this code for your own personal or commercial projects without explicit written permission. Only the original author retains the right to use and monetize this project.


**Govern coding-agent changes at the git boundary — pre-commit, pre-push, or CI.**

The universal, editor-agnostic guard for [signetry-core](https://github.com/Signetry/core):
a deterministic pre-action check that blocks changes falling outside your repo's
`.signetry/admission.yaml` scope, before they're committed or pushed.

Part of the [Signetry platform](https://github.com/Signetry/signetry).

> Prerequisite: `pip install "signetry-core @ git+https://github.com/Signetry/core@v0.6.0"` and a `.signetry/admission.yaml` in
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

**Copyright (c) 2026 Binay Dalai. All rights reserved.** This code is not open source. You may not use, copy, modify, distribute, or commercialize it for your own personal or commercial purposes without explicit written permission from the author, who alone retains the right to use and monetize this project. See [CONTRIBUTING.md](CONTRIBUTING.md).
