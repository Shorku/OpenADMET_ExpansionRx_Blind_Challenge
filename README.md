Submission status:               iteration 2 transitional (sub-ensemble of 3 models from ensemble-candidate)

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
