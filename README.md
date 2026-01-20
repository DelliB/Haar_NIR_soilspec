#Motivation

Rapid, cost-effective soil monitoring is increasingly reliant on handheld Near-Infrared (NIR) scanners; however, field moisture significantly reduces prediction accuracy by introducing noise and obscuring spectral features. Traditional correction methods, such as External Parameter Orthogonalization (EPO), rely on experimentally intensive drying curves that are difficult to standardize. This project evaluates the Discrete Haar Multi-Resolution Wavelet algorithm as a preprocessing technique to compress spectral data and enhance signal-to-noise ratios. The goal is to determine if Haar-transformed spectra can maintain predictive accuracy for Organic Carbon, pH, and Clay while reducing the dampening effects of soil wetness.

#Methods

##Data Preparation

Dataset: We utilized 2,106 unique mineral topsoil samples from the KSSL database (dry) and a specific subset of 50 samples re-wetted to saturation and scanned continuously until dry to create a wetness gradient (307 unique wet scans).
Preprocessing: Spectra were interpolated to 2 nm spacing and normalized using the Standard Normal Variate (SNV) algorithm prior to wavelet transformation. Signals were padded to a power of 2 to facilitate iterative bisection.

##Haar Wavelet Analysis

Transformation: We applied a discrete Haar transform, decomposing the signal into "trends" (signal skeletons/averages) and "fluctuations" (details) using pairwise calculations.
Compression: Signals were compressed by discarding higher-level fluctuations (back-transforming partial coefficients). We tested compression levels ranging from full signal down to 0.5% retention.

##Modeling & Validation

Algorithms: We trained linear Partial Least Squares Regression (PLSR) and tree-based Cubist models.
Scenarios: Performance was evaluated across three scenarios: dry-calibrated/dry-predicted, dry-calibrated/wet-predicted, and wet-calibrated/wet-predicted.
Software: Analysis was performed in R (v.4.2.1) using tidyverse, pls, Cubist, and prospectr packages.
