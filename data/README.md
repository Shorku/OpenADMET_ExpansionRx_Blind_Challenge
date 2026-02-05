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

included in the final solution: `admet_external_train_geoms.zip`

calculated but not used: `admet_external_unused_geoms.zip`

**Format:**

The geometries are in `.xyz` XMOL format. 
Each `<id>.<conf_id>.xyz` file contains Cartesian coordinates for the `conf_id`-th 
conformer of a molecule with internal id `id`.

### Molecular orbitals

**OpenADMET/ExpansionRx data**

train set: [data at kaggle](https://www.kaggle.com/datasets/oleggromov/openadmet-expansionrx-challenge-train-mol-orbs)

test set: [data at kaggle](https://www.kaggle.com/datasets/oleggromov/openadmet-expansionrx-challenge-test-mol-orbs)

**External train data (no ADMET properties)**

included in the final solution: ⏳️🗜️📤️

calculated but not used: ⏳️🗜️📤️

**External train data with ADMET properties**

included in the final solution: ⏳️🗜️📤️

calculated but not used: ⏳️🗜️📤️

**Format:**

The molecular orbitals of a molecule with internal id `id` are stored in 
`<id>.npz` files (numpy compressed .npz format).

`connectivity` array: pairs of indexes of the connected atoms (bonded or conjugated)

`num_electrons` array: the number of the explicit electrons 

`mo_occupation_conf<conf_id>` arrays: MOs occupation numbers for the `conf_id`-th conformer

`mos_conf<conf_id>_rot<rot_id>` arrays: the molecular orbitals of `rot_id`-th spatial
orientation of `conf_id`-th conformer (in Grimme's vDZP basis set)

`atoms_conf<conf_id>` arrays: atomic numbers for the `conf_id`-th conformer

`coords_conf<conf_id>_rot<rot_id>` arrays: atomic cartesian coordinates of `rot_id`-th spatial
orientation of `conf_id`-th conformer

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

- Embed up to 25 conformers (RDKit)
- Geometry optimization (RDKit, only if MMFF94 parameters are available)
- Remove duplicates
- Geometry optimization (xTB)
- Remove high energy conformers (10 kJ/mole window)
- Remove duplicates
- Generate 5 replicas for each structure via whole molecule random rotation
- Calculate molecular orbitals (xTB, PTB parametrization)

### Data stats

Molecules: 30,653

Conformers: 209,305

Wavefunctions: 1,046,535

Compute: ~2300 CPUh


