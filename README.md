# naur

> naur, not the aur.

Pacman repository for tenebrux/Tenebrux packages, hosted on GitHub Pages.
Serves pre-built packages so installs and updates never depend on the AUR at
install time or a single third-party server.

## Usage

Add to `/etc/pacman.conf`:

```ini
[naur]
SigLevel = Optional TrustAll
Server = https://tenebrux.github.io/naur/$arch/
```

Then:

```bash
sudo pacman -Sy
sudo pacman -S dusk umbra ember rwr nody-greeter shikai-theme
```

## What's in the repo

| Package | Source | Why it's here |
|---------|--------|---------------|
| `dusk` | github.com/tenebrux/dusk releases | Panel — no AUR package |
| `umbra` | github.com/tenebrux/umbra releases | Installer — no AUR package |
| `ember` | github.com/tenebrux/ember releases | Clipboard/notifications — no AUR package |
| `rwr` | github.com/FynxLabs/rwr releases | Config management — no AUR package |
| `shikai-theme` | AUR (rebuilt) | Greeter theme — pre-built so installs don't need yay/AUR at install time |

> **xlibre** packages are NOT mirrored here — they live in their own repo at
> `x11libre.net/repo/arch_based/`. Tenebrux's pacman.conf points directly at
> `[xlibre]` for X server packages.
>
> **nody-greeter** is too large (100MB+) for git/GitHub Pages. It gets built
> into the Tenebrux ISO's local `[tenebrux-aur]` repo at ISO build time instead.

## Updating the repo

```bash
mise install          # install tools
mise run fetch        # download tenebrux release packages
mise run fetch-aur    # build AUR packages (nody-greeter, shikai-theme)
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
- **On repository_dispatch** — triggered by dusk/umbra/ember release workflows
- **Manually** — via GitHub Actions "Run workflow" button

## Architecture support

- `x86_64` — primary, fully supported
- `aarch64` — scaffolded; packages added as arm64 releases become available

## License

MIT — see [LICENSE](LICENSE).
