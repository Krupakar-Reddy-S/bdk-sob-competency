# bdk-sob-competency

Summer of Bitcoin 2026 competency test for [bitcoindevkit/bdk_wallet#410](https://github.com/bitcoindevkit/bdk_wallet/issues/410) — *Improve CI persistence and MSRV testing, automate issue triage*.

By: Krupakar Reddy S ([@Krupakar-Reddy-S](https://github.com/Krupakar-Reddy-S))
Date: 2026-04-25

## What this repository demonstrates

The umbrella issue's competency-test checklist has five items. Each is exercised here:

| # | Requirement | Where to look |
|---|-------------|---------------|
| 1 | Personal-account GitHub repo | This repo, owner `Krupakar-Reddy-S` |
| 2 | Rust hello-world, properly signed commits | `src/main.rs`; every commit is PGP-signed (ed25519, key `4BDF4CF20371DD45`) and shows the green **Verified** badge in GitHub |
| 3 | GitHub Actions job that builds and checks formatting | [`.github/workflows/ci.yml`](.github/workflows/ci.yml) — two jobs: `Build` (`cargo build --verbose`) and `Format Check` (`cargo fmt --all --check`), runs on every push and pull request |
| 4 | Feature branch with a code change | [`feat/print-bitcoin-greeting`](https://github.com/Krupakar-Reddy-S/bdk-sob-competency/tree/feat/print-bitcoin-greeting) — replaces the stock `Hello, world!` with a Bitcoin-themed greeting that includes a notional block-height value |
| 5 | PR opened from the feature branch | [PR #1](https://github.com/Krupakar-Reddy-S/bdk-sob-competency/pull/1) |

## CI status

CI is wired to run `cargo build` and `cargo fmt --all --check` on every push and pull request. Both jobs were green on the initial CI commit and on the feature-branch PR.

## Notes on the signed-commits setup

- Key type: ed25519 (Curve 25519, ECC sign+encrypt)
- Key ID: `4BDF4CF20371DD45`
- Fingerprint: `555C 2326 3B17 89E0 456D F62D 4BDF 4CF2 0371 DD45`
- Email on key: `krupakarreddysuda0@gmail.com` (matches GitHub-verified email)
- `git config --global commit.gpgsign true` is set so every new commit signs by default
- `gpg --list-secret-keys --keyid-format=long` and `git log --pretty='%G?'` both confirm signing

This pre-empts one of the items the umbrella issue picks up: enforcing signed commits in CI for `bdk_wallet` itself, modeled on [`bdk-floresta`'s `sigs.yml`](https://github.com/luisschwab/bdk-floresta/blob/master/.github/workflows/sigs.yml) and [`bdk-bitcoind-client`'s `commit_signatures.yml`](https://github.com/bitcoindevkit/bdk-bitcoind-client/blob/master/.github/workflows/commit_signatures.yml). My SoB proposal builds on these references.

## Build locally

```bash
cargo fmt --all --check
cargo build
cargo run
```
