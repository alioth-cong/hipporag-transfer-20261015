# HippoRAG archive transfer

Public transfer of the three original archives. Each part is at most 512 MiB (536,870,912 bytes). Parts preserve the original bytes and are concatenated in numeric order.

## Download on a Linux server

Requires Bash, curl, sha256sum, awk, and about 33 GB of free disk space for parts and reconstructed archives. No GitHub login is needed after the release is published.

```bash
curl -fL --retry 8 -o download-hipporag.sh https://github.com/alioth-cong/hipporag-transfer-20261015/releases/download/archives-20261015/download.sh
bash download-hipporag.sh
```

The script supports resuming incomplete downloads, verifies each part, reconstructs the three archives in `hipporag-transfer/`, and verifies the original SHA-256 hashes. Keep the parts until verification succeeds; rerun the same command after a network interruption. Archives are not extracted automatically.

| Archive | Original bytes | Parts |
|---|---:|---:|
| `hipporag-checkout.tgz` | 5,351,944,547 | 10 |
| `outputs-speedppr.tgz` | 3,984,064,553 | 8 |
| `fixtures.tgz` | 6,549,129,671 | 13 |

## Manual reassembly

Download all 31 parts and both SHA256SUMS files from [the release](https://github.com/alioth-cong/hipporag-transfer-20261015/releases/tag/archives-20261015). In the download directory:

```bash
sha256sum -c SHA256SUMS.parts
cat hipporag-checkout.tgz.part[0-9][0-9][0-9][0-9] > hipporag-checkout.tgz
cat outputs-speedppr.tgz.part[0-9][0-9][0-9][0-9] > outputs-speedppr.tgz
cat fixtures.tgz.part[0-9][0-9][0-9][0-9] > fixtures.tgz
sha256sum -c SHA256SUMS.originals
```

See `manifest.json` in the release for the size and hash of every part and original archive.
