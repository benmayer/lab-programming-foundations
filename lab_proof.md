# Lab Proof: HomeGuard Security System

**Name:** Ben Mayer

## Program path
`course work/week-1/lab-programming-foundations/homeguard_system.py` (also as notebook: `homeguard_system.ipynb`, same folder)

## Run command
```
cd "/Users/ben-macbook-air/Files/Projects/Ironhack Bootcamp/course work/week-1/lab-programming-foundations"
python3 homeguard_system.py            # fixed, deterministic cases
python3 homeguard_system.py --random   # optional: seeded random readings (seed 42)
```
Notebook version: open `homeguard_system.ipynb` and use "Run All" (the output below is identical).

## Fixed cases
| Case | Mode | What it proves |
|------|------|----------------|
| 1 | AWAY | Door opened -> HIGH security alert; motion -> HIGH security alert |
| 2 | AWAY | Door + motion in the same tick -> extra CRITICAL "possible break-in" alert |
| 3 | SLEEP | 35°F and 95°F do not alert; 34°F, 96°F and smoke do (safety works in every mode) |
| 4 | HOME | 62°F -> comfort notice; 65°F (edge) -> none; 30°F -> safety alert only; door open >5 min -> notice |

## Output
```

##################################################
# CASE 1: Security (AWAY) - door opens, then motion
##################################################
=== HomeGuard Security System ===
Time: 14:30:00
Mode: AWAY

Time: 14:30:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 68°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 14:31:00
[READING] Living Room Motion: No activity
[READING] Front Door: OPENED
[ALERT!] 🚨 HIGH: SECURITY: Front Door opened while in AWAY mode!
[LOG] [14:31:00] Sending notification to homeowner...
[READING] Kitchen Temperature: 68°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 14:32:00
[READING] Living Room Motion: Motion detected
[ALERT!] 🚨 HIGH: SECURITY: Living Room Motion detected while in AWAY mode!
[LOG] [14:32:00] Sending notification to homeowner...
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 68°F (Normal)
[READING] Bedroom Smoke: CLEAR

[SUMMARY] 16 events logged, 2 alerts/notices raised

##################################################
# CASE 2: Break-in (AWAY) - door + motion in the same tick
##################################################
=== HomeGuard Security System ===
Time: 02:10:00
Mode: AWAY

Time: 02:10:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 68°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 02:11:00
[READING] Living Room Motion: Motion detected
[ALERT!] 🚨 HIGH: SECURITY: Living Room Motion detected while in AWAY mode!
[LOG] [02:11:00] Sending notification to homeowner...
[READING] Front Door: OPENED
[ALERT!] 🚨 HIGH: SECURITY: Front Door opened while in AWAY mode!
[LOG] [02:11:00] Sending notification to homeowner...
[READING] Kitchen Temperature: 68°F (Normal)
[READING] Bedroom Smoke: CLEAR
[ALERT!] 🚨 CRITICAL: SECURITY: Multiple sensors triggered - possible break-in!
[LOG] [02:11:00] Sending notification to homeowner...

[SUMMARY] 14 events logged, 3 alerts/notices raised

##################################################
# CASE 3: Safety (SLEEP) - boundaries 35/95 are NOT alerts; 34, 96, smoke are
##################################################
=== HomeGuard Security System ===
Time: 03:00:00
Mode: SLEEP

Time: 03:00:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 68°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 03:01:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 35°F (Outside comfort range)
[READING] Bedroom Smoke: CLEAR

Time: 03:02:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 34°F (Too cold)
[ALERT!] 🚨 CRITICAL: SAFETY: Kitchen Temperature at 34°F - frozen pipe risk!
[LOG] [03:02:00] Sending notification to homeowner...
[READING] Bedroom Smoke: CLEAR

Time: 03:03:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 95°F (Outside comfort range)
[READING] Bedroom Smoke: CLEAR

Time: 03:04:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 96°F (Too hot)
[ALERT!] 🚨 CRITICAL: SAFETY: Kitchen Temperature at 96°F - equipment failure risk!
[LOG] [03:04:00] Sending notification to homeowner...
[READING] Bedroom Smoke: CLEAR

Time: 03:05:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 68°F (Normal)
[READING] Bedroom Smoke: SMOKE DETECTED
[ALERT!] 🚨 CRITICAL: SAFETY: Bedroom Smoke smoke detected - fire risk!
[LOG] [03:05:00] Sending notification to homeowner...

[SUMMARY] 30 events logged, 3 alerts/notices raised

##################################################
# CASE 4: Comfort (HOME) - cold notice; safety overrides comfort; door open >5 min
##################################################
=== HomeGuard Security System ===
Time: 10:00:00
Mode: HOME

Time: 10:00:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 68°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 10:01:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 62°F (Outside comfort range)
[NOTICE] 🔔 INFO: COMFORT: Kitchen Temperature at 62°F is outside the 65-75°F comfort range
[READING] Bedroom Smoke: CLEAR

Time: 10:02:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 65°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 10:03:00
[READING] Living Room Motion: No activity
[READING] Front Door: CLOSED
[READING] Kitchen Temperature: 30°F (Too cold)
[ALERT!] 🚨 CRITICAL: SAFETY: Kitchen Temperature at 30°F - frozen pipe risk!
[LOG] [10:03:00] Sending notification to homeowner...
[READING] Bedroom Smoke: CLEAR

Time: 10:04:00
[READING] Living Room Motion: No activity
[READING] Front Door: OPENED
[READING] Kitchen Temperature: 70°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 10:05:00
[READING] Living Room Motion: No activity
[READING] Front Door: OPENED
[READING] Kitchen Temperature: 70°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 10:06:00
[READING] Living Room Motion: No activity
[READING] Front Door: OPENED
[READING] Kitchen Temperature: 70°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 10:07:00
[READING] Living Room Motion: No activity
[READING] Front Door: OPENED
[READING] Kitchen Temperature: 70°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 10:08:00
[READING] Living Room Motion: No activity
[READING] Front Door: OPENED
[READING] Kitchen Temperature: 70°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 10:09:00
[READING] Living Room Motion: No activity
[READING] Front Door: OPENED
[READING] Kitchen Temperature: 70°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 10:10:00
[READING] Living Room Motion: No activity
[READING] Front Door: OPENED
[NOTICE] 🔔 INFO: COMFORT: Front Door has been open for 6 minutes
[READING] Kitchen Temperature: 70°F (Normal)
[READING] Bedroom Smoke: CLEAR

Time: 10:11:00
[READING] Living Room Motion: No activity
[READING] Front Door: OPENED
[READING] Kitchen Temperature: 70°F (Normal)
[READING] Bedroom Smoke: CLEAR

[SUMMARY] 52 events logged, 3 alerts/notices raised
```

## Edge case: "door open for more than 5 minutes" (Case 4)
The Front Door opens at 10:04. At 10:09 it has been open exactly 5 minutes and **no** notice is
sent; at 10:10 (6 minutes) the notice `Front Door has been open for 6 minutes` appears once, and
10:11 does not repeat it. I used a strict `>` because the requirement says "more than 5 minutes", so
exactly 5 is still normal. Each sensor stores `since` (when its value last changed) and a
`long_open_flagged` bool, so the clock restarts when the door closes and one opening cannot
spam the homeowner every tick.

## Design choice
Alert rules live in `Sensor.isAbnormal(mode)`, and the safety checks run before the comfort check.
That is why a 30°F reading in HOME mode (Case 4, 10:03) gives only the frozen-pipe alert instead of
a comfort notice as well: the most severe message wins and the mode only affects security and comfort.
