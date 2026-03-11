# Monitoring & Automation

## Design Philosophy

> "Out of sight, out of mind" is the enemy. The monitoring system is external memory and vigilance supplement. The boat watches herself and tells you when she needs attention.

This is predictive maintenance — the same thing SysOps does for infrastructure, applied to floating infrastructure that occasionally tries to sink.

## Architecture Overview

```
┌─────────────────────────────────────────────────┐
│                NMEA 2000 Backbone                │
│  (CAN bus — engine, GPS, depth, wind, tanks,     │
│   autopilot, AIS, chartplotter)                  │
└──────────────┬──────────────────────────────────┘
               │
         Actisense NGT-1
         (USB-to-NMEA gateway, ~$200-250)
               │
┌──────────────┴──────────────────────────────────┐
│          Primary Raspberry Pi                    │
│  ┌─────────────────────────────────────────┐    │
│  │         Signal K Server                  │    │
│  │  - Aggregates all NMEA 2000 data        │    │
│  │  - Plugin architecture                   │    │
│  │  - Web dashboard                         │    │
│  │  - Data logging                          │    │
│  │  - Alert rules → phone notifications    │    │
│  └─────────────────────────────────────────┘    │
│                                                  │
│  GPIO/I2C Sensors:                              │
│  - Bilge water level                            │
│  - Compartment temp & humidity (multiple)       │
│  - Barometric pressure                          │
│  - Racor vacuum gauge (analog transducer)       │
│  - Fuel filter bowl camera (optional)           │
└──────────────────────────────────────────────────┘
               │
          Starlink WiFi
               │
┌──────────────┴────────────────┐
│  Victron Cerbo GX             │
│  - VE.Bus / VE.Direct         │
│  - Battery state               │
│  - Solar production            │
│  - Shore power status          │
│  - Bridges to NMEA 2000       │
│  - Built-in Signal K iface    │
│  - VRM remote dashboard       │
└───────────────────────────────┘

┌──────────────────────────────────────────────────┐
│          Secondary Raspberry Pi (Failover)        │
│  - Mirrors critical monitoring:                   │
│    bilge level, battery state, shore power        │
│  - Independent alert pathway                      │
│  - Catches failures of primary Pi or its PSU     │
│  - On separate circuit / diode-isolated power    │
└──────────────────────────────────────────────────┘
```

## Signal K

Open-source marine data server purpose-built for Raspberry Pi:
- Aggregates NMEA 2000 data into unified data model
- Web-based dashboard accessible from any device on boat WiFi (or remotely via Starlink)
- Plugin ecosystem for anchor watch, engine monitoring, Home Assistant integration, etc.
- Data logging for trend analysis
- Active community of SysOps/developer types building boat monitoring systems
- **Join the Signal K Discord**

## Sensors & Monitoring

### Engine Monitoring (via NMEA 2000)
- RPM, coolant temperature, oil pressure, fuel flow
- Engine hour meter (drives time-based maintenance alerts)
- Trending: gradual temperature increase at same RPM → fouling heat exchanger (caught weeks before it's a problem)

### Fuel Quality Monitoring

| Method | Cost | What It Tells You |
|---|---|---|
| Racor vacuum gauge | ~$30 | Filter clogging rate — #1 early warning of contamination |
| Racor transparent bowl | Included | Visual water/sediment accumulation |
| Bowl camera → Pi | ~$20 | Remote visual inspection |
| Inline fuel quality sensor (Parker Hannifin, etc.) | $500-$1,500 | Continuous water content and particulate measurement |
| Fuel polishing system pressure | Varies | Filter condition in polishing circuit |

Layered approach: biocide treatment (prevention) + fuel polishing (active maintenance) + Racor vacuum gauge (real-time) + bowl inspection (visual) + inline sensors (trending)

### Battery Monitoring (via Victron + NMEA 2000)
- Individual cell voltages, pack voltage
- Current in/out, state of charge
- Temperature
- State of health (degradation trending)
- Charge/discharge history
- Estimated time remaining on battery
- Alerts: low SOC, charging failures, unusual current draw

### Bilge Monitoring
- Float sensor or ultrasonic level sensor on Pi GPIO
- Log pump cycles and water level trends
- **Key insight**: If pump cycles more frequently this month than last month, something is changing
- Unusual current draw on bilge pump circuit → potential leak detection
- Alarm on unexpected water level

### Tank Levels (via NMEA 2000)
- Fresh water, fuel, holding tank (sewage)
- Capacitive tank senders (no moving parts, reliable)
- Know holding tank is at 80% before leaving dock, not at 100% while anchored in no-discharge zone

### Environmental
- Temperature sensors: engine room, bilge, cabin, lazarette
  - Rising engine compartment temp when engine not running → possible electrical fault
  - High humidity in closed compartment → mold incoming
- Barometric pressure trending
  - Rapidly dropping barometer = incoming bad weather
  - Alert on threshold rate of change

### Shore Power
- Voltage, frequency, current draw
- Alert when out of spec (protects charger and electronics)

### Anchor Watch (Signal K plugin)
- Chain counter sensor counts links passing gypsy
- Combined with GPS and depth → calculated swing radius
- Alert if GPS position drifts beyond swing radius
- Anchor drag at 3 AM → phone buzzes before you're on the rocks

## Maintenance Scheduling System

### Data Model
Every maintainable item has:
- Replacement interval (time-based OR usage-based)
- Last-serviced date
- Engine hours at last service (for hour-based items)
- Cost history
- Alert threshold (advance warning period)
- Parts inventory (quantity on hand, minimum stock level)

### Key Maintenance Intervals

| Item | Interval | Trigger |
|---|---|---|
| Engine oil | 100 hours or annually | Engine hour meter |
| Raw water impeller | 200 hours or 2 years | Engine hour meter |
| Fuel filters | 200 hours | Engine hour meter + Racor vacuum |
| Bottom paint | 12-18 months | Calendar |
| Zinc anodes | 6-12 months | Calendar + visual at haul |
| Standing rigging inspection | Annual | Calendar |
| Standing rigging replacement | 10-12 years | Calendar (CRITICAL) |
| Winch service | Annual | Calendar |
| Through-hull exercise | Quarterly | Calendar |
| Head rebuild | As needed | Behavioral (stiffness, smell) |
| Sail inspection | Annual | Calendar |

### Alerts
- Notification in advance: "Oil change due in 15 engine hours"
- Low inventory: "Only 1 fuel filter remaining — reorder"
- Overdue: "Standing rigging inspection 2 months overdue — SAFETY"

## Hardware Budget

| Item | Est. Cost |
|---|---|
| 2× Raspberry Pi (4B or 5) | $120-$160 |
| Actisense NGT-1 USB gateway | $200-$250 |
| Assorted sensors (bilge, temp, humidity, baro) | $50-$100 |
| Enclosures, wiring, connectors | $50-$100 |
| Camera for fuel filter bowl | $20 |
| Power supplies, fuses, isolation | $50 |
| **Total (excluding Victron battery system)** | **$500-$700** |

Remarkably cheap for a comprehensive monitoring system that commercial vessels pay tens of thousands for.

## Future Enhancements
- Home Assistant integration for complex automation rules
- Historical data analysis for predictive maintenance modeling
- Weather routing integration (GRIB file overlay on chartplotter data)
- Remote monitoring when away from boat (Starlink + Iridium backup)
- AIS traffic analysis and collision risk alerting
