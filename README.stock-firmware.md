## Stock firmware partition imports

These firmware blobs were pulled from a rooted running stock Samsung ROM and copied into this vendor tree as reference-packaged firmware.

- Source device: `SM-A9200`
- Source fingerprint: `samsung/a9y18qltezc/a9y18qltechn:10/QP1A.190711.020/A9200ZCS5CVI1:user/release-keys`
- Extraction date: `2026-03-19`
- Extraction method: rooted `adb shell su -c tar ...` followed by `adb pull`

## Imported paths

- `vendor/firmware_mnt/image/*`
  - `a512_zap.*`
  - `cdsp.*`
  - `cdspr.jsn`
- `vendor/firmware-modem/image/*`
  - `adsp.*`
  - `modem.*`
  - `mba.mbn`
  - `qdsp6m.qdb`
  - `adspr.jsn`
  - `adsps.jsn`
  - `adspua.jsn`

## Why these were added

- Live stock boot uses `qcom,kgsl-hyp` with `qcom,firmware-name = a512_zap`.
- The earlier offline repack `vendor.img` did not include the mounted firmware-partition payloads.
- The bring-up logs also showed missing `adsp.mdt` and `cdsp.mdt`, which come from mounted firmware partitions on stock.

## Important note

On stock, these files are normally provided by separate mounted partitions:

- `/vendor/firmware_mnt`
- `/vendor/firmware-modem`
- `/vendor/dsp`

In this tree, the runtime mounts are handled by `init.target.rc` rather than active `fstab.qcom` entries.

So these copies serve two purposes:

- keep the exact stock payload in-tree for comparison and packaging
- make the firmware set auditable while we continue fixing runtime mount and secure-init issues
- provide a `vendor/firmware/a512_zap.*` fallback copy while the canonical runtime source remains `/vendor/firmware_mnt/image/a512_zap.*`

## Verification

Hashes for every imported file are recorded in `stock-firmware-partitions.sha256`.
