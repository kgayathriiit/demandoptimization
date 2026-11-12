# Coordinated Load-Generation Optimization for Renewable Integrated Microgrid

Project page for the NPEC 2025 paper by Gayathri K and Pallavi Bharadwaj (SPEL, IIT Gandhinagar).
Paper: https://doi.org/10.1109/NPEC66512.2025.11450301

## Files

| File | What it is |
|---|---|
| `index.html` | The page, the LP model and the 1-minute simulation (JavaScript) |
| `data.js` | Load, PV-irradiance and price data (1-minute, 24 h), generated from `pvLoadPriceData.mat` and `Appliancedata_v1 - Copy.csv` exactly as `initialConditions.m` processes them |
| `README.md` | This file |

Both `index.html` and `data.js` must be in the repository root.

## How the live optimization works

1. Every 5 minutes of the simulated day (288 times), the page builds the linear program of
   `battSolarOptimize.m` (241-step horizon, same objective, penalties and limits) and solves it with
   the HiGHS solver (loaded from jsDelivr, `highs@1.8.0`).
2. The battery set-point is the mean of the first 5 planned steps; the shed amounts of the first step are applied.
3. A 1-minute power balance applies the Simulink coordination rules (diesel dispatch, battery
   protection at 19 % / 85 % SOC, 96 % efficiency) and computes grid power, cost and CO2.

Differences from the Simulink model: no electrical network (no losses, voltages or reactive power) and an
instantaneous battery inverter. Shed limits use the load at each step of the horizon (paper equation 5).

## Updating the site

Edit or upload the files on GitHub and commit; GitHub Pages republishes in a minute or two.
To change the data, regenerate `data.js` with the same field names.
