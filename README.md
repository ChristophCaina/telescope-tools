# Telescope Tools

One simple web app for everything you use in an observing session – a ZWO Seestar, an INDI mount with a camera, more to come – plus a bridge to **Stellarium** and a **live window** with the current view or the growing stack.

```
Stellarium ──Telescope Control :10001/:10002──┐
Browser ─────────────── http :8070 ───────────┤ Astro-Station ──Alpaca :5555──> seestar_alp ──> Seestar
Live window <── snapshots ────────────────────┘               └──INDI :7624──> indiserver ──> mount + camera
```

- **One tab per device**, switch devices on/off per session
- **Tonight**: targets above 30° with time window and culmination, planets and Moon; OpenNGC search
- **GoTo**, arrow keys / D-pad, park, stop all, red-light mode
- **Stellarium** "External software" telescope per device (works where Stellarium's INDI support doesn't, e.g. Ubuntu 24.04 / Mint 22)
- **Live window** that pops up as soon as images arrive, stays on top next to Stellarium
- **Safe by default**: nothing starts on its own. GoTo/moving is refused while the Seestar arm is folded, a running stack only ends after confirmation, a new target cleanly ends the previous one
- **Mount + camera rig**: choose camera and optics, field of view and image scale are computed, rig and location go into every FITS header

Status: early, tested with a Seestar S50 (firmware 9.75) and INDI simulators. The user interface and the detailed docs are German for now; English is planned.

## Quick start (Linux laptop)

Requirements: [seestar_alp](https://github.com/smart-underworld/seestar_alp) for a Seestar, `indi-bin` for INDI devices, Stellarium.

```bash
sudo apt install python3-aiohttp python3-gi python3-gi-cairo gir1.2-gtk-3.0 indi-bin stellarium
git clone https://github.com/ChristophCaina/telescope-tools ~/Astro/telescope-tools
bash ~/Astro/telescope-tools/field/install-desktop.sh
```

Then double-click **"Astro-Session starten"** on the desktop and open `http://localhost:8070`.

Try it without hardware: `python3 tools/fake_seestar.py --offset 10000` starts a practice Seestar (see [docs/de/station.md](docs/de/station.md#trockenlauf-ohne-seestar)).

## Documentation (German)

- [Astro-Station](docs/de/station.md) – devices, Stellarium, live window, API
- [Feld-Laptop](docs/de/feld-laptop.md) – services, desktop launcher, location from GPS or the Seestar

## Optional

Automatic stacking with Siril, a web gallery, Immich and Home Assistant integration live in [seestar-astro-pipeline](https://github.com/ChristophCaina/seestar-astro-pipeline). Telescope Tools stores captures with the same file names, so the pipeline can pick them up – nothing here depends on it.

## Roadmap

- LX200 bridge for Stellarium Mobile / SkySafari (tablet, phone)
- ASCOM Alpaca device adapter
- English UI and docs, one-step install, live window for Windows/macOS
