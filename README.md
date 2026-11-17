# Shan Shui firmware releases

Published firmware for Shan Shui e-paper boards. Each board checks the latest stable
release here once a day and installs newer ones itself; over Telegram, `/update` installs
the latest stable release, `/update beta` or `/update alpha` the newest test release, and
`/update v12` release 12 (older ones too). Releases are published by the source
repository's release workflow; nothing here is uploaded by hand.

Releases are numbered `v1`, `v2`, ... across all channels; beta and alpha releases are
marked as pre-releases. The releases `stable`, `beta` and `alpha` are pointers: each holds
only the `release.manifest` of the newest release at that channel or a more stable one.

Each numbered release holds:

| File | What it is |
| --- | --- |
| `release.manifest` | The release number, channel, build ID and files, authenticated with the boards' fleet key. |
| `firmware.enc` | The application image, encrypted and authenticated for Shan Shui boards (AES-256-CTR with an HMAC-SHA256 tag). It cannot be used without a board's key. |
| `earth_maps.bin`, `moon_map.bin` | Map data made from public NASA imagery, unencrypted. Their SHA-256 digests are in the manifest, so boards reject altered copies. |
| `partitions.bin`, `bootloader.bin` | For setting up a new board over USB. |

The daily check only installs a stable release newer than the one running. If a new
release cannot reach GitHub and Telegram on its first start, the board rolls back to the
previous one.
