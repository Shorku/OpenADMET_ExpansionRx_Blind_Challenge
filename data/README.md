## OpenADMET + ExpansionRx Blind Challenge

The repository contains the calculated data for the solution to the 
**OpenADMET + ExpansionRx Blind Challenge** by the user `Shorku`.

Author: Oleg Gromov

Date: Dec 2025 - Jan 2026

## Contents

- [Indexes](#indexes)
- [Geometries](#geometries)
- [Molecular orbitals](#molecular-orbitals)
- [Molecular properties](#molecular-properties)
- [Methods](#methods)
- [Data stats](#data-stats)

### Indexes

**OpenADMET/ExpansionRx data**

train set: `openadmet_train_index.csv`

test set: `openadmet_test_index.csv`

**External train data (no ADMET properties)**

included in the final solution: `physchem_external_train_index.csv`

calculated but not used: `physchem_external_unused_index.csv`

**External train data with ADMET properties**

included in the final solution: `admet_external_train_index.csv`

calculated but not used: `admet_external_unused_index.csv`

**Columns:**

`Molecule Name`: molecule name from OpenADMET/ExpansionRx data if available, a preferred molecule name otherwise 

`DTXSID`: DSSTox substance identifier

`CASRN`: CAS registry number

`SMILES`: molecule in the SMILES format

`id`: internal molecule id, a BLAKE2b hash of molecules canonical SMILES 

`nconf`: the number of available conformers

### Geometries

**OpenADMET/ExpansionRx data**

train set: `openadmet_train_geoms.zip`

test set: `openadmet_test_geoms.zip`

**External train data (no ADMET properties)**

included in the final solution: `physchem_external_train_geoms.zip`

calculated but not used: `physchem_external_unused_geoms.zip`

**External train data with ADMET properties**

included in the final solution: ⏳️🗜️📤️

calculated but not used: ⏳️🗜️📤️

**Format:**

The geometries are in `.xyz` XMOL format. 
Each `<id>.<conf_id>.xyz` file contains Cartesian coordinates for the `conf_id`-th 
conformer of a molecule with internal id `id`.

### Molecular orbitals

**OpenADMET/ExpansionRx data**

train set: ⏳️🗜️📤️

test set: [data at kaggle](https://www.kaggle.com/datasets/oleggromov/openadmet-expansionrx-challenge-test-orbs)

**External train data (no ADMET properties)**

included in the final solution: ⏳️🗜️📤️

calculated but not used: ⏳️🗜️📤️

**External train data with ADMET properties**

included in the final solution: ⏳️🗜️📤️

calculated but not used: ⏳️🗜️📤️

**Format:**

The molecular orbitals of `rot_id`-th spatial orientation of `conf_id`-th 
conformer of a molecule with internal id `id`are stored in 
`<id>.<conf_id>.<rot_id>.zip` archives. 
Each zip-archive will contain `<id>.<conf_id>.<rot_id>.xyz` file with Cartesian 
coordinates and `<id>.<conf_id>.<rot_id>.json` with PTB calculation output.
A calculation output example is give below. The values are rounded for illustrative purpose. 
Each column in the `molecular orbitals` array is a molecular orbital expanded 
in Grimme's vDZP basis set: 
```plaintext
{'HOMO-LUMO gap / eV': 17.47780448,
 'dipole / a.u.': [-0.29942028, -0.61002809, -0.40525771],
 'number of molecular orbitals': 13,
 'number of electrons': 8,
 'number of unpaired electrons': 0,
 'fractional occupation': [2.0, 2.0, 2.0, 2.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0],
 'molecular orbitals': [[-0.71, -0.00, -0.26, -0.00,  0.31, -0.00, -0.02, -0.00, -0.00, -0.00, -0.04,  0.00,  0.20],
                        [-0.05, -0.00, -0.16, -0.00, -0.09,  0.00,  0.09,  0.00, -0.00,  0.00,  0.08,  0.00, -0.06],
                        [ 0.06, -0.17, -0.52,  0.44, -0.25, -0.14,  0.17, -0.00, -0.14,  0.09, -0.06,  0.44,  0.58],
                        [ 0.04,  0.48, -0.34, -0.22, -0.17,  0.40,  0.12,  0.00,  0.07, -0.26, -0.04, -0.23,  0.38],
                        [ 0.03, -0.31, -0.26, -0.59, -0.12, -0.26,  0.09,  0.00,  0.19,  0.17, -0.03, -0.60,  0.28],
                        [-0.01, -0.04, -0.19,  0.19,  0.02,  0.03, -0.02, -0.00,  0.00, -0.10, -0.04, -0.33, -0.52],
                        [-0.01,  0.11, -0.13, -0.10,  0.01, -0.07, -0.01,  0.00, -0.00,  0.30, -0.03,  0.17, -0.35],
                        [-0.01, -0.07, -0.10, -0.25,  0.01,  0.05, -0.01, -0.00, -0.00, -0.19, -0.02,  0.45, -0.26],
                        [ 0.00,  0.02,  0.02,  0.00, -0.10, -0.25,  0.02,  0.06,  0.31, -0.34, -0.72,  0.18, -0.12],
                        [-0.00, -0.02,  0.01, -0.00,  0.03,  0.23,  0.39, -0.41, -0.06,  0.31, -0.36, -0.03, -0.34],
                        [ 0.00, -0.03,  0.01,  0.00, -0.10,  0.35, -0.26,  0.30,  0.21,  0.46, -0.30,  0.12,  0.15],
                        [-0.01, -0.00, -0.01,  0.00,  0.13,  0.02,  0.45,  0.35,  0.42,  0.03,  0.28,  0.24, -0.29],
                        [ 0.00, -0.00, -0.00,  0.01, -0.00,  0.01, -0.19, -0.42,  0.61,  0.02,  0.26,  0.35,  0.18],
                        [-0.21,  0.33,  0.20, -0.00, -0.22, -0.26, -0.05, -0.00,  0.00,  0.00, -0.08,  0.00,  0.07],
                        [ 0.04,  0.05,  0.02, -0.00, -0.29, -0.10,  0.11,  0.00,  0.00,  0.12,  0.15, -0.00, -0.26],
                        [-0.03,  0.02, -0.03,  0.02,  0.16,  0.23, -0.18, -0.17,  0.13, -0.13, -0.03, -0.20, -0.11],
                        [ 0.01,  0.01, -0.02, -0.01, -0.17, -0.01, -0.22,  0.09, -0.07,  0.27,  0.06,  0.10, -0.28],
                        [-0.02,  0.01, -0.01, -0.03,  0.18,  0.18, -0.05,  0.23, -0.18, -0.20, -0.04,  0.27,  0.02],
                        [-0.21, -0.33,  0.20,  0.00, -0.22,  0.26, -0.05,  0.00,  0.00, -0.00, -0.08, -0.00,  0.07],
                        [ 0.04, -0.05,  0.02,  0.00, -0.29,  0.10,  0.11,  0.00,  0.00, -0.12,  0.16, -0.00, -0.26],
                        [-0.01, -0.02, -0.03,  0.02,  0.00, -0.14, -0.24,  0.17,  0.13, -0.07,  0.02, -0.20, -0.23],
                        [-0.04, -0.02, -0.02, -0.01,  0.28, -0.26, -0.06, -0.09, -0.07,  0.31, -0.07,  0.10,  0.05],
                        [ 0.01, -0.01, -0.01, -0.03, -0.10, -0.00, -0.15, -0.23, -0.18, -0.17,  0.04,  0.27, -0.19]],
 'method': 'PTB'}
```

### Molecular properties

**General molecular properties**

file: `mol_endpoints.zip`

`id`: internal molecule id, a BLAKE2b hash of molecules canonical SMILES

`num_shell_el`: the number of shell electrons

`num_core_el`: the number of core electrons

`vol_av`: molecular volume, weighted average over conformers 

`surf_av`: molecular surface, weighted average over conformers

`Rg_av`: gyration radius, weighted average over conformers

**Conformer-specific molecular properties**

file: `conf_endpoints.zip`

`id`: internal molecule id, a BLAKE2b hash of molecules canonical SMILES

`conf_id`: conformer id

`PTB_dipole_au`: molecular dipole from PTB calculation, a.u.

`PTB_homo_lumo_eV`: HOMO-LUMO gap from PTB calculation, eV

`xTB_E_Eh`: total energy from xTB caclulation, Eh

`vol`: molecular volume

`surf`: molecular surface

`Rg`: gyration radius

`Ellips1`:

`Ellips2`:

`Ellips3`:

`rel_conf_E_kJ`: relative enegrgy of a conformer with respect to the lowest energy conformer

**Spatial orientation-specific molecular properties**

file: `rot_endpoints.zip`

`id`: internal molecule id, a BLAKE2b hash of molecules canonical SMILES

`conf_id`: conformer id

`rot_id`: molecule rotation (as a whole) id, i.e. two different rot_id's are the same conformer of the same molecule but differently oriented

`PTB_dipole_x_au`: x-th component of the molecular dipole from PTB calculation, a.u.

`PTB_dipole_y_au`: y-th component of the molecular dipole from PTB calculation, a.u.

`PTB_dipole_z_au`: z-th component of the molecular dipole from PTB calculation, a.u.

### Methods

The general idea is outlined in the [JCTC paper](https://doi.org/10.1021/acs.jctc.5c00425). 
The description of the particular workflow used here is underway. 

### Data stats

Molecules: 30,653

Conformers: 209,305

Wavefunctions: 1,046,535

Compute: ~2300 CPUh


