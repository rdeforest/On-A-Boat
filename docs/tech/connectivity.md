# Connectivity

## Layered Internet Strategy

| Layer | Purpose | Monthly Cost |
|---|---|---|
| **Starlink** | Primary internet — all situational awareness, work, communication | ~$165 |
| **Iridium** | Emergency backup — guaranteed global comms when Starlink is down | ~$50-150 |
| **Marina WiFi** | Supplementary when docked (save Starlink data if on metered plan) | Usually included |
| **Cellular** | Near-shore backup | Existing phone plan |

## Starlink — Primary Internet

### Technology
- Low-Earth orbit satellite constellation (~550 km altitude, vs 35,785 km for geostationary)
- **Flat-panel phased array antenna** — electronic beam steering, no mechanical movement
- Tracks satellites without moving parts — perfect for a boat that's heeling, pitching, changing heading
- Latency under 30ms (vs 600ms+ for traditional maritime satellite)
- Real-world speeds: 100+ Mbps common in coastal zones

### Plan: Roam Unlimited ($165/month)
- Covers coastal waters within 12 nautical miles
- "In-motion" defined as speeds over 10 mph — most sailboats at hull speed are under this threshold
- Can use Standard dish (cheaper) for most sailing, not just the expensive High Performance dish
- Ocean Mode available for offshore: $2/GB, limited to 5 consecutive days at a time

### Hardware Options
- **Standard dish** (~$300-500): Adequate for most sailboat use (under 10 mph)
- **Flat High Performance dish** (~$2,500): Better in-motion performance, aluminum construction, designed for harsh environments. 3-year warranty, built for 10-year survivability.

### Installation
- Mount on pole, arch, or rail — needs clearest sky view with least obstructions
- Masts and rigging cause some brief micro-outages but generally don't significantly affect service
- Starlink app includes AR tool to find ideal install location
- Power: AC via inverter from DC when needed; ~50-100W consumption
- Additional electrical cost: ~$10-20/month

### What Starlink Enables
- Real-time AIS traffic overlay (every commercial vessel's course and speed)
- Continuous GRIB weather file updates
- Real-time tidal data
- Video calls from anchor
- Remote work capability
- Signal K remote monitoring access
- Asking Claude questions from sea

## Iridium — Emergency Backup

### Status
Iridium is very much a going concern — 66 LEO satellites with true pole-to-pole coverage. Certified for GMDSS (Global Maritime Distress and Safety System) since January 2020.

### Role
Not for internet — max 704 Kbps on best Iridium Certus service (less than 1% of Starlink speed). It's for guaranteed emergency communications when Starlink is down, in any weather, anywhere on Earth.

### Options for Sailboat
- **Iridium GO! exec** (~$1,575): Creates WiFi hotspot from Iridium network. Phone connects for texts, basic data, voice calls. Not fast, but globally reliable.
- **Iridium satellite phone** (handheld): Simpler, voice + SMS only. Ultimate fallback.
- **Iridium Certus terminals**: Higher bandwidth (up to 700 Kbps) but much more expensive hardware and service. Overkill for backup role.

### Recommendation
Iridium GO! exec or basic satellite handset as emergency backup. The ability to call for help from anywhere via a device that works with a tiny omnidirectional antenna regardless of boat orientation is genuine safety equipment, not a luxury.

## Use Cases by Connectivity Layer

| Scenario | Primary | Backup |
|---|---|---|
| At marina | Marina WiFi / Starlink | Cellular |
| Coastal sailing (< 12nm) | Starlink | Cellular / Iridium |
| Offshore day trip | Starlink (Ocean Mode) | Iridium |
| Emergency / Starlink down | Iridium | VHF radio |
| Distress | VHF Ch 16 / DSC | Iridium / EPIRB |
