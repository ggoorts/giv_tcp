# Local GivTCP compatibility candidate

Version3.6.9-reserve.1 uses the pinned official3.6.9 image and replaces only GivTCP/write.py. The image checks the official source checksum before replacement and the exact patched checksum afterwards.

The existing two fixes are retained: three-phase Battery Power Cutoff writes HR1078, and AC percentage requests of0 are mapped to the supported1% minimum. Valid1–100% requests and failure handling retain the existing paths.1% is not a physical0W stop.

Official Lite mode, security defaults, dependency pins and recovery behavior are unchanged. Lite mode remains off by default. Enabling it reduces active stack/module reads and changes derived SOC kWh; verify Predbat's inverter SOC% binding and live operation before accepting it. Percentage bindings,11kW limits and6% reserve floor remain installation settings.

CI runs captured-inverter regressions for direct, REST and MQTT controls and released Lite behavior. It then builds an arm64 image and runs those regressions inside that exact image before publishing it. The upstream Linux/Windows full-suite coverage workflow also runs. Mocks and CI do not establish physical hold or EV recovery.

This is a review candidate. Installation and Lite enablement are separate decisions. Keep only one GivTCP app active. The add-on uses the official homeassistant_config mapping at/config and retains ingress-only8099 defaults. Do not enable LAN Access merely for diagnostics.

Previous image3.6.8-reserve.2 is retained for rollback; review new3.6.9 settings compatibility before reverting. No Home Assistant automation or control mapping is added by this overlay.
