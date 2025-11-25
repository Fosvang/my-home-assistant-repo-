# Home Assistant + LoRaWAN Repo

Formål
------
Centraliseret konfiguration, versionering og CI for Home Assistant-projektet med LoRaWAN-enheder.

Indhold (kort)
---------------
- `homeassistant/` - alle Home Assistant YAML-filer og packages
- `lorawan/` - enhedsbeskrivelser (EUI), templates og eksempler
- `docs/` - projekt-dokumentation (MkDocs eller ren Markdown)
- `.github/workflows/` - CI / autoformat / PR-skabeloner
- `tools/` - hjælpe-scripts (fx parse_hex_payload.py)
---------------
1. Clone repo:
   ```bash
   git clone git@github.com:fosvang/ my-home-assistant-repo.git
   cd homeassistant

