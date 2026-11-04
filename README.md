# Osmolality calculator

A single-page tool for making solutions to a target osmolality from stock solutions. It runs in the browser; your solution and stock concentrations are stored locally.

## Features

- Non-ideal models: Pitzer for salts; Norrish water-activity models for glucose, sucrose, sorbitol, mannitol, glycerol and urea; sucrose constant for trehalose; approximate coefficients for DMSO and ethanol; virial estimate for PEG.
- Buffers split into acid and base forms at the set pH.
- Pipetting volumes for the whole mix from your stock concentrations.
- Optional measured base osmolality: measure the components before topping up and the model only predicts the top-up.
- Optional stock check: measure a diluted top-up stock (default 4×) once or twice and, if ticked, use the measured stock concentration everywhere. Off by default.
- Correction workflow: enter one or two readings per cycle (the mean is used and each reading's sample volume is subtracted). A correction is suggested only when the mean is outside the tolerance; within tolerance the cycle is marked green.
- Figures showing the model behind the numbers.

## Correction workflow

1. Prepare the mix and press **Start correction**.
2. Measure one or two samples, enter the readings and press **Adjust**.
3. If the mean is within ±tolerance (default 1% of target), the cycle turns green and no addition is suggested.
4. Otherwise add the suggested volumes, press **Apply**, and measure again.

Non-adjuster components are kept at their starting concentrations through every correction. The tolerance should not be set below the osmometer's repeatability; for a Gonotec Osmomat 3000 that is about 0.5% (CV) between 400 and 1500 mOsm/kg.

## Stock check

Dilute the top-up stock by the set factor, measure it, and enter the reading(s). The calculator inverts its model to give the effective stock concentration and shows it against the nominal value. Tick **Use measured stock concentration** to apply it to the mix and to corrections.

## Publish on GitHub Pages

1. Upload `index.html` and `README.md` to a public repository.
2. Settings → Pages → Deploy from a branch → `main`, `/ (root)`.
3. The page appears at `https://<username>.github.io/<repository>/`. Later commits redeploy automatically.

## Accuracy

The calculator is an estimate; verify solutions on an osmometer. Salt-sugar cross-interactions and mixed-electrolyte terms without published parameters are not included. Concentrated mixtures are flagged.

## Sources

- Pitzer & Mayorga (1973), J. Phys. Chem. 77, 2300–2308.
- Pitzer & Mayorga (1974), J. Solution Chem. 3, 539–546.
- Pitzer & Kim (1974), J. Am. Chem. Soc. 96, 5701–5707.
- Chirife, Ferro Fontán & Benmergui (1980), J. Food Technol. 15, 59–70.
- Galmarini et al. (2008), LWT 41, 628–631.
- Robinson & Stokes, Electrolyte Solutions, 2nd ed.
