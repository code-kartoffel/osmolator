# Osmolality calculator

A single-page tool for making buffers to a target osmolality. Enter the components of a solution and the stocks they come from, set a target, and it tells you how much glucose, sucrose or another solute to pipette.

It runs entirely in the browser. Nothing is sent anywhere; your last solution and your stock concentrations are kept in the browser's local storage.


## Features

- Non-ideal osmotic coefficients: Pitzer model for salts; published Norrish water-activity models for glucose, sucrose, sorbitol, mannitol, glycerol and urea; sucrose-equivalent Norrish treatment for trehalose; legacy approximations for DMSO and ethanol; virial estimate for PEG.
- Buffers (HEPES, MOPS, MES, Tris, sodium and potassium phosphate) split into acid and base forms at the pH you set.
- Stocks remembered per component, with pipetting volumes in µL or mL and the water to add.
- Target as a reference plus an offset, for example vesicle interior + 50 mOsm/kg.
- Optional calibration to a measured osmolality of the base solution.
- Iterative post-measurement correction: enter the osmometer result and press one **Adjust** button; the app automatically accounts for the test sample removal (50 µL by default) and calculates the next addition while keeping all non-adjuster components at their starting concentrations. The corrected state is carried into the next test cycle.
- Ionic strength and Debye length of the final solution.
- A collapsible Figures section showing the model behind the numbers: salt and sugar non-ideality, PEG, buffer speciation, Debye length and how the top-up is solved. The last three charts follow your current solution.

## Publish it on GitHub Pages (recommended)

1. Create a new repository on GitHub, for example `osmolality-calculator`.
2. Upload `index.html` and `README.md` (Add file → Upload files), then commit.
3. Go to Settings → Pages. Under "Build and deployment", choose "Deploy from a branch", select `main` and `/ (root)`, and save.
4. After a minute or two the page is live at `https://<your-username>.github.io/osmolality-calculator/`.

GitHub Pages on a free account requires the repository to be public.

## Publish it on GitLab Pages

1. Create a new project on GitLab and push all files, including `.gitlab-ci.yml`.
2. The pipeline copies `index.html` into `public/` and publishes it.
3. Find the address under Deploy → Pages. It is either `https://<your-username>.gitlab.io/osmolality-calculator/` or a unique `*.gitlab.io` domain, depending on your settings.

`.gitlab-ci.yml` starts with a dot, so some file browsers hide it. Make sure it gets uploaded.

## Run it locally

Open `index.html` in any browser. It works offline; only the font needs a connection, and it falls back to the system font without one.

## Accuracy and model scope

The calculator is a thermodynamic estimate, not a substitute for an osmometer. Salts use published Pitzer binary interaction parameters at 25 °C. Same-charge and ternary mixed-electrolyte terms are not guessed when parameters are unavailable.

Glucose, sucrose, sorbitol, mannitol, glycerol and urea use the published Norrish water-activity relation, converted to osmolality through `osmolality = -ln(a_w)/M_water`. Trehalose uses the sucrose Norrish constant because published measurements report nearly identical water-activity lowering for trehalose and sucrose at equal concentration. DMSO, ethanol and the PEG models remain approximate and are identified as such in the app.

Specific salt-neutral cross-interactions (for example glucose-MgCl2) are not introduced without published parameters. Concentrated mixed solutions are therefore flagged because their error can exceed the error of the corresponding binary solutions.

Always verify the final solution on an osmometer. The optional base-solution calibration is intended to remove a measured offset from the starting mixture rather than to hide model limitations.

## Iterative measured correction

After the initial recipe is prepared, click **Start correction workflow**. The workflow is independent of the original recipe display and tracks the actual remaining volume and component amounts through repeated measurements.

1. Measure the configured test sample (default 50 µL), enter the measured osmolality, and press **Adjust (sample already removed)**. The same click automatically subtracts that sample from the tracked mixture. Sampling a well-mixed solution decreases amount and volume proportionally, so concentrations are unchanged by sampling itself.
2. The difference between the measurement and the model prediction at that composition is used as a local additive calibration offset for this correction cycle only. No new thermodynamic coefficient is fitted or invented.
3. If osmolality is too low, the calculator recommends the selected osmolyte stock plus the required amounts of every background-component stock so their original concentrations remain unchanged.
4. If osmolality is too high, it recommends a matched dilution: water plus the required background-component stocks, so the osmolyte is diluted while background concentrations remain unchanged.
5. Make the suggested addition and press **Apply suggested addition**. The corrected volume and amounts become the starting point for the next test. Measure the next sample, enter its result, and press **Adjust** again.

The correction workflow requires liquid stocks that are more concentrated than the fixed background concentrations. It preserves every non-adjuster component, not just salts, so salt and buffer concentrations do not drift during repeated corrections.

## Main sources

- Pitzer, K. S. & Mayorga, G. (1973). *Thermodynamics of electrolytes. II. Activity and osmotic coefficients for strong electrolytes with one or both ions univalent.* J. Phys. Chem. 77, 2300–2308. DOI: 10.1021/j100638a009.
- Pitzer, K. S. & Mayorga, G. (1974). *Thermodynamics of electrolytes. III. Activity and osmotic coefficients for 2-2 electrolytes.* J. Solution Chem. 3, 539–546. DOI: 10.1007/BF00648138.
- Pitzer, K. S. & Kim, J. J. (1974). *Thermodynamics of electrolytes. IV. Activity and osmotic coefficients for mixed electrolytes.* J. Am. Chem. Soc. 96, 5701–5707. DOI: 10.1021/ja00825a004.
- Chirife, J., Ferro Fontán, C. & Benmergui, E. A. (1980). *The prediction of water activity in aqueous solutions in connection with intermediate moisture foods. IV. a_w prediction in aqueous non-electrolyte solutions.* J. Food Technol. 15, 59–70. DOI: 10.1111/j.1365-2621.1980.tb00919.x. Published Norrish constants used here: glucose 2.25, sucrose 6.47, sorbitol 1.65, mannitol 0.906, glycerol 1.16, urea -2.02.
- Galmarini, M. V., Chirife, J., Zamora, M. C. & Pérez, A. (2008). *Determination and correlation of the water activity of unsaturated, supersaturated and saturated trehalose solutions.* LWT 41, 628–631. DOI: 10.1016/j.lwt.2007.04.007.
- Robinson, R. A. & Stokes, R. H. *Electrolyte Solutions*, 2nd ed. Butterworths.
