# Proprietary Runtime Notes

This directory is for A9 2018 vendor-specific runtime notes that belong with the proprietary tree rather than the generic Samsung IMS project.

## Security / Lockscreen Related Vendor Pieces

The following proprietary components are relevant when validating lockscreen, credentials, and future SELinux enforcing work:

- `proprietary/vendor/bin/hw/android.hardware.gatekeeper@1.0-service`
- `proprietary/vendor/bin/hw/android.hardware.keymaster@3.0-service`
- `proprietary/vendor/bin/hw/android.hardware.biometrics.fingerprint@2.1-service`
- matching init RC files under `proprietary/vendor/etc/init/`

## Packaging Expectations

The vendor makefile should keep packaging these runtime files correctly, because missing binaries or RC files can surface as:

- lockscreen credentials not persisting
- fingerprint menu or enrollment failures
- keystore/gatekeeper startup failures
- boot stalls while framework waits for HAL-backed services

## Scope Boundary

These notes are intentionally stored in the vendor tree because they are device- and blob-specific. Generic Samsung IMS patch documentation belongs in the separate `samsung-ims-patches` repository.
