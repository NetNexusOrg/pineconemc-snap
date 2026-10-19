# PineconeMC snap

Unofficial snap packaging for
[ElyPrismLauncher/Launcher](https://github.com/ElyPrismLauncher/Launcher)
(branded as **PineconeMC**), published on the Snap Store as **`pineconemc`**:
<https://snapcraft.io/pineconemc>.

The snap builds the launcher unmodified from a fixed upstream tag.

| | |
|---|---|
| Snap name | `pineconemc` |
| Snap Store | <https://snapcraft.io/pineconemc> |
| Upstream source | <https://github.com/ElyPrismLauncher/Launcher> |
| Version | `11.1.1` |
| Architectures | `amd64` |
| Confinement | `strict` |
| License | `GPL-3.0-only` |
| Snap packaging repo | <https://github.com/NetNexusOrg/pineconemc-snap> |

Java runtimes are bundled (Java 8, 17 and 21, detected automatically) and
further ones can be downloaded on demand. Everything the launcher keeps —
instances, mods, worlds, accounts — lives in `~/snap/pineconemc/common`.

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
