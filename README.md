# argus-android

Android and Wear OS clients for Argus: wearable biosignal capture, sleep-cycle smart wake, and an across-the-room phone alarm, built on argus-signal-core.

The watch app records heart rate (with inter-beat intervals) and motion overnight on a Galaxy Watch, picks a light-sleep moment inside a wake window, and wakes you. The phone app rings the final alarm across the room, so turning it off means getting up.

## Status

Scaffolding. Both apps are still Android Studio's templates, set up with the shared application ID. Sensor capture, the wake decision and the alarm come next.

## Modules

| Module | Runs on | Role | State |
| --- | --- | --- | --- |
| `wear` | Galaxy Watch, Wear OS 5 or later | Overnight capture, wake decision, watch alarm | Template |
| `mobile` | Android phone, Android 14 or later | Across-the-room alarm | Template |
| `shared` | Both | Data Layer paths and message models | Planned |

Both apps use the application ID `io.github.maxgabrielsusman.argus`. The Wearable Data Layer only connects a watch app and a phone app that share a package name and signing key, so the two IDs must stay the same. Each module keeps its own namespace (`io.github.maxgabrielsusman.argus.wear` and `io.github.maxgabrielsusman.argus.mobile`).

The signal processing (beat-to-beat HRV, motion, sleep and circadian models) lives in [argus-signal-core](https://github.com/Max-Gabriel-Susman/argus-signal-core), a Rust library the apps will call through UniFFI bindings.

## Build and run

Requires Android Studio Rabbit 2 (2026.2.2) or later.

1. Open this directory in Android Studio and let Gradle sync.
2. Watch app: create a Wear OS virtual device (Tools > Device Manager > Create, category Wear OS, Wear OS Large Round), pick the `wear` run configuration and run it.
3. Phone app: connect a phone with USB debugging on, or create a phone virtual device, then pick the `mobile` run configuration and run it.

Sensor capture needs a real Galaxy Watch, because the Samsung Health Sensor SDK doesn't run on emulators.

## License

Apache-2.0. See [LICENSE](LICENSE).
