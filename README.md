# goodgrief.dev

The front page of [goodgrief.dev](https://goodgrief.dev): the gg mark and a link to the
[documentation](https://docs.goodgrief.dev). A single static `index.html`, plus the newest gg
release's installers, deployed to GitHub Pages by `.github/workflows/deploy.yml`.

The mark is the gg console's screensaver, ported from `Gg.Console/State/LoadingArt.cs` in
[glyph-guild/gg](https://github.com/glyph-guild/gg): it breathes on a cosine and, while dim, a few
of its characters shimmer.

## The installers

`https://goodgrief.dev/install.sh` and `install.ps1` are byte-for-byte copies of the newest
[gg release](https://github.com/glyph-guild/gg/releases)'s installers. They are **not stored in this
repository**: every deploy downloads them from the release, runs `gh attestation verify` against gg's
release workflow (`publish-cli.yml`), and refuses to publish if either check fails. Each is published
with a `.sha256` beside it, and `install-version.txt` names the release they came from.

The deploy runs on every push to `main`, and every half hour, when it publishes only if the newest
release's installers differ from what is served.

To check a script before running it, wherever it was downloaded from:

```sh
curl -fsSLO https://goodgrief.dev/install.sh
gh attestation verify install.sh --repo glyph-guild/gg
sudo sh install.sh
```
