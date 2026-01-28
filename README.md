## OpenADMET + ExpansionRx Blind Challenge

The repository contains a description of the solution to the 
**OpenADMET + ExpansionRx Blind Challenge** by the user `Shorku`.

Author: Oleg Gromov

Date: Dec 2025 - Jan 2026

## Contents

- [Preface](#preface)
- [Overview](#overview)
- [Outline](#outline)
- [Timeline](#timeline)

### Preface

The main objective of the presented solution is to field-test learning from
the full electronic structure of a molecule on the real-world data in real
competition conditions to obtain a fair performance assessment. Hence, the
solution is constrained to a single model architecture of interest.

**TL;DR** Somehow it performs even better than expected but much work is still
to be done.

### Overview

Model type:                      [RhNet2](https://github.com/Shorku/rhnet2) (revised PyG implementation)

Model description:               [JCTC paper](https://doi.org/10.1021/acs.jctc.5c00425)

Fitting regime:                  multitask (9 challenge + 117 additional endpoints)

Model code status:               preparation for publication

Input data type:                 electron density

Input data calculation backend:  [xTB](https://github.com/grimme-lab/xtb)

Input data pipeline code status: preparation for publication

### Outline

**Model**

✅️ input data pipeline efficiency

✅️ RAM consumption 

✅️ embeddings dimensions

⛔️ model stability

⛔️ self-attention

**Challenge solution issues (my faults)**

- somewhat random collection of external data
- train data distribution not addressed
- naive random train-val split
- insufficient analysis of the performance on the val data
- tautomers not addressed 

**Comment**

Replacing DFT densities with PTB densities along with the model's basis and MOs projection procedure updates 
allowed to speed up the input data generation be several orders of magnitude compared to the previous version. 
E.g. the total dataset of 30,000 molecules (> 200,000 conformer structures and > 1,000,000 wavefunctions, 
including test set and unused data) required only ~2300 CPUh (less than 3 days with a single 32-core node).

Inherent redundancy in the graph data (the initial states of some embeddings are essentially different views 
of the same matrices) was made to appear only inside the model. 
This and the more aggressive graph pruning and input data precision reduction resulted in up to ~10 times 
less RAM consumption compared to the previous version. 
It allowed to accommodate a train set of ~15,000 molecules (~500,000 wavefunctions) in just ~100 Gb of RAM 
and to some extent improved the situation with RAM -> VRAM transfer bottleneck. 
Still, the bandwidth is critical.

For some reason, the straightforward reimplementation of the local self-attention mechanism from the previous
version resulted in severe train loss oscillations. 
Seems to be something technical, I need to look into it.

The major remaining issue is model's instability (expected for a GNN tbh). 
Here, I tried a multistage fitting switching optimizers to achieve better stability.
It did help but only a little.
For this reason, the fine optimization of model and data parameters for better competition performance 
is still complicated as it would each time require a number of repeated fittings.
Hence, I didn't really try to tune the hyperparameters, properly balance the training data, or choose 
an adequate train/val splitting strategy. 
Instead, I focused my attention on the model architecture and training details that could lead to noticeable 
performance improvements even in an unstable model.

All in all, now I have some homework to do and the next time there will be less development and more data science.

### Timeline

### Iteration 1 (baseline)

**Status**: complete

**Model**: ensemble of 11 8-layer GNNs

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly, no LogD or KSOL) molecules

**Metrics**: MA-RAE 0.61 | LogD 0.29 | KSOL 0.38 | MLM 0.36 | HLM 0.30 | Efflux 0.32 | Papp 0.21 | MPPB 0.19 | MBPB 0.16 | MGMB 0.25

### Iteration 2 (Vox populi)

**Status**: complete

**Model**: ensemble of 25 2- to 8-layer GNNS

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly, no LogD or KSOL) molecules

**Metrics**: MA-RAE 0.60 | LogD 0.29 | KSOL 0.37 | MLM 0.35 | HLM 0.29 | Efflux 0.31 | Papp 0.21 | MPPB 0.19 | MBPB 0.16 | MGMB 0.25

### Iteration 3 (Model architecture update)

**Status**: complete

**Model**: a single 8-layer GNN from validation

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly, no LogD or KSOL) molecules

**Metrics**: internal validation score improved by 0.005 - 0.01

### Iteration 4 (Per-target optimization strategies)

**Status**: complete

**Model**: a single 8-layer GNN from validation

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly, no LogD or KSOL) molecules

**Metrics**: LB score improved by 0.01 compared to a unified approach

### Iteration 5 (Ready-to-go external data)

**Status**: complete

**Model**: a single 8-layer GNN from validation

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly, no LogD or KSOL) molecules + ~12000 molecules from KERMT and PharmaBench (LogD, KSOL, HLM, Papp targets) 

**Metrics**: Both internal validation and LB scores for the affected targets deteriorated by 0.01 - 0.04

### Iteration 6 (Medium-rare external data)

**Status**: complete

**Model**: a single 8-layer GNN from validation

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly, no LogD or KSOL) molecules + ~5000 molecules from ChEMBL (LogD, HLM, MLM, MPPB targets) filtered and aggregated by the assay descriptions

**Metrics**: Both internal validation and LB scores improved for the LogD and HLM targets by ~0.01, less certain about MLM and MPPB

### Iteration 7 (EOF)

**Status**: complete

**Model**: ensemble of 65 8-layer GNNs

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly, no LogD or KSOL) molecules + ~5000 molecules from ChEMBL (LogD, HLM, MLM, MPPB targets) filtered and aggregated by the assay descriptions

**Metrics**

Final submission: 

MA-RAE 0.58 | LogD 0.28 | KSOL 0.38 | MLM 0.35 | HLM 0.29 | Efflux 0.31 | Papp 0.22 | MPPB 0.19 | MBPB 0.14 | MGMB 0.20

Best compiled from various submissions*: 

MA-RAE nan | LogD 0.27 | KSOL 0.37 | MLM 0.35 | HLM 0.29 | Efflux 0.29 | Papp 0.21 | MPPB 0.19 | MBPB 0.14 | MGMB 0.19

*for consistency reasons the final submission consists of the predictions* 
*by the final ensemble rather than a compilation of the best shots from*
*different submissions throughout the challenge*


