# Changelog — signetry-precommit

Follows [Keep a Changelog](https://keepachangelog.com/) / [SemVer](https://semver.org/).

## [Unreleased]

### Changed

- Rebranded the platform from Umbra to Signetry: CLI `umbra` → `signetry`, env
  `UMBRA_*` → `SIGNETRY_*`, config `.umbra/` → `.signetry/`, package
  `umbra-core` → `signetry-core`, and the sibling `umbra-reviewer` →
  `signetry-reviewer`. Renamed `universal/umbra-guard.sh` → `universal/signetry-guard.sh`
  and updated the pre-commit hook `id` `umbra-guard` → `signetry-guard`.

## [0.3.0] — 2026-07-26

### Added

- Split out of the `signetry-plugins` monorepo into a dedicated repository under the
  [Signetry umbrella](https://github.com/Signetry/signetry), per the platform
  architecture (one repo per integration).
- Pins `signetry-core>=0.3.0` (capability graph, plan binding, masked verifier,
  G1/G2/G3 gates, extension admission).
