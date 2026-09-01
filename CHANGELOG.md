# Changelog — signetry-precommit

Follows [Keep a Changelog](https://keepachangelog.com/) / [SemVer](https://semver.org/).

## [Unreleased]

### Changed

- **Licence: this repository is now [Apache-2.0](LICENSE)** (previously
  all-rights-reserved / source-available). Signetry has moved to an open-core model:
  the integration surface — this repo, the GitHub Action, the editor and agent plugins,
  the eval suite — is Apache-2.0, while the engine
  ([`signetry-core`](https://github.com/Signetry/core)) is BUSL-1.1 and converts to
  Apache-2.0 on 2030-08-31. The CLA is retained so contributions can be relicensed
  across that boundary; it does not reduce anyone's Apache-2.0 rights. See
  [CONTRIBUTING.md](CONTRIBUTING.md).
- Signetry naming: CLI `signetry`, env `SIGNETRY_*`, config `.signetry/`, package
  `signetry-core`, and the sibling `signetry-reviewer`. The guard script is
  `universal/signetry-guard.sh` and the pre-commit hook `id` is `signetry-guard`.
- **The CLA's fallback licence grant is now non-exclusive.** It previously granted the
  Owner an *exclusive* licence where copyright assignment is not permitted by law, which
  would have stripped contributors of the right to use their own contribution — directly
  contradicting the rights the LICENSE grants everyone. The CLA text is now identical
  across all Signetry repositories (bar the engine/integration licence wording) so the
  legal terms cannot drift per-repo again. See [CLA.md](CLA.md) §2–3.

## [0.3.0] — 2026-07-26

### Added

- Split out of the `signetry-plugins` monorepo into a dedicated repository under the
  [Signetry umbrella](https://github.com/Signetry/signetry), per the platform
  architecture (one repo per integration).
- Pins `signetry-core>=0.3.0` (capability graph, plan binding, masked verifier,
  G1/G2/G3 gates, extension admission).
