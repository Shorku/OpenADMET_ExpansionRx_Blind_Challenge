Submission status:               iteration 5 transitional (single model, not validated)

Model type:                      [RhNet2](https://github.com/Shorku/rhnet2) (revised PyG implementation)

Model description:               [JCTC paper](https://doi.org/10.1021/acs.jctc.5c00425)

Fitting regime:                  multitask

Model code status:               preparation for publication

Input data type:                 electron density

Input data calculation backend:  [xTB](https://github.com/grimme-lab/xtb)

Input data pipeline code status: preparation for publication

### Iteration 1 (baseline)

**Status**: complete

**Model**: ensemble of 11 8-layer GNNs

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly) molecules with no LogD or KSOL known

**Metrics**: MA-RAE 0.61 | LogD 0.29 | KSOL 0.38 | MLM 0.36 | HLM 0.30 | Efflux 0.32 | Papp 0.21 | MPPB 0.19 | MBPB 0.16 | MGMB 0.25

### Iteration 2 (Vox populi)

**Status**: complete

**Model**: ensemble of 25 2- to 8-layer GNNS

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly) molecules with no LogD or KSOL known

**Metrics**: MA-RAE 0.60 | LogD 0.29 | KSOL 0.37 | MLM 0.35 | HLM 0.29 | Efflux 0.31 | Papp 0.21 | MPPB 0.19 | MBPB 0.16 | MGMB 0.25

### Iteration 3 (Model architecture update)

**Status**: complete

**Model**: -

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly) molecules with no LogD or KSOL known

**Metrics**: no prod ensemble was fitted, internal validation score improved by 0.005 - 0.01

### Iteration 4 (Per-endpoint optimization strategies)

**Status**: complete

**Model**: a single 8-layer GNN

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly) molecules with no LogD or KSOL known

**Metrics**: Improvement of the LB score by 0.01 compared to a unified approach

### Iteration 5 (External data)

**Status**: 🚧 🛠️ 🚧

**Model**: 🚧 🛠️ 🚧

**Data**: the challenge data + phys.chem. properties of additional ~6000 (non-drug mostly) molecules with no LogD or KSOL known + 🚧 🛠️ 🚧

**Metrics**: 🚧 🛠️ 🚧
