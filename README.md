# WIDS LHC Project

This project presents a machine learning–based analysis for separating Prompt, Non-Prompt, and Background D\* candidates in proton–proton collision data from the LHC as part of the WIDS. Using ROOT-based datasets and a Boosted Decision Tree (BDT) classifier. The model is trained exclusively on topological variables to exploit decay geometry and lifetime information, while kinematic variables are used only for validation and interpretation. I have chosen the base case hyperparamters for model training with max depth as 4, thus all the further analysis is with respect to it but still I have included the plots with different sets of hyperparamters.

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

## Definition of Physics Classes

### Prompt

- D\* mesons produced directly at the primary vertex.
- These candidates have: Small impact parameters, Large cosine of pointing angle, Short decay lengths

### Non-Prompt

- D\* mesons originating from beauty hadron decays.
- These particles decay away from the primary vertex and therefore show: Larger decay lengths, Larger impact parameters, Distinct topological signatures compared to prompt signals

### Background (BKG)

- Combinatorial background formed from random track combinations.
- These candidates do not correspond to real D\* decays and typically show: Poor pointing, Broad distributions in mass and topological variables

---

## Variable Definitions

### Topological variables

- fCpaD0: Cosine of the pointing angle between the reconstructed D⁰ momentum and the line joining the primary and secondary vertices. Values closer to 1 indicate a well-aligned decay.
- fCpaXYD0: Transverse-plane version of the cosine of the pointing angle, sensitive to decay geometry in the XY plane.
- fDecayLengthXYD0: Transverse decay length of the D⁰ candidate, reflecting the displacement of the decay vertex from the primary vertex.
- fImpactParameterProductD0: Product of the impact parameters of the D⁰ decay tracks, useful for distinguishing displaced decays from prompt ones.
- fImpParamSoftPi: Impact parameter of the soft pion from the D\* decay, sensitive to the decay topology.
- fMaxNormalisedDeltaIPD0: Maximum normalized difference in impact parameters of D⁰ decay tracks, capturing track-level displacement inconsistencies.

### Kinematic variables

- fPt: Transverse momentum (pT) of the D\* candidate.
- fM: Invariant mass of the D\* candidate.
- fMD0: Invariant mass of the D⁰ candidate.
- fInvDeltaMass: Mass difference between the D* and D⁰ candidates, used to identify the characteristic D* signal peak.

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

## Pre-Training Variable Distributions

Before training the classifier, distributions of all selected variables were studied for:

- Prompt
- Non-Prompt
- Background

## Key Observations

- Topological variables such as: fCpaD0, fCpaXYD0, fDecayLengthXYD0 show clear separation between signal and background.
- Background events are broadly distributed, while prompt candidates peak sharply near physically expected values.
- Non-prompt events typically lie between prompt and background, reflecting their displaced decay nature.
- Kinematic variables (fM, fMD0, fInvDeltaMass) show clear mass peaks for signal and wide distributions for background.
- These observations justify the use of topological variables alone for model training.

---

## ROC Curve Analysis

- ROC curves were produced for all major class combinations: Prompt vs Background, Non-Prompt vs Background, Prompt vs Non-Prompt

### Interpretation

- Non-Prompt vs Background shows the highest AUC (~0.94), indicating strong separation.
- Prompt vs Background also shows good discrimination (AUC ~0.90).
- Prompt vs Non-Prompt is more challenging (AUC ~0.82), as expected due to overlapping physical characteristics.
- The diagonal dashed line represents random classification, and all trained curves lie significantly above it, confirming meaningful learning.

---

## BDT Score Distributions

BDT score distributions were obtained for each class:

- Prompt events peak at high BDT scores
- Background events peak near zero
- Non-Prompt events occupy an intermediate region

This behavior confirms that the classifier correctly assigns higher signal-likeness to prompt candidates and effectively suppresses background.

---

## Correlation Matrix

The correlation matrix of the topological variables shows:

- Mostly weak to moderate correlations
- No strongly redundant variables
- A well-conditioned feature space suitable for BDT training

This supports the robustness of the variable selection.

---

## Post-Training Results (pT ∈ 3–4 GeV/c)

After BDT training, both topological and kinematic variables were re-plotted for the BDT-selected events. The topological distributions show strong background suppression with prompt and non-prompt signals concentrated in physically expected regions, indicating effective learning of decay topology. Despite not being used for training, the kinematic variables also exhibit improved signal-to-background separation after selection. This confirms that the classifier generalizes well and enhances genuine D\* signals without relying on trivial kinematic correlations.

---

## Overall Conclusions

- A complete ML-based classification pipeline for D\* meson analysis has been successfully implemented.
- Topological variables provide strong discriminating power between signal and background.
- The XGBoost classifier performs well across multiple class combinations.
- The model generalizes well to unseen test data.
- The analysis framework is modular and easily extendable to: Other pT bins, Additional PID variables, Mixed-class datasets (future extension)

This repository fulfills all the objectives outlined in the problem statement for a single pT bin (3–4 GeV/c) and provides a solid foundation for further physics-driven machine learning studies.

---

## Notes

- ROOT files are excluded from the repository using `.gitignore`.
- All plots generated during the analysis are stored in the `plots/` directory.
- This repository corresponds to a single pT bin as required.
