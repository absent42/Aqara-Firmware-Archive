# Aqara Firmware Archive

Community archive of firmware OTA updates for Aqara IoT devices.

## Layout

```
<Friendly Name>/<model>/<version>/release.json   metadata (md5, size, notes, regions)
<Friendly Name>/<model>/<version>/<original-name>.ota|.bin|.zip   firmware image (when downloaded)
<Friendly Name>/<model>/model.json               model identity (pid, Matter pid, names)
<Friendly Name>/README.md                        per-device summary
```

## Notes

- The model id (e.g. lumi.camera.agl005) is the reliable identifier, one device name may cover several hardware models.
- For a given model and version the binary can be identical across regions, so region is recorded in release.json rather than duplicated as folders. Identical firmware version are established through MD5 file hashes.
- Region here reflects the OTA serving cloud. Some devices are region locked at the account or factory-image layer even when the OTA binary matches, so an identical image does not guarantee cross-region interchangeability.

See [INDEX.md](INDEX.md) for the A-Z list and [REGIONS.md](REGIONS.md) to browse by region.

## Disclaimer

- Not affiliated with, endorsed by, or supported by Aqara.
- Flashing incorrect firmware may brick a device.