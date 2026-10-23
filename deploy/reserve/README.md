# Local GivTCP compatibility candidate

The image is based on pinned official GivTCP3.6.8 and overlays only write.py. The Dockerfile checks both the normalized official writer checksum and the exact candidate checksum.

Candidate3.6.8-reserve.2 retains the three-phase HR1078 runtime-reserve correction and adds the existing AC minimum handling to setChargeRateAC and setDischargeRateAC:0 maps to1%, valid1–100% stay unchanged, and invalid bounds remain rejected. Accepted percentage and computed-watt cache updates use the same minimum. Predbat bindings and maximum-rate configuration are outside this change.

The AC register cannot express a true0W stop.1% is only the lowest supported rate; actual hold and recovery require separate physical observations. No additional Home Assistant automation is part of this candidate.

The branch workflow runs capture-backed MQTT/REST/direct percentage regressions and the existing reserve tests before building the arm64 image. Rollback uses the retained3.6.8-reserve.1 tag; settings are not migrated by this overlay.
