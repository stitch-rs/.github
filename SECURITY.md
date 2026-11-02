# Security Policy

## Supported Versions

We provide security fixes and maintenance updates for active production
versions of our core crates:

| Project | Active Release Branch | Supported |
| :--- | :--- | :---: |
| `stitch` | `main` | :white_check_mark: |
| `stitch-data` | `main` | :white_check_mark: |
| `stitch-wire` | `main` | :white_check_mark: |

---

## Reporting a Vulnerability

The **stitch-rs** team takes memory safety, cryptographic integrity, and
denial-of-service vulnerabilities with utmost seriousness.

If you believe you have found a security vulnerability in any repository
within the `stitch-rs` organization:

1. **Do not open a public GitHub issue.** Public disclosure exposes
   production systems before a remedy can be deployed.
2. Submit a confidential report via GitHub Security Advisories:
   - Navigate to the affected repository's **Security** tab.
   - Click **Report a vulnerability**.
3. Alternatively, report the issue directly to the organization security
   maintainers.

### What to Include in Your Report

To help us triage and remediate the issue rapidly, please provide:

- A clear description of the vulnerability and its potential impact
  (e.g. integer overflow, out-of-bounds read/write, parser stall / DoS,
  undefined behavior under Miri).
- Exact version, commit hash, and compiler toolchain where the issue was
  reproduced.
- A minimal reproducible test case, fuzz artifact, or script demonstrating
  the exploit.
- Any proposed remediations or patches.

---

## Our Commitment

- We will acknowledge receipt of your vulnerability report within **48 hours**.
- We will provide an initial assessment and timeline for remediation.
- Once a fix is verified, we will release patched versions and publish a
  coordinated security advisory crediting your discovery.
