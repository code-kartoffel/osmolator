# OSMOLATOR

A single-page tool for making solutions to a target osmolality from stock solutions. It runs entirely in the browser, works on desktop, iPad and phone, and stores nothing: every reload starts from the default solution (10 mM NaCl, adjusted with glucose to 900 mOsm/kg in 10 mL).

## Steps

1. **Formulate the solution.** Components at their final concentrations with their stocks, the adjustment solution (usually a sugar) and its stock, the target osmolality and the final volume.
2. **Measure the adjustment solution (optional).** Measure a dilution of the adjustment stock (default 4×) once or twice. The calculator shows the expected reading and the stock concentration implied by your reading. Tick the box to use the measured concentration for the mix and for corrections; it is off by default.
3. **Mix.** The target osmolality and what to pipette: each stock, then the water. Copy recipe puts the list on the clipboard.
4. **Measure and correct.** Enter one or two readings (the mean is used, and each reading's sample volume is subtracted) and press Adjust. Within the tolerance (default ±1% of the target) the cycle turns green. Otherwise add the suggested volumes, press Apply and measure again. All other components stay at their concentrations.
5. **Details.** Collapsible calculation breakdown and figures explaining the models.

Each step has a Tips button with a short description.

## Models

- Salts: Pitzer ion-interaction model at 25 °C with published binary parameters.
- Glucose, sucrose, sorbitol, mannitol, glycerol, urea: Norrish water-activity model; trehalose uses the sucrose constant.
- DMSO and ethanol: approximate osmotic coefficients. PEG: virial estimate.
- Buffers split into acid and base forms at the set pH.

The calculator is an estimate; always verify on an osmometer. Set the correction tolerance no lower than your osmometer's repeatability (for a Gonotec Osmomat 3000, about 0.5% CV between 400 and 1500 mOsm/kg).

## Publish on GitHub Pages

1. Upload `index.html` and `README.md` to a public repository.
2. Settings → Pages → Deploy from a branch → `main`, `/ (root)`.
3. The page appears at `https://<username>.github.io/<repository>/`. Later commits redeploy automatically.

## Sources

- Pitzer & Mayorga (1973), J. Phys. Chem. 77, 2300–2308.
- Pitzer & Mayorga (1974), J. Solution Chem. 3, 539–546.
- Pitzer & Kim (1974), J. Am. Chem. Soc. 96, 5701–5707.
- Chirife, Ferro Fontán & Benmergui (1980), J. Food Technol. 15, 59–70.
- Galmarini et al. (2008), LWT 41, 628–631.
- Robinson & Stokes, Electrolyte Solutions, 2nd ed.
