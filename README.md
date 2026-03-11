# On-A-Boat

Documentation and planning for transitioning to liveaboard life on a sailing vessel in Southern California.

## Project Status

**Phase: Research & Planning**

- [ ] Confirm employment stability (Mars hire expected soon)
- [ ] Complete ASA sailing certifications (101 → 106)
- [ ] Join sailing club (Harbor Sailboats — pending location confirmation)
- [ ] Get on marina waitlists
- [ ] Begin boat search
- [ ] Marine survey(s)
- [ ] Purchase boat with transferable slip + liveaboard permission
- [ ] Move aboard
- [ ] Modernization and automation buildout

## Budget Summary

| Category | Amount |
|---|---|
| Boat purchase | $20,000 |
| Repairs & upgrades | $20,000 |
| Emergency reserve | $60,000 |
| **Total** | **$100,000** |

Target monthly TCO: **under $2,500**

## Documentation

### Planning & Finance
- [Budget & Financial Analysis](docs/budget-and-financials.md) — TCO breakdown, monthly cost modeling, financial comparison to renting
- [Marina & Slip Strategy](docs/marina-and-slip-strategy.md) — San Diego marina landscape, waitlists, liveaboard permits, slip acquisition tactics

### Boat Selection
- [Boat Selection Guide](docs/boat-selection.md) — Target size, brands, decades, hull types, what to prioritize
- [Marine Survey Guide](docs/marine-survey-guide.md) — SAMS/NAMS certifications, two-survey strategy, what surveyors look for
- [Seaworthiness & Heavy Weather](docs/seaworthiness-and-heavy-weather.md) — Hull design, stability, what makes a boat survive rough seas

### Systems & Technical
- [Propulsion](docs/propulsion.md) — Impellers vs propellers, folding props, diesel reliability, backup propulsion
- [Electrical & Power Systems](docs/electrical-and-power.md) — Battery banks, charging hierarchy, solar, lithium vs lead-acid, decoupling architecture
- [Monitoring & Automation](docs/monitoring-and-automation.md) — NMEA 2000, Signal K, Raspberry Pi, predictive maintenance
- [Connectivity](docs/connectivity.md) — Starlink, Iridium, layered internet strategy
- [Ground Tackle & Anchoring](docs/ground-tackle.md) — Windlass, chain counter, anchor drag alarms, hull protection

### Safety & Maintenance
- [Safety & Redundancy](docs/safety-and-redundancy.md) — Bilge pumps, fire extinguishers, defense-in-depth philosophy
- [Maintenance Guide](docs/maintenance.md) — Annual rhythm, engine care, bottom paint, rigging, systems overview

### Education
- [Sailing Education Plan](docs/sailing-education.md) — ASA course progression, school recommendations, timeline

## Design Principles

1. **Redundancy everywhere** — Every critical system has a failover. No single point of failure should be catastrophic.
2. **Monitoring compensates for memory** — Automation and alerting systems address ADD/out-of-sight-out-of-mind tendencies.
3. **Buy for who you are, not who you plan to be** — The boat should survive spontaneous decisions and squirrel-brain moments.
4. **Moorage first** — Never buy a boat without a confirmed slip. Learned the hard way.
5. **The $60k doesn't exist until the emergency happens** — Emergency reserve must not influence purchase decisions.

## License

[MIT](LICENSE)
