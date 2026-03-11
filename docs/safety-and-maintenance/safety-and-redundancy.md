# Safety & Redundancy

## Design Philosophy

> Every critical system has a failover. No single point of failure should be catastrophic.

Apply the same redundancy thinking as server infrastructure: primary system, failover, monitoring, and graceful degradation. Boats get into serious trouble when multiple systems fail simultaneously because the owner didn't think about redundancy, or when a single failure cascades because systems were interdependent.

## Redundancy Matrix

| System | Primary | Secondary | Tertiary | Last Resort |
|---|---|---|---|---|
| Navigation | Chartplotter | Backup handheld GPS | Paper charts + compass | Dead reckoning |
| Bilge | Auto electric (2000+ GPH) | Secondary electric (separate circuit/battery) | Manual diaphragm pump (cockpit-mounted) | Bucket |
| Communication | VHF radio | Handheld backup VHF | Starlink | Iridium |
| Propulsion | Diesel inboard | Sails | Emergency outboard (6-8 HP) | — |
| Electrical | Shore power | Alternator | Solar panels | Battery bank |
| Anchoring | Primary anchor + rode | Secondary anchor on separate rode | — | — |
| Steering | Wheel/tiller | Autopilot | Emergency tiller | — |
| Position info | GPS/chartplotter | Handheld GPS | Radar | Visual / paper charts |
| Distress | VHF DSC Ch 16 | Iridium | EPIRB | Flares + horn |

## Bilge Pump System (Defense in Depth)

### Layer 1: Primary Electric (automatic)
- 2,000+ GPH rated (actual installed capacity: ~1,200-1,400 GPH due to head and hose losses)
- Float switch activated (runs without intervention)
- **Wired directly to battery** (not through main panel breaker — works even if electrical panel fails)
- Handles nuisance water: stuffing box drip, rain, condensation

### Layer 2: Secondary Electric (automatic failover)
- Separate circuit, ideally separate battery
- Own float switch set slightly **higher** than primary's switch
- Activates only when water level means primary has failed or can't keep up

### Layer 3: Manual Diaphragm Pump
- High-capacity: Whale Titan or Henderson, 25-30 GPM (1,500-1,800 GPH)
- Permanently mounted in cockpit (operable from safe position)
- No electricity, no wiring, no switches — nothing to fail except your arm
- The Navy doesn't trust electric pumps for damage control — they use people with manual pumps

### Layer 4: Bucket
- A frightened human with a bucket can move a surprising amount of water
- Zero failure modes

### Monitoring
- Bilge pump counter/alarm in cabin
- Logs every pump cycle
- If pump cycles every 10 minutes when it normally cycles once an hour → early warning
- Tied into Signal K monitoring system

### Context
A one-inch hole below the waterline admits ~1,500-2,500 GPH depending on depth. The primary pump at installed capacity barely keeps up with a single small breach. It buys time — it doesn't solve the problem. Finding and stopping the leak is the actual solution.

## Through-Hull Safety

- Every hole in the hull below the waterline has a seacock valve
- **Exercise them (open and close) quarterly** so they don't seize
- Inspect at every haul-out
- Older bronze through-hulls: check for dezincification (zinc leaches out, leaves porous weak fitting that looks fine but crumbles)
- Know the location of every through-hull and keep wooden plugs sized to each one within reach — if a through-hull fails, hammering a plug into it is faster than anything else
- A failed through-hull is a hole in your boat below the waterline

## Fire Safety

- Multiple fire extinguishers (minimum: one in galley area, one in engine compartment, one in cabin accessible from cockpit)
- Engine compartment automatic fire suppression system (HFC-227ea or similar)
- Galley fire blanket
- Smoke and CO detectors
- Propane/LPG sniffer if using gas for cooking (propane is heavier than air and pools in bilge — explosive)
- Fuel shutoff accessible from cockpit

## Man Overboard

- MOB equipment readily accessible (throwable PFD, life sling)
- Practice MOB recovery drills regularly (covered in ASA courses)
- AIS MOB beacon on PFD (transmits position to chartplotter if you go in)
- When singlehanding: always wear PFD with harness, clip tether to jacklines
- Kill cord on engine when singlehanding (engine stops if you go overboard)

## Heavy Weather Preparation

- Sea anchor / drogue (slows boat, keeps stern to waves)
- Storm sails (small, heavily built)
- Lee cloths on berths (keep you in your bunk in rough seas)
- Jacklines (deck-length webbing to clip safety tether to)
- Companionway storm boards (seal below decks from boarding seas)

## Emergency Equipment List

- [ ] EPIRB (Emergency Position Indicating Radio Beacon) — registered to vessel
- [ ] Flares (current, not expired)
- [ ] Horn (air horn or fixed)
- [ ] VHF radio (fixed mount) + handheld backup
- [ ] First aid kit (marine-specific)
- [ ] Fire extinguishers (3+ locations)
- [ ] Throwable PFD
- [ ] Life sling or MOB recovery device
- [ ] PFDs for all aboard (inflatable with harness for offshore)
- [ ] Safety tethers and jacklines
- [ ] Wooden plugs for every through-hull
- [ ] Flashlights / headlamps (waterproof, with spare batteries)
- [ ] Radar reflector (makes you visible to ships)
- [ ] Navigation lights (all working, with spares)
- [ ] Anchor light
- [ ] Tool kit for emergency repairs
- [ ] Spare parts kit (see maintenance doc)
