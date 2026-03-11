# Electrical & Power Systems

## Charging Hierarchy

1. **Shore power** → battery charger (primary when at dock)
2. **Engine alternator** (primary when motoring/sailing)
3. **Solar panels** (continuous trickle; handles most daytime loads at anchor)
4. **Wind generator** (optional; noisy, most marina liveaboards find solar sufficient)

### Alternator Upgrade
Stock marine diesel alternators are modest (50-80 amps) — inadequate for modern liveaboard loads. Upgrade path:
- High-output marine alternator: 100-150 amps
- External smart voltage regulator (stock internal regulators are primitive)
- Proper charge profiles for battery chemistry

## Battery Technology

### Lithium Iron Phosphate (LiFePO4) — RECOMMENDED
- 3x upfront cost vs lead-acid
- Usable to 80-90% depth of discharge (vs 50% for lead-acid)
- 1/3 the weight
- 10+ year lifespan (vs 3-5 years lead-acid)
- Charges much faster
- Total cost of ownership over a decade actually favors lithium
- Built-in BMS monitors cell voltages, temperature, state of health

### Lead-Acid (AGM or Flooded)
- Cheap upfront
- Heavy
- 50% max discharge without damage
- 3-5 year lifespan
- Well-understood technology

### Target Bank Size
For the planned electrical load (Starlink, chartplotter, AIS, radar, autopilot, refrigeration, lights, devices):
- **400-600 Ah lithium** (equivalent to 800-1200 Ah lead-acid)
- Combined with **300-400W solar panels**
- Provides several days of autonomy away from shore power

## Decoupling Architecture

### Design Principle
No maintenance operation on any single component should cascade into user-visible impact. Same as clinic migration work — fallback/fallforward, graceful degradation.

### Battery Bank Design
Build house bank as **two independent sub-banks**, each capable of running essential loads alone:

```
Sub-Bank A ←→ Battery Combiner/Parallel Switch ←→ Sub-Bank B
                         ↓
                   House Loads
```

- Normal operation: combined as one large bank
- Maintenance mode: open combiner, remaining sub-bank carries load at reduced capacity
- Monitoring system adjusts alerts and capacity estimates based on current configuration
- Hot-spare architecture

### Charging Source Distribution
- Solar split across both sub-banks (or smart distribution)
- Alternator charges through smart splitter to both banks
- Shore power inverter/charger addresses both banks
- **No charging source hard-wired to only one bank** — taking a bank offline must not remove a charging pathway

### Start Battery
- Dedicated, separate from house banks
- Battery selector switch allows emergency use of house bank for starting

### Critical Systems Power
- NMEA 2000 backbone: own protected power supply (small dedicated battery or most-protected circuit)
- Raspberry Pi monitoring: automatic transfer switch or diode-isolated feed from both sub-banks
- Monitoring infrastructure = last thing to lose power (like monitoring servers on best UPS in data center)

### Circuit Design
- Both Pis on house battery bank with dedicated circuit (not shore power alone)
- Monitoring continues during marina power outage
- Total Pi power consumption: ~10-15W

## Solar Panel Mounting
- Stern arch, bimini frame, or rail-mounted
- 300-400W target
- Consider shading from boom, rigging
- MPPT charge controller (not PWM) for efficiency

## Shore Power Monitoring
- Voltage, frequency, current draw monitoring
- Marina power quality is notoriously inconsistent
- Low voltage from long dock runs or overloaded pedestals damages equipment
- Alert when shore power is out of spec

## Victron Ecosystem

Victron Energy components are designed for exactly this kind of integrated system:
- Battery monitors
- Charge controllers (MPPT solar)
- Inverter/chargers
- All communicate on VE.Bus and VE.Direct
- **Cerbo GX**: aggregates all Victron data, serves VRM web dashboard, bridges to NMEA 2000
- Built-in Signal K interface
- Single dashboard: state of charge, charge/discharge rates, solar production, shore power status, time remaining on battery

## Power Budget Estimation

| Load | Watts | Hours/Day | Wh/Day |
|---|---|---|---|
| Refrigeration | 50 | 12 (cycling) | 600 |
| Starlink | 50-100 | 24 | 1,200-2,400 |
| LED lighting | 20 | 6 | 120 |
| Chartplotter/AIS | 25 | 12 | 300 |
| Phones/laptops | 30 | 8 | 240 |
| Instruments (misc) | 15 | 24 | 360 |
| Raspberry Pis | 15 | 24 | 360 |
| **Total** | | | **~3,200-4,400** |

At 12V: ~270-370 Ah/day. A 600Ah lithium bank provides 1.5-2 days autonomy without any charging. With 300-400W solar producing ~1,200-1,600 Wh/day in San Diego sun, you extend that significantly.
