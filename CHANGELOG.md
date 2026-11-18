# Changelog

## [Unreleased]

### Fixed
- German-locale statements (`Kontoauszug`, from April 2026 onward) parsed to
  0 transactions: amounts like `-245,36 EUR` / `+1.234,56 EUR` are now read in
  transaction rows and balance lines.
- Statements failed ofxstatement's balance validation because Scalable prints
  the opening balance as of the first value date. When start + transactions ≠
  end, the start balance is now derived from the (reliable) end balance and a
  warning is logged; the printed value stays available as
  `parser.printed_start_balance`.
- German page footers (`Geschäftsführer: …`, `Aufsichtsrat: …`) no longer leak
  into transaction memos.

### Added
- Transaction types `Erhaltene Zinsen` (INT) and `Abhebung vom Geldkonto`
  (XFER), confirmed against real statements.

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
