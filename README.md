# Shan Shui firmware releases

Published firmware for Shan Shui e-paper boards. Each board checks the latest release
here once a day and when asked over Telegram (`/update`), and installs newer releases
itself. Releases are published by the source repository's release workflow; nothing here
is uploaded by hand.

Each release holds:

| File | What it is |
| --- | --- |
| `release.manifest` | The release number, build ID and files, authenticated with the boards' fleet key. |
| `firmware.enc` | The application image, encrypted and authenticated for Shan Shui boards (AES-256-CTR with an HMAC-SHA256 tag). It cannot be used without a board's key. |
| `earth_maps.bin`, `moon_map.bin` | Map data made from public NASA imagery, unencrypted. Their SHA-256 digests are in the manifest, so boards reject altered copies. |
| `partitions.bin`, `bootloader.bin` | For setting up a new board over USB. |

A board only installs a release newer than the one it runs. If a new release cannot reach
GitHub and Telegram on its first start, the board rolls back to the previous one.
