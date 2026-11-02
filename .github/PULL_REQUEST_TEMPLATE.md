# Pull Request

## Summary

<!-- Provide a concise description of the motivation, changes, and architectural rationale. -->

## Changes

<!-- Group your changes logically according to architectural layers: -->
- **Core / Layout**:
- **Transforms / Codecs**:
- **Wire / Framing**:
- **Tooling / Tests**:

## Verification

<!-- Detail the automated and manual verification performed before opening the PR: -->
- [ ] `cargo fmt --all -- --check`
- [ ] `cargo clippy --workspace --all-targets --all-features -- -D warnings`
- [ ] `cargo test --workspace --all-targets --all-features`
- [ ] `cargo check --no-default-features` (strict `#![no_std]` compliance)
- [ ] `npx markdownlint-cli2 "**/*.md"` (0 issues)
- [ ] Miri verification (`cargo +nightly miri test` if applicable)

## Related Issues

<!-- Link relevant issues: Closes #123 / Ref #456 -->
