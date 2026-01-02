# WIDS LHC Project

This repository contains the machine learning analysis performed as part of the
WIDS–LHC project.

The analysis is carried out for the transverse momentum (pT) range:

**pT = 3–4 GeV/c**

---

## Input Files

The following ROOT files are used in the analysis (not included in the repository):

1. `Bkg_DstarToD0Pi.root`
2. `Nonprompt_DstarToD0Pi.root`
3. `Prompt_DstarToD0Pi.root`

Each file contains a TTree named `treeMLDstar`.

---

## Objectives and Tasks

- Inspect the ROOT files using the ROOT browser and identify the available branches.
- Obtain plots of the selected parameters for **Prompt**, **Non-Prompt**, and
  **Background** classes on the same canvas.
- Study the variables discussed in the meetings and select only topological
  variables for model training.

### Topological Variables (used for training)

1. `fCpaD0`
2. `fCpaXYD0`
3. `fDecayLengthXYD0`
4. `fImpactParameterProductD0`
5. `fImpParamSoftPi`
6. `fMaxNormalisedDeltaIPD0`

### Kinematic Variables (used for plotting and evaluation)

1. `fPt`
2. `fM`
3. `fMD0`
4. `fInvDeltaMass`

---

## Model Training

- Train the model in the following pT ranges:
  [1,1.5,2,3,4,6,8,10,12,16,24]

- The pT branch used is `fPt`.
- For this repository, the analysis is performed for **pT = 3–4 GeV/c**.
- Divide the dataset into:
  - Training set
  - Testing set
- Test fraction used: **0.3**
- Train the model using only topological variables.
- Explore different sets of hyperparameters and list their values explicitly.

---

## Model Evaluation

- Obtain ROC curves for different class combinations.
- Obtain BDT score distributions for each class.
- Plot the correlation matrix of topological variables.
- After training, re-plot the above-mentioned parameters for the selected pT range.
- Use the test fraction of the dataset to evaluate the trained model.

---

## Notes

- ROOT files are excluded from the repository using `.gitignore`.
- All plots generated during the analysis are stored in the `plots/` directory.
- This repository corresponds to a single pT bin as required.
