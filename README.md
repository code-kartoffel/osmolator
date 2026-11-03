# Osmolality calculator

A single-page tool for making buffers to a target osmolality. Enter the components of a solution and the stocks they come from, set a target, and it tells you how much glucose, sucrose or another solute to pipette.

It runs entirely in the browser. Nothing is sent anywhere; your last solution and your stock concentrations are kept in the browser's local storage.

## Features

- Non-ideal osmotic coefficients: Pitzer model for salts, reference-data interpolation for glucose/sucrose/urea/glycerol, explicit approximations for the remaining small molecules, and a virial estimate for PEG.
- Buffers (HEPES, MOPS, MES, Tris, sodium and potassium phosphate) split into acid and base forms at the pH you set.
- Stocks remembered per component, with pipetting volumes in µL or mL and the water to add.
- Target as a reference plus an offset, for example vesicle interior + 50 mOsm/kg.
- Optional calibration to a measured osmolality of the base solution.
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

## Accuracy

For supported single-salt solutions, the electrolyte calculation uses the standard Pitzer osmotic-coefficient expression at 25 °C with published beta(0), beta(1), beta(2) and Cphi parameters. Glucose, sucrose, urea and glycerol use concentration-dependent reference trends rather than unconstrained polynomial extrapolation. Trehalose, sorbitol, mannitol, DMSO and ethanol remain approximate, phosphate parameters are less certain, and PEG can be off by 20–30%. Mixed salt-neutral solutions can have additional interaction terms that are not available for every pair; the app warns when those terms may matter. Each component's model is listed under "Calculation details" on the page.

Always check the final solution on an osmometer. Entering a measured value for the base solution removes most of the baseline model error, but it cannot fully correct concentration-dependent salt-neutral interactions in a concentrated final mixture.

## Main sources

- Pitzer, K. S. & Mayorga, G. (1973). Thermodynamics of electrolytes II. J. Phys. Chem. 77, 2300–2308.
- Pitzer, K. S. & Mayorga, G. (1974). Thermodynamics of electrolytes III. J. Solution Chem. 3, 539–546.
- Robinson, R. A. & Stokes, R. H. Electrolyte Solutions, 2nd ed. (Butterworths).
- Scatchard, G., Hamer, W. J. & Wood, S. E. (1938). Osmotic coefficients of aqueous nonelectrolyte solutions (reference data used for sucrose, urea and glycerol trends).
- Wang, P., Pitzer, K. S. & Simonson, J. M. (1998). Thermodynamic properties of aqueous magnesium chloride solutions. J. Phys. Chem. Ref. Data 27, 971–991.

## Model notes

- The electrolyte routine evaluates the Pitzer osmotic-coefficient expression on molality, including the Debye–Hückel term and every cation–anion parameter available in the built-in table. It does not invent missing same-charge or ternary parameters.
- Molar concentrations are converted to molality using apparent molar volumes and an explicit estimate of kilograms of water per litre of final solution.
- Glucose, sucrose, urea and glycerol are evaluated from concentration-dependent osmotic-coefficient reference curves with conservative interpolation.
- Buffers are speciated at the chosen pH and iterated with the ionic-strength correction.
- PEG is evaluated with a mass-concentration virial expansion.
- Specific salt–neutral interactions are not universally parameterized; concentrated mixtures are therefore flagged even when both binary component models are well characterized.
