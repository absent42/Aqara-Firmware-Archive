# Aqara Firmware Archive

Community archive of Aqara device firmware, organised so an end user can
find an image by the device's friendly name.

## Layout

```
<Friendly Name>/<model>/<version>/release.json   metadata (md5, size, notes, regions)
<Friendly Name>/<model>/<version>/<original-name>.ota|.bin|.zip   firmware image (when downloaded)
<Friendly Name>/<model>/model.json               model identity (pid, Matter pid, names)
<Friendly Name>/README.md                        per-device summary
```

## Notes

- The model id (e.g. lumi.camera.agl005) is the stable key. Friendly names
  can be renamed and one name may cover several hardware models.
- For a given model and version the binary is identical across regions, so
  region is recorded in release.json rather than duplicated as folders.
- Region here reflects the OTA serving cloud. Some devices are region locked
  at the account or factory-image layer even when the OTA binary matches, so
  an identical image does not guarantee cross-region interchangeability.

See [INDEX.md](INDEX.md) for the A-Z list and [REGIONS.md](REGIONS.md) to browse by region.
