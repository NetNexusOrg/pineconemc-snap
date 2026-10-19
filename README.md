# PineconeMC snap

Snap packaging for [ElyPrismLauncher/Launcher](https://github.com/ElyPrismLauncher/Launcher)
(branded as **PineconeMC**).

The snap builds the launcher from source at a fixed upstream tag.

| | |
|---|---|
| Snap name | `pineconemc` |
| Upstream source | `https://github.com/ElyPrismLauncher/Launcher.git` |
| Snap packaging repo | `https://github.com/NetNexusOrg/pineconemc-snap` |
| Version | `11.1.1` (kept in sync with `source-tag`) |
| Base | `core24` + `kde-neon-6` extension (Qt6/KF6 from the KDE content snap) |
| Architectures | `amd64` |
| Confinement | `strict` |
| Grade | `stable` |

## Building

The build requires the source to be a git repository (not a shallow clone),
because `snapcraft remote-build` uploads the project to Launchpad. A git
identity must be configured, otherwise snapcraft cannot create the commit it
ships to the build farm.

```bash
sudo snap install snapcraft --classic

git init
git config user.name "Your Name"
git config user.email "you@example.com"
git add -A
git commit -m "snap: packaging for PineconeMC 11.1.1"

# Build on Launchpad (needs a Launchpad account; public upload)
snapcraft remote-build --build-for amd64 --launchpad-accept-public-upload
```

The finished snap (`pineconemc_11.1.1_amd64.snap`) is downloaded into the
project directory. Interrupted builds can be resumed with
`snapcraft remote-build --recover`.

### Building locally instead

```bash
sudo snap install multipass   # or: sudo snap install lxd
snapcraft --build-for amd64
```

## Installing

```bash
sudo snap install --dangerous pineconemc_11.1.1_amd64.snap
```

`--dangerous` is needed because the snap is not signed by the store. The `home`
interface is auto-connected on classic systems (including for sideloaded snaps),
so no manual connection is required. If it is ever missing, connect it with:

```bash
sudo snap connect pineconemc:home
```

## Verifying

```bash
snap run pineconemc
snap connections pineconemc
snap run --shell pineconemc -c 'ldd $SNAP/usr/bin/elyprismlauncher | grep "not found"'
```

## Publishing to the Snap Store

The snap is built with `grade: stable` and strict confinement, so it can be
uploaded as is. Publishing needs a Snap Store account, which is separate from
the Launchpad account used for remote builds:

```bash
snapcraft login                  # Ubuntu One / snapcraft.io account
snapcraft register pineconemc    # only once, to claim the name
snapcraft upload --release=edge pineconemc_11.1.1_amd64.snap
```

Releasing to `stable` triggers a manual store review:

```bash
snapcraft release pineconemc <revision> stable
```

The icon used in the store listing and in the app grid comes from
`snap/gui/icon.png` (256x256).

## Updating the launcher version

Change `version` and `source-tag` in `snap/snapcraft.yaml` together, then rebuild.

## Runtime layout

| | |
|---|---|
| Command | `usr/bin/elyprismlauncher` |
| Data directory | `$SNAP_USER_COMMON` (i.e. `~/snap/pineconemc/common`) |
| Java runtimes | Java 8, 17 and 21 bundled at `$SNAP/usr/lib/jvm` (detected automatically), plus on-demand downloads |

The launcher detects the snap environment itself (`DesktopServices::isSnap()`)
and stores its data under `$SNAP_USER_COMMON`; no extra environment variables
are required.

Window decorations come from libdecor: the game renders through SDL3 on native
Wayland, where GNOME does not draw server-side decorations, so the GTK plugin of
libdecor (staged in the snap, with the cairo plugin as fallback) draws the title
bar and follows the system GTK theme.

## Credits

This repository contains only the snap packaging; the launcher is built
unmodified from the upstream source. It is not affiliated with or supported by
the PineconeMC developers. All credit for the application goes to:

- **PineconeMC / ElyPrismLauncher** — <https://github.com/ElyPrismLauncher/Launcher>
  (GPL-3.0-only), the launcher that this snap packages.
- **Prism Launcher** — <https://prismlauncher.org>, the upstream project that
  PineconeMC is forked from.
- The icon in `snap/gui/icon.png` is the upstream PineconeMC artwork.
- The bundled Java runtimes are the Ubuntu packages (`openjdk-8/17/21-jre`).

## Reporting issues

- Problems with the **snap** (packaging, missing runtime libraries, confinement):
  <https://github.com/NetNexusOrg/pineconemc-snap/issues>
- Problems with the **launcher or the game** (accounts, instances, mods):
  <https://github.com/ElyPrismLauncher/Launcher/issues>

## License

PineconeMC is licensed under GPL-3.0-only. This packaging lives alongside it
under the same terms.
