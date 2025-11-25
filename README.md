# My Home Assistant + LoRaWAN repo

Formål: centraliseret konfiguration, versionering og CI for Home Assistant og LoRaWAN-enheder.

Struktur:
- `homeassistant/` - hovedkonfiguration (YAML)
- `lorawan/devices/` - per-enhed YAML beskrivelser og EUI
- `docs/` - projekt-dokumentation

CI:
- `ci.yml` validerer YAML og kører tests på PR.

Se `docs/architecture.md` for arkitektur-oversigt.
