# Changelog — signetry-precommit

Follows [Keep a Changelog](https://keepachangelog.com/) / [SemVer](https://semver.org/).

## [Unreleased]

### Changed

- Signetry naming: CLI `signetry`, env `SIGNETRY_*`, config `.signetry/`, package
  `signetry-core`, and the sibling `signetry-reviewer`. The guard script is
  `universal/signetry-guard.sh` and the pre-commit hook `id` is `signetry-guard`.

## [0.3.0] — 2026-07-26

### Added

- Split out of the `signetry-plugins` monorepo into a dedicated repository under the
  [Signetry umbrella](https://github.com/Signetry/signetry), per the platform
  architecture (one repo per integration).
- Pins `signetry-core>=0.3.0` (capability graph, plan binding, masked verifier,
  G1/G2/G3 gates, extension admission).
