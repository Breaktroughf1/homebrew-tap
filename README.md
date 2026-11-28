# Breaktroughf1 Homebrew tap

Homebrew formulae for [Breaktrough](https://breaktroughf1.com) tools.

```sh
brew install breaktroughf1/tap/lockward
brew install breaktroughf1/tap/wardmap
brew install breaktroughf1/tap/dpdpward
brew install breaktroughf1/tap/peerward
brew install breaktroughf1/tap/appward
brew install breaktroughf1/tap/niyam
brew install breaktroughf1/tap/lineward
brew install breaktroughf1/tap/pramaan
```

With Homebrew 6 or later, installing by the fully qualified name trusts only that formula, not the whole tap ([tap trust](https://docs.brew.sh/Tap-Trust)); no other step is needed. If you tap the repository first, trust just the formula you want, for example `brew trust --formula breaktroughf1/tap/wardmap`.

| Formula | Description |
|---|---|
| [`lockward`](https://github.com/Breaktroughf1/lockward) | Lockfile and policy gate for AI agent skills, MCP servers, hooks and rules |
| [`wardmap`](https://github.com/Breaktroughf1/wardmap) | Map which secrets and cloud roles one compromised CI credential can reach |
| [`dpdpward`](https://github.com/Breaktroughf1/dpdpward) | Map personal data in code for India's DPDP Act: data map, ROPA, safeguards |
| [`peerward`](https://github.com/Breaktroughf1/peerward) | Sign, verify, audit and pin A2A Agent Cards; fail CI when a peer drifts |
| [`appward`](https://github.com/Breaktroughf1/appward) | Find keys and backends shipped in web, Android and iOS apps and their reach |
| [`niyam`](https://github.com/Breaktroughf1/niyam) | CERT-In and SEBI CSCRF evidence scanner for cloud, hosts and repositories |
| [`lineward`](https://github.com/Breaktroughf1/lineward) | Find AI-assisted lines in a pull request and enforce human review on them |
| [`pramaan`](https://github.com/Breaktroughf1/pramaan) | Second-factor verifier for Indian payment apps: attested device binding |

## How the formula is updated

`.github/workflows/update.yml` runs every three hours (and on demand). For each formula it runs `bin/update-formula.sh <formula>`, which:

1. finds the tool's latest release (releases without a signed `checksums.txt` are skipped and the formula is left unchanged);
2. downloads its `checksums.txt` and verifies the Sigstore signature with `cosign verify-blob`, requiring the certificate identity `https://github.com/Breaktroughf1/<tool>/.github/workflows/release.yml@refs/tags/<tag>`;
3. writes `Formula/<tool>.rb` using the SHA-256 values from that signed file.

Each new formula is installed and tested with Homebrew before it is pushed, and a failure for one tool does not hold back the others. No tokens or secrets are stored anywhere: the job uses its own short-lived `GITHUB_TOKEN`. `test.yml` installs every formula on macOS and Linux (Intel and ARM) weekly and on every change.

To package a specific release by hand: Actions → update → Run workflow → pick the formula and enter the tag `vX.Y.Z`.

## Licence

The formulae are Apache-2.0, like the software they install.
