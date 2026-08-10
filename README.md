# # Bayesian Stellar Age Estimation

## Project Overview

This project develops probabilistic models for estimating the ages
of cool main-sequence stars by combining stellar rotation,
spectroscopy, Gaia measurements, and stellar-evolution models.

## Research Question

Does combining stellar spectroscopy with rotation measurements
produce more accurate and reliable stellar-age estimates than
using rotation alone?

## Objectives

1. Establish a deterministic gyrochronology baseline.
2. Develop a Bayesian gyrochronology model.
3. Develop a spectroscopy/evolutionary model.
4. Develop a combined model.
5. Validate the models using open clusters with accepted ages.
6. Quantify uncertainty and credible-interval coverage.

## Models

### Model A — Deterministic Gyrochronology

Rotation + temperature → age estimate.

### Model B — Bayesian Gyrochronology

Rotation + temperature + uncertainties → posterior age distribution.

### Model C — Spectroscopic/Evolutionary Model

Teff + log(g) + [Fe/H] + Gaia photometry/parallax → age.

### Model D — Combined Model

Rotation + spectroscopy + Gaia + stellar evolution → posterior age.

## Data Sources

- Gaia
- Kepler / K2 / TESS
- APOGEE
- LAMOST
- GALAH
- Gaia RVS
- Published open-cluster catalogues

## Project Status

### Completed
- Project definition

### In Progress
- Literature review
- Dataset selection

### Planned
- Data collection
- Data cleaning
- Baseline gyrochronology
- Bayesian modelling
- MCMC validation
- Model comparison

## Repository Structure

```text
data/
notebooks/
src/
results/
tests/
requirements.txt
