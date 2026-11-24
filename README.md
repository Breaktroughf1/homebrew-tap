# Breaktroughf1 Homebrew tap

Homebrew formulae for [Breaktrough](https://breaktroughf1.com) tools.

```sh
brew install breaktroughf1/tap/lockward
```

With Homebrew 6 or later, installing by this fully qualified name trusts only the `lockward` formula, not the whole tap ([tap trust](https://docs.brew.sh/Tap-Trust)); no other step is needed. If you tap the repository first, trust just this formula with `brew trust --formula breaktroughf1/tap/lockward`.

| Formula | Description |
|---|---|
| [`lockward`](https://github.com/Breaktroughf1/lockward) | Lockfile and policy gate for AI agent skills, MCP servers, hooks and rules |

## How the formula is updated

`.github/workflows/update.yml` runs every three hours (and on demand). It runs `bin/update-formula.sh`, which:

1. finds the latest Lockward release;
2. downloads its `checksums.txt` and verifies the Sigstore signature with `cosign verify-blob`, requiring the certificate identity `https://github.com/Breaktroughf1/lockward/.github/workflows/release.yml@refs/tags/<tag>`;
3. writes `Formula/lockward.rb` using the SHA-256 values from that signed file.

The new formula is installed and tested with Homebrew before it is pushed. No tokens or secrets are stored anywhere: the job uses its own short-lived `GITHUB_TOKEN`. `test.yml` installs the formula on macOS and Linux (Intel and ARM) weekly and on every change.

To package a specific release by hand: Actions → update → Run workflow → tag `vX.Y.Z`.

## Licence

The formulae are Apache-2.0, like the software they install.
