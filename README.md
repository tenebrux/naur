# naur

> naur, not the aur.

Small Pacman passthrough repository hosted on GitHub Pages. It republishes
validated release packages under a stable Pacman endpoint.

## Usage

Add to `/etc/pacman.conf`:

```ini
[naur]
SigLevel = Optional TrustAll
Server = https://pkgs.tenebrux.com
```

Then:

```bash
sudo pacman -Sy
sudo pacman -S rwr
```

## What's in the repo

| Package | Source | Why it's here |
|---------|--------|---------------|
| `rwr` | github.com/FynxLabs/rwr releases | Stable package endpoint for post-install setup |

Naur does not currently mirror private Tenebrux repositories or build AUR
packages. Dusk, Umbra, and the installer-only helper packages are bundled by
the Tenebrux ISO until they have a public release source or Naur receives a
dedicated read-only release token.

## Updating the repo

```bash
mise install          # install tools
mise run fetch        # download required stable release packages
mise run build        # regenerate repo database (repo-add)
# Or all at once:
mise run update
```

Production publishing is handled by the `Update Repo` GitHub Actions
workflow. Run it manually from the Actions tab when an immediate deployment
is needed; it also runs daily and after release dispatches.

## CI

The `.github/workflows/update.yml` workflow rebuilds and deploys the repo with
GitHub Pages:
- **On schedule** (daily at 06:00 UTC) — catches new releases automatically
- **On repository_dispatch** — available for future release publishers
- **Manually** — via GitHub Actions "Run workflow" button

## Architecture support

- `x86_64` — supported

## License

MIT — see [LICENSE](LICENSE).
