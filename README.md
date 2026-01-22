## OpenADMET + ExpansionRx Blind Challenge

The repository contains a description of the solution to the 
**OpenADMET + ExpansionRx Blind Challenge** by the user `Shorku`.

Author: Oleg Gromov

Date: Dec 2025 - Jan 2026

### Preface

The main objective of the presented solution is to field-test learning from
the full electronic structure of a molecule on the real-world data in real
competition conditions to obtain a fair performance assessment. Hence, the
solution is constrained to a single model architecture of interest.

**TL;DR** Somehow it performs even better than expected but much work is still
to be done

### Overview

Model type:                      [RhNet2](https://github.com/Shorku/rhnet2) (revised PyG implementation)

Model description:               [JCTC paper](https://doi.org/10.1021/acs.jctc.5c00425)

Fitting regime:                  multitask (9 challenge + 117 additional endpoints)

Model code status:               preparation for publication

Input data type:                 electron density

Input data calculation backend:  [xTB](https://github.com/grimme-lab/xtb)

Input data pipeline code status: preparation for publication

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

MA-RAE None | LogD 0.27 | KSOL 0.37 | MLM 0.35 | HLM 0.29 | Efflux 0.29 | Papp 0.21 | MPPB 0.19 | MBPB 0.14 | MGMB 0.19

*for consistency reasons the final submission consists of predictions* 
*by a final ensemble rather than a compilation of the best shots from*
*different models*
