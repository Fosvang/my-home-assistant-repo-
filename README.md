# Home Assistant + LoRaWAN Repo

Formål (Purpose)
----------------
Dette repository centraliserer konfiguration, versionering og CI for et Home Assistant-projekt der bruger LoRaWAN-enheder.
This repository centralizes configuration, versioning and CI for a Home Assistant project using LoRaWAN devices.

Indholdsoversigt (At a glance)
------------------------------
- `homeassistant/` – Home Assistant YAML-konfigurationer og packages (core config)
- `lorawan/` – Enhedsbeskrivelser (EUI), payload-templates og eksempler
- `docs/` – Projekt-dokumentation (MkDocs eller ren Markdown)
- `.github/workflows/` – CI, autoformat og PR-skabeloner
- `tools/` – Hjælpe-scripts (fx parse_hex_payload.py)
- `.gitignore`, `README.md`, (evt.) `LICENSE`, `secrets.example.yaml`

Quick links
-----------
- Konfigmappe: homeassistant/
- LoRaWAN-eksempler: lorawan/
- Dokumentation: docs/

Repositorystruktur (Detailed)
-----------------------------
- homeassistant/
  - configuration.yaml (entry point)
  - packages/ (opdelte funktioner, automatiseringer, sensorer)
  - blueprints/ (genbrugelige automation-blueprints)
  - secrets.yaml (skal ikke committes — se nedenfor)
- lorawan/
  - devices.yaml (EUI, device profiles, noter)
  - templates/ (payload-dekodere, eksempler)
  - examples/ (TTN/ChirpStack integration snippets)
- docs/
  - mkdocs.yml eller README.md med installations- og udviklerguide
- tools/
  - scripts til at parse og teste payloads, dump/restore værktøjer osv.

Hurtigstart (Quick start)
-------------------------
1. Clone repo
   - SSH:
     ```bash
     git clone git@github.com:Fosvang/my-home-assistant-repo-.git
     ```
   - HTTPS:
     ```bash
     git clone https://github.com/Fosvang/my-home-assistant-repo-.git
     ```
2. Gennemgå konfiguration
   ```bash
   cd my-home-assistant-repo-
   ls -la homeassistant
   ```
3. Test konfiguration (to muligheder)
   - Brug Home Assistant UI: Configuration → Server Controls → Check Configuration
   - Eller lokal CLI (kræver Home Assistant installeret):
     ```bash
     # Eksempel: kræver 'hass' CLI tilgængelig
     hass --script check_config -c ./homeassistant
     ```
   - Eller kør container med din config (eksempel):
     ```bash
     docker run --rm -v "$(pwd)/homeassistant:/config" ghcr.io/home-assistant/home-assistant:stable
     ```
4. Tilføj eller opdater LoRaWAN-devices
   - Se `lorawan/devices.yaml` for format og eksempler.
   - Hold device-EUI og nøgler ude af repository — brug `secrets.yaml` eller din TTN/ChirpStack-projektkonfiguration.

LoRaWAN — eksempelsnippet
-------------------------
Eksempel på, hvordan en device-entry i `lorawan/devices.yaml` kan se ud:
```yaml
- name: sensortag-livingroom
  dev_eui: "00-80-00-00-00-01-02-03"
  description: "Temperatur & fugt, LoRaWAN - testrapport"
  payload_template: "lorawan/templates/sensortag_v1.json"
  adr: true
```
Til payload-dekodning gemmes skabeloner i `lorawan/templates/` og kan genbruges i integrationen (TTN / ChirpStack).

Sikkerhed og hemmeligheder (Secrets)
-----------------------------------

CI / Formattering
-----------------
- Repo'et forventes at have GitHub Actions i `.github/workflows/` til:
  - YAML lint / Home Assistant config check
  - Autoformat (prettier / yamllint)
  - Tests for tools scripts (fx pytest for Python-scripts)
- Se workflow-filerne for detaljer om krav og triggers.

Contributing
------------
- Branch-navngivning: feature/<kort-beskrivelse> eller fix/<kort-beskrivelse>
- Lav PR mod `main` (eller `master`) med tydelig titel og beskrivelse.
- Tilføj CHANGELOG-entry ved større ændringer.
- Kør lokale checks før PR:
  - YAML lint
  - Config check (se afsnit Hurtigstart)

Eksempler på nyttige kommandoer
-------------------------------
- Liste filer:
  ```bash
  tree -L 2
  ```
- Kør et hjælpe-script:
  ```bash
  python3 tools/parse_hex_payload.py tests/sample_payloads.json
  ```

License
-------
MIT.

Kontakt / Forfatter
-------------------
Repo vedligeholdes af Fosvang — opret en Issue eller PR for spørgsmål, rettelser eller forslag.

TODO / Fremtidige forbedringer
------------------------------
- Dokumentation af deployment (Docker Compose, Supervisor, eller Home Assistant OS)
- Flere eksempler til TTN og ChirpStack
- Automatiske tests for payload-dekodere


