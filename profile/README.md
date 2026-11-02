# Stitch Organization

<div align="center">

[![Rust: 2024 Edition](https://img.shields.io/badge/rust-2024_edition-orange.svg?logo=rust&logoColor=orange)](https://doc.rust-lang.org/edition-guide/rust-2024/)
[![License: MIT OR Apache-2.0](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue.svg)](#license)
[![GitHub](https://img.shields.io/badge/github-stitch--rs-181717?logo=github)](https://github.com/stitch-rs)

**Monomorphic, Zero-Allocation Systems Architecture & High-Performance Data Engineering for Rust.**  
*Home of the Sewing Machine Architecture (SMA), Adaptive Data Layouts, and Microsecond Wire Protocols.*

</div>

---

## Welcome to Stitch (`stitch-rs`)

**Stitch** is a high-performance, modular systems engineering platform
designed to eliminate runtime allocation overhead, virtual dispatch
(`Box<dyn ...>`), and cache thrashing across data transformation,
network framing, and transactional execution pipelines.

Rooted in the **Sewing Machine Architecture (SMA)**, Stitch decomposes
complex workflows into strictly bounded, cache-aligned U-cycles with
zero runtime cost.

### Core Architectural Pillars

- **The Monomorphic U-Cycle (SMA)**: Zero dynamic dispatch, total function
  contracts on ascent, and full compiler inlining across execution chains.
- **The Scrooge Systems Mindset**: Mechanical sympathy to 64-byte L1D cache
  lines, packed memory layouts, elimination of pointer chasing, and empirical
  Criterion benchmark validation.
- **Strict `no_std` Isolation**: Embedded-first and realtime-ready core
  kernels without mandatory heap allocations or hidden runtime barriers.
- **Pure Orthogonal Separation**: Clean decoupling of policy from mechanism,
  memory layouts from payload codecs, and transport from data structures.

---

## Ecosystem Repositories

| Repository | Status | Description | Primary Role |
| :--- | :---: | :--- | :--- |
| [**`stitch`**](https://github.com/stitch-rs/stitch) | ![Active](https://img.shields.io/badge/status-active-brightgreen) | Canonical Sewing Machine Architecture (SMA) engine, sealed monomorphic execution chains, U-cycle traversal, and CQS capabilities. | Monomorphic Execution Kernel |
| [**`stitch-data`**](https://github.com/stitch-rs/stitch-data) | ![Active](https://img.shields.io/badge/status-active-brightgreen) | High-density data layout & transformation engine: AoS/SoA columnar blocks, SIMD Delta/RLE/BitStream codecs, feature masks, and derive macros. | Data & Transformation Engine |
| [**`stitch-wire`**](https://github.com/stitch-rs/stitch-wire) | ![Planned](https://img.shields.io/badge/status-planned-blue) | Microsecond wire framing, streaming resync parser, hardware Castagnoli CRC32, and UDP/TCP/IPC transport bus. | Framing & Transport Bus |
| [**`stitch-tune`**](https://github.com/stitch-rs/stitch-tune) | ![Planned](https://img.shields.io/badge/status-planned-blue) | Automated dataset profiler, layout optimizer, and code generator for empirical serialization tuning. | Developer Tooling & CLI |

---

## Quickstart: The Stitch Paradigm

### 1. Monomorphic Execution Pipeline (`stitch`)

```rust
use stitch::prelude::*;

let pipeline = Pipeline::on_terminal(RecordTerminal::new())
    .wrap(CrcLayer::new())
    .wrap(TelemetryLayer::new());

let outcome = pipeline.dispatch(&mut blackboard, payload)?;
```

### 2. High-Density Schema & Layouts (`stitch-data`)

```rust
use stitch_data::prelude::*;

#[derive(StitchRecord)]
pub struct SensorReading {
    pub timestamp: u64,
    #[stitch(zigzag)]
    pub delta_temp: i16,
    #[stitch(bits = 4)]
    pub sensor_id: u8,
}
```

---

## Contributing & Community Standards

All repositories under **`stitch-rs`** uphold strict engineering standards:

- All changes go through pull requests targeting `dev` with full CI pass
  (Miri, Clippy with zero warnings, ASan, fuzz testing).
- Codebase artifacts and commits strictly adhere to [Conventional Commits](https://www.conventionalcommits.org/).
- Review the [Contributing Guide](CONTRIBUTING.md) and [Code of Conduct](CODE_OF_CONDUCT.md).

---

## License

All official Stitch ecosystem projects are dual-licensed under **MIT** OR **Apache-2.0**.
