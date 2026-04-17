# ventd/hardware-profiles

Community-curated database of hardware fingerprint → fan profile mappings, consumed by the [ventd](https://github.com/ventd/ventd) daemon at first boot so a new install on hardware someone has already calibrated skips the 60-second calibration sweep.

## What a profile is

A tuple of:

- **Fingerprint** — DMI board vendor / name / version, Super I/O chip name, PCI subsystem IDs, CPU microcode family. Enough to uniquely identify a motherboard + cooling layout.
- **Channel roles** — which hwmon channels are case fans, CPU fans, pump, GPU fans, AIO fans.
- **Calibration seed** — `start_pwm`, `stop_pwm`, `max_rpm` per channel, pre-measured so new installs skip the sweep.
- **Default curves** — sensible linear curves tuned for the motherboard's thermal envelope.

## How it's used

ventd reads `profiles.yaml` at install time (via `go:embed`) and opportunistically at runtime (opt-in via `hwdb.allow_remote: true`). Fingerprint match on a fresh install → one-click zero-config wizard.

## Contributing

Every entry is curated. No PRs accepted yet — the schema is still in flux while `internal/hwdb` lands in ventd. Once the `ventd` binary has a `ventdctl profile submit` path, that becomes the blessed contribution flow.

## License

GPL-3.0. See [LICENSE](LICENSE).
