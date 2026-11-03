# Contributing to stitch-rs Ecosystem Projects

First off, thank you for considering contributing to **stitch-rs**!
Our projects focus on zero-cost abstractions, monomorphic execution pipelines,
and ultra-high-performance data engineering.

To maintain production-grade reliability and architectural purity, we adhere
to the strict engineering guidelines detailed below.

---

## 1. Governance & Code of Conduct

All contributors, maintainers, and community members must abide by the
[Code of Conduct](CODE_OF_CONDUCT.md). We are committed to providing a
welcoming, constructive, and harassment-free experience for everyone.

---

## 2. Repository & Branching Strategy

Our repositories enforce a structured Git branching workflow:

- **`main`**: Production and stable release tags only. Protected branch;
  direct commits are prohibited.
- **`dev`**: Active integration branch. All features, refactorings, and
  fixes are merged here via Pull Requests.
- **`feature/<name>`**: New capabilities or experimental subsystems
  branched from `dev`.
- **`fix/<name>`**: Bug fixes and regression remedies branched from `dev`.
- **`hotfix/<name>`**: Critical hotfixes branched directly from `main`
  when necessary.

---

## 3. Commit Message Standards

We strictly enforce the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
specification. Every commit message must be in the imperative mood and
in English:

```text
<type>(<optional-scope>): <description in imperative mood>

[optional body]

[optional footer(s)]
```

### Allowed Types

- `feat`: A new user-facing or public API capability.
- `fix`: A bug fix, panic fix, or memory safety remedy.
- `docs`: Documentation updates, specs, or RFC amendments.
- `refactor`: Code adjustments without altering external behavior or adding features.
- `perf`: Measurable performance improvements backed by benchmark proofs.
- `test`: Unit, integration, fuzzing, or property-based test additions.
- `build`: Cargo build scripts, dependencies, or toolchain adjustments.
- `ci`: GitHub Actions workflows or automated lint configurations.
- `chore`: Housekeeping, formatting, or repository hygiene.

---

## 4. Systems Engineering & Quality Principles

Contributors must respect our core systems engineering tenets:

### 4.1 Scrooge Systems Mindset (Mechanical Sympathy)

- **Cache-Line Efficiency**: Align critical hot-path lookup records to 64-byte
  L1D cache boundaries. Eliminate struct padding holes using `repr(C)` and
  sorted field definitions.
- **Contiguous Flat Layouts**: Prefer contiguous zero-copy memory slices
  (`zerocopy`, `mmap`) over pointer-chasing and dynamic allocations (`Box<dyn ...>`).
- **Zero-Allocation Hot Paths**: Serializers, decoders, and pipeline traversals
  must run in `#![no_std]` without allocating on heap.

### 4.2 Explicit Failure & Anti-Silent Error Suppression

- Never swallow errors or return dummy fallbacks (`0`, `""`, `None`) on failure.
- Always propagate errors using typed domain errors (`Result<T, E>`).
- The use of `.unwrap()`, `.expect()`, or lazy fallback defaults on untrusted
  input is strictly forbidden.

### 4.3 Safety Boundaries & FFI

- Wrap unsafe operations in safe, zero-cost abstractions.
- Every `unsafe` block must include an explicit `// SAFETY:` explanatory
  comment describing invariants and proof of correctness.
- Panics must never cross C-ABI or external host boundaries (use `catch_unwind`
  or error barriers).

---

## 5. Automated Git Hooks & Pre-PR Local Verification

To completely eliminate CI build failures caused by formatting or Clippy warnings, we provide
native, zero-dependency Git pre-commit hooks located in `.githooks/`.

### 5.1 Setting Up Git Hooks

Run the setup helper once to configure Git:

```bash
# Enable repository-level hooks
git config core.hooksPath .githooks
chmod +x .githooks/*
```

Or execute `./scripts/setup-hooks.sh` if provided in the repository.

Once configured, Git will automatically run `cargo fmt --all`, re-stage modified files,
and run `cargo clippy` before allowing any commit to proceed.

### 5.2 Manual Quality Checklist

Before pushing commits and submitting a Pull Request, ensure that all local
quality gates pass with zero warnings:

```bash
# 1. Formatting check
cargo fmt --all -- --check

# 2. Strict Clippy check with zero warnings allowed
cargo clippy --workspace --all-targets --all-features -- -D warnings

# 3. Comprehensive test suite
cargo test --workspace --all-targets --all-features

# 4. Strict #![no_std] verification
cargo check --no-default-features

# 5. Markdown documentation linting
npx markdownlint-cli2 "**/*.md"
```

---

## 6. Pull Request Process

1. Fork the repository and create your branch from `dev`.
2. Write unit tests proving your changes and preventing regressions.
3. If introducing architectural shifts or new wire formats, provide or update
   the corresponding RFC/Architecture specification.
4. Ensure all CI checks turn green on your PR.
5. Await review from maintainers.
