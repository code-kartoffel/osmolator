# Osmolality calculator

A single-page tool for making buffers to a target osmolality. Enter the components of a solution and the stocks they come from, set a target, and it tells you how much glucose, sucrose or another solute to pipette.

It runs entirely in the browser. Nothing is sent anywhere; your last solution and your stock concentrations are kept in the browser's local storage.

## Features

- Non-ideal osmotic coefficients: Pitzer model for salts, fitted coefficients for sugars and small molecules, virial estimate for PEG.
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

Typical agreement with measured values is within 1–2% for salt solutions and physiological buffers, and within a few percent for glucose and sucrose up to about 1 mol/kg. Phosphate parameters, trehalose, glycerol, DMSO and ethanol are approximate, and PEG can be off by 20–30%. Each component's model is listed under "Calculation details" on the page.

Always check the final solution on an osmometer. Entering a measured value for the base solution removes most of the model error.

## Main sources

- Pitzer, K. S. & Mayorga, G. (1973). Thermodynamics of electrolytes II. J. Phys. Chem. 77, 2300–2308.
- Pitzer, K. S. & Mayorga, G. (1974). Thermodynamics of electrolytes III. J. Solution Chem. 3, 539–546.
- Robinson, R. A. & Stokes, R. H. Electrolyte Solutions, 2nd ed. (Butterworths).
