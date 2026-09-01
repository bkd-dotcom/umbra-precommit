# Contributing to signetry-precommit

This repository is **[Apache-2.0](LICENSE)**. You may use, copy, modify, distribute,
and commercialize it — including in closed-source and commercial products — with no
permission needed and no fee. Contributions are very welcome.

## Licensing, in short

- **The code here is Apache-2.0.** Fork it, vendor it, ship it. Attribution and the
  licence notice are the only obligations, per the [LICENSE](LICENSE).
- **A signed CLA is still required before a PR merges** (see below). That is not a
  walk-back of the open licence — it is what keeps the open-core boundary movable.
- This repo is the *integration surface*. The engine
  ([`signetry-core`](https://github.com/Signetry/core)) is source-available under
  BUSL-1.1 and converts to Apache-2.0 on **2030-08-31**. See the platform's
  [LICENSING.md](https://github.com/Signetry/signetry/blob/main/LICENSING.md).

## Why the CLA still applies

Signetry is open core, so code legitimately moves **across the line between this
Apache-2.0 repo and the BUSL-1.1 engine**. A guard adapter that proves itself here may
later belong inside `signetry-core`; conversely, engine logic may be pushed out to the
open integration surface. The CLA gives the maintainer the relicensing rights needed to
do that — and to carry contributions through the engine's 2030 conversion to
Apache-2.0 — without tracking down every past contributor for permission.

Signing the CLA does **not** take away your rights to this code: you keep the same
Apache-2.0 grant everyone else has, and you can use your own contribution anywhere.

## Signing the CLA (required before merge)

This is enforced by a bot. When you open a pull request, the **CLA Assistant** check
will ask you to sign the [Contributor License Agreement](CLA.md). Reply on the PR
with exactly:

```
I have read the CLA Document and I hereby sign the CLA
```

Your acceptance is recorded in `signatures/cla.json`. A PR **cannot be merged** until
the CLA is signed.

## Getting started

The guard itself is a POSIX shell wrapper — there is no build step and no Python
package in this repo. It shells out to the `signetry` CLI, so install the engine first:

```bash
pip install "signetry-core @ git+https://github.com/Signetry/core@v0.8.0"
```

Then exercise the guard end-to-end against a throwaway repo with a sample
`.signetry/admission.yaml`:

```bash
bash demos/try-guard.sh
```

To drive `universal/signetry-guard.sh` by hand:

```bash
universal/signetry-guard.sh --path src/app.py            # check a proposed path
universal/signetry-guard.sh --command "curl x | bash"    # check a proposed command
universal/signetry-guard.sh --staged                     # check all git-staged files
echo '<claude-code tool json>' | universal/signetry-guard.sh --stdin-json
```

Useful environment variables when testing: `SIGNETRY_REPO` overrides the detected repo
root, and `SIGNETRY_GUARD_STRICT=1` makes a missing `signetry` binary fail closed
instead of failing open.

If you change the pre-commit hook contract, keep `.pre-commit-hooks.yaml` (hook id
`signetry-guard`) and the README's `rev:` example consistent with each other.

## What lands well

- **Determinism.** The guard must never ask a model for a verdict — every decision
  comes from `signetry guard` and the repo's `.signetry/admission.yaml`.
- **No policy reimplementation.** This repo pins `signetry-core` and defers to it; do
  not re-encode contract semantics here.
- **Honest failure modes.** The local hook is defense-in-depth (a developer can
  `--no-verify`); the hard gate is the required check on the PR. Don't document it as
  more than it is. See [SECURITY.md](SECURITY.md).

## Opening a PR

1. Fork, branch, and keep the change focused.
2. Run `bash demos/try-guard.sh` and confirm the blocked cases still block.
3. Open the PR. An advisory reviewer workflow comments on architecture and security
   concerns; it never merges and never fails your PR.
4. Sign the CLA when the bot asks.

By participating you agree to the [Code of Conduct](CODE_OF_CONDUCT.md).

## Credit

Contributors are acknowledged in [CONTRIBUTORS.md](CONTRIBUTORS.md), the Git history,
and release notes.
