# Firmware Update Submission

Use this PR to add a new firmware image (or a new region/version of an existing
device) to the archive. Fill in the details below and complete the checklist.
Remove this template and write a normal description if your PR is not a firmware
submission (for example a docs or tooling change).

## Device

- Friendly name (no "Aqara" prefix):
- Model id (for example `lumi.camera.agl005` or `aqara.matter.4447_4145`):
- Product id (pid):
- Matter pid (matterPid, leave blank if not a Matter device):

## Firmware

- Version:
- Region(s) served (one or more of: au, cn, eu, kr, ru, us):
- Release date (YYYY-MM-DD, from the build if known):
- File size in bytes:
- MD5:

## Release notes

```
Paste the manufacturer release notes here, if any.
```

## Provenance

Help reviewers confirm this is a genuine, unmodified image.

- How was the firmware obtained (region/account, OTA capture, official tool)?
- Source URL (if it was served from a public endpoint):
- Confirm the image is unmodified from what the device was served:

## Files in this PR

Place the binary and its metadata at the canonical path. The firmware keeps its
original filename from the source URL (which carries the build timestamp and
hash), with its original extension (.ota, .bin or .zip):

```
<Friendly Name>/<model>/<version>/<original-firmware-filename>.ota
<Friendly Name>/<model>/<version>/release.json
<Friendly Name>/<model>/model.json        (only if this is a new model)
```

The `release.json` must contain these fields:

```json
{
  "model": "lumi.camera.agl005",
  "friendlyName": "Camera G100",
  "firmwareVersion": "4.5.45_0004",
  "firmwareMD5": "e4be5f02930a0f3cf0143707da1176d8",
  "fileSize": 25569384,
  "releaseNotes": "Fix known issues",
  "regions": ["us", "eu", "au", "kr"],
  "releaseDate": "2026-05-15"
}
```

A new model also needs `model.json`:

```json
{
  "model": "lumi.camera.agl005",
  "pid": "12300",
  "matterPid": "",
  "friendlyNames": ["Camera G100"]
}
```

## How to compute the MD5

- Windows (PowerShell): `Get-FileHash -Algorithm MD5 path\to\file.bin`
- Linux/macOS: `md5sum path/to/file.bin`

The value must match `firmwareMD5` in `release.json` exactly.

## Checklist

- [ ] Folder path follows `<Friendly Name>/<model>/<version>/`
- [ ] Friendly name folder has no "Aqara" prefix
- [ ] Binary keeps its original filename and extension (.ota, .bin or .zip) from the source URL
- [ ] `release.json` is included with all required fields above
- [ ] `firmwareMD5` matches the committed binary (verified with the command above)
- [ ] `fileSize` matches the binary size in bytes
- [ ] Region codes are from the allowed set (au, cn, eu, kr, ru, us)
- [ ] Binary is committed through Git LFS (it appears as an LFS pointer, not a raw blob)
- [ ] `model.json` is included if this is a new model, with `pid`/`matterPid`
- [ ] Existing firmware files were not modified or deleted
- [ ] If this firmware is identical to a version already in the archive, I have
      noted that in the description rather than overwriting it
