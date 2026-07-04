# Aqara Firmware Archive

Community archive of firmware OTA updates for Aqara IoT devices.

To request an Aqara firmware image not currently in the archive, please open a issue using the [firmware request form](https://github.com/absent42/Aqara-Firmware-Archive/issues/new?template=firmware-request.yml).

To contribute a firmware image you have please open a [pull request](https://github.com/absent42/Aqara-Firmware-Archive/pulls).

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

## Flashing

The files under each `<version>/` folder are the same OTA images Aqara's own cloud serves to a device. Most Zigbee and Matter ecosystems let you point their OTA mechanism at a local copy of one of these files instead of fetching it from the vendor, so you can push a specific version.

Always match the exact model id and check the MD5 in `release.json` against the downloaded file before flashing. Flashing the wrong image for a model can brick the device.

### Zigbee2MQTT

1. Download the `.ota`/`.bin` file for your device's model and version.
2. In the OTA menu, pick the device to update, select `custom firmware` as the source.
3. Choose the downloaded file as the source and trigger the update.

Details: https://www.zigbee2mqtt.io/guide/usage/ota_updates.html

### ZHA (Home Assistant)

1. Download the `.ota`/`.bin` file for your device's model and version.
2. In Home Assistant, go to the ZHA integration's configuration and set a local OTA firmware directory (or `zha.ota.zigpy_ota.dir` depending on ZHA version), then place the file in that folder.
3. From the device page in Home Assistant, use the "Update" entity/button to check for and install the firmware.

Details: https://www.home-assistant.io/integrations/zha/#updating-firmware and https://github.com/zigpy/zigpy/wiki/OTA

### Home Assistant Matter integration

Home Assistant's Matter integration talks to a separate Matter Server add-on (formerly `python-matter-server`, now the matter.js-based `matterjs-server`), which normally serves OTA updates published by the manufacturer through the Matter fabric. The Matter Server also supports an OTA provider directory option for serving local, unpublished `.ota` files instead - check the current Matter Server add-on documentation for the exact configuration flag, since this is a low-level option without a dedicated Home Assistant UI. Once an update is available, Home Assistant shows it as a normal `Update` entity on the device.

Details: https://github.com/matter-js/matterjs-server

### Standalone Matter (chip-tool)

1. Download the `.ota` file for your device's model and version.
2. Run the CHIP OTA Provider app (from the connectedhomeip tooling) pointing at the local file, e.g. `chip-ota-provider-app --filepath <file> --discriminator 22`, and commission it onto the same fabric as the target device.
3. Announce the provider to the device with chip-tool, e.g. `chip-tool otasoftwareupdaterequestor announce-ota-provider <provider-node-id> 0 0 0 <target-node-id> 0`.

Details: https://project-chip.github.io/connectedhomeip-doc/guides/software_update.html

## Disclaimer

- Not affiliated with, endorsed by, or supported by Aqara.
- Flashing incorrect firmware may brick a device.
