# Classifier decorrelation on real ATLAS Open Data

Janus Capellan Aban

This repository applies classifier decorrelation by conditional optimal transport to **real 13 TeV proton–proton collision data and official simulation** from the ATLAS experiment.

A classifier trained to separate top quark pairs (ttbar) from W bosons produced with jets (W + jets) uses missing transverse energy as one of its inputs. Cutting on the classifier therefore reshapes (sculpts) the W + jets missing transverse energy spectrum. A conditional optimal transport map replaces each score by its percentile among W + jets events with similar missing transverse energy, which removes the dependence. The classifier and the map are built on simulation and then applied unchanged to real collision data.

## Why it matters beyond physics

The same calculation is a fairness correction. Read background events as people who should not be flagged and missing transverse energy groups as protected groups: decorrelation then equalises false positive rates across groups. Certifying how small the remaining gap is, with a guarantee that holds even though the map was fitted on data, is an open statistical problem.

| Particle physics | Fairness |
|---|---|
| Background (W + jets) events | Negative outcome cases |
| Missing transverse energy group | Protected group |
| Background efficiency in a group | Group false positive rate |
| Sculpting of the background shape | Unequal false positive rates |

## Data

- **Source:** ATLAS Open Data for Education and Outreach, 2025 beta release, 13 TeV, 2015 and 2016 data, about 36 fb⁻¹ ([CERN Open Data record 93910](https://opendata.cern.ch/record/93910)), licence CC0.
- **Selection:** `1LMET30` skim, then exactly one lepton (pT ≥ 30 GeV), at least two jets (pT ≥ 30 GeV), missing transverse energy ≥ 30 GeV and W transverse mass ≥ 30 GeV.
- **Simulation:** ttbar (410470) and Sherpa 2.2.11 W + jets (700338 to 700349).
- Files are streamed from CERN; no data are stored in this repository.

## Important notes

- This is a **teaching example**, not an ATLAS result, and **not a monojet search**: the release has no zero-lepton skim. Section 9 of the notebook explains how to extend it.
- Only ttbar and W + jets are simulated, so the comparison with real data is qualitative. No systematic uncertainties are included.

## Running the notebook

Requirements: Python 3.10 or later and an internet connection.

    pip install -r requirements.txt
    jupyter notebook atlas_opendata_decorrelation.ipynb

- By default the notebook reads a limited number of events per file; increase `MAX_EVENTS_PER_FILE` and `N_DATA_FILES` in Section 1 for more statistics.
- CERN's server limits request rates. The notebook groups requests and retries automatically. If problems persist, set `ACCESS = 'download'` to download each file once (one real-data file is about 8 GB).

## Related work

- Simulated monojet version and a fairness pilot simulation: [uncertainty-aware-decorrelation](https://github.com/YOUR-USERNAME/uncertainty-aware-decorrelation)

## References

- ATLAS Collaboration (2025). ROOT ntuple format 2015–2016 proton–proton Open Data for Education and Outreach (beta release). CERN Open Data Portal. doi:10.7483/OPENDATA.ATLAS.B5M9.44TN
- P. Chakravarti, L. Kania, O. Behnke, M. Kuusela and L. Wasserman. Robust semi-parametric signal detection in particle physics with classifiers decorrelated via optimal transport. arXiv:2409.06399.
- M. Algren, J. A. Raine and T. Golling. Decorrelation using optimal transport. European Physical Journal C 84, 579 (2024).
- ATLAS Open Data example notebooks: https://github.com/atlas-outreach-data-tools/notebooks-collection-opendata

## Contact

janus.aban@gmail.com
