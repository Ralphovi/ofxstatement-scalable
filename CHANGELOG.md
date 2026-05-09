# Changelog

## [0.1.2] - 2026-05-08

### Developer tooling
- Added `build` and `twine` to `[project.optional-dependencies].dev` so
  contributors can `python -m build --sdist --wheel` and `twine upload`
  without an extra `pip install`.
- Refreshed `Makefile`: typo-free `.PHONY:` declarations (the previous
  file said `PHONY:` without the leading dot, so the directive did
  nothing); added a `ruff` target and a `package` target (`python3 -m
  build --sdist --wheel`); dropped stale references to `bin/pytest`
  and `setup.py` (the latter was deleted in the pyproject.toml
  migration). Mirrors the cleanup the upstream paypal-2 maintainer
  applied to that plugin.

## [0.1.1] - 2026-05-04

### Added
- `parse()` now logs the installed plugin version as its first INFO
  line. Lets a user reading the convert output confirm which install
  actually ran, without having to drop out and `pip show
  ofxstatement-scalable`. Resolved at runtime via
  `importlib.metadata.version` with a graceful `"unknown"` fallback.

## [0.1.0] - 2026-04-06

### Added
- Initial release: PDF Cash Account Statement parser for Scalable Capital Bank
- IBAN and BIC extraction from the clearing account header line
- Statement period and start/end balance parsing (German locale `1.234,56`)
- Transaction rows parsed from the table (booking date, value date, description, amount)
- Stable transaction IDs (MD5 of booking date / value date / description / amount)
- `CREDIT` / `DEBIT` transaction type assigned from the amount sign
