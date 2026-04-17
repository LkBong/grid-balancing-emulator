# Balance the Grid

A single-file browser game simulating UK National Grid frequency management. You play as a grid operator working a 12-hour shift (06:00-18:00), dispatching generation sources to keep grid frequency within the safe band.

## How to play

Open `balance-the-grid.html` directly in a browser. No server, build step, or installation required.

## Objective

Keep grid frequency between **49.8 and 50.2 Hz** for the full shift. Frequency below 48.5 Hz or above 51.5 Hz triggers a cascade failure and ends the game.

Your score combines stability (time spent in the safe band), environmental performance (low carbon dispatch), and financial balance.

## Controls

| Source | Range | Control |
|---|---|---|
| Gas | 0-500 MW | Continuous slider |
| Nuclear | 300-800 MW | Pulse buttons (+/-50 MW, 8s cooldown) |
| Hydro | 0-200 MW | Pulse buttons (+/-40 MW, 2.8s cooldown) |
| Battery | +150 / -120 MW | Mode toggle (discharge / standby / charge) |
| Interconnect | +200 / -150 MW | Mode toggle (import / off / export) |
| Curtailment | -130 MW demand | Toggle (30s cooldown) |

Solar and wind output are weather-driven and not directly controllable.

## Scripted events

The shift includes a sequence of events that force you to adapt:

- **07:00** - solar generation begins ramping up
- **07:45** - winds strengthen
- **08:30** - cloud bank reduces solar by 75%
- **09:30** - morning industrial demand surge (+180 MW)
- **10:30** - skies clear, solar restored
- **11:00** - gas turbine trips offline for 40 minutes
- **12:00** - winds drop sharply
- **13:00** - gas turbine returns
- **15:00** - evening demand surge (+250 MW)
- **16:00** - solar goes offline at sunset
- **17:00** - demand begins easing

## Upgrades

Spend your operating budget on infrastructure upgrades:

| Upgrade | Cost | Effect |
|---|---|---|
| Peaker Plant | £3,000 | Gas ceiling 500 to 750 MW |
| Grid Battery+ | £4,000 | Storage 600 to 1,200 MWh |
| Offshore Wind | £5,000 | Wind capacity +50% |
| Smart Grid AI | £3,500 | Reduces frequency sensitivity |
| Solar Farm+ | £2,500 | Solar ceiling 350 to 500 MW |
| Pumped Hydro+ | £4,500 | Hydro ceiling 200 to 400 MW |

## Scoring

- **Stability score** - proportion of ticks spent within the 49.8-50.2 Hz band
- **Environmental score** - penalised for high gas output, rewarded for renewables
- **Balance** - net operating profit after gas costs and interconnect fees

## Technical notes

Built as a single HTML file with inline CSS, HTML, and JavaScript. The UK map uses D3.js v7 with custom region polygons for 11 GB regions and animated transmission lines.

**Dependency:** D3.js v7.8.5 loaded from cdnjs.
