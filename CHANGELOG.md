# Changelog

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
