# Accurate Calculation of the Thermal Conductivity of Liquids from Molecular Dynamics Using a Heat Flux Decomposition Based Correction

This repository accompanies the research paper

**"Accurate Calculation of the Thermal Conductivity of Liquids from Molecular Dynamics Using a Heat Flux Decomposition Based Correction"**

---

## Repository Contents

This repository contains LAMMPS data files with all FF parameter details, all LAMMPS input scripts, post processing scripts, and a jupyter notebook for model development
and testing related to the study. Below is a breakdown of the key folders and files:

### 1. LAMMPS Data Files
- `LAMMPS_Data_Files` folder containing all LAMMPS data files for initial NPT simulations.


### 2. LAMMPS Simulation Input Scripts
- Located in the `LAMMPS_Input_Scripts` folder.
- Includes:
  - `in.lmp.DIR_INDEX_NPT.txt` for NPT simulation to obtain average densities at a given state point for a given system
  - `in.lmp.DIR_INDEX_HeatFluxDecom.txt` for reshaping the cubic simulation box into a cuboid box and then performing NEMD simulations with heat flux decomposition.
  - The outputs of `in.lmp.DIR_INDEX_HeatFluxDecom.txt` contain the instantaneous heat fluxes as described in the reference paper. Time averaging the intantaneous heat fluxes (post equilibration) and dividing by the imposed heat flux gives the fractional heat fluxes Q'


### 3. Postprocessing Scripts
- Located in the `Postprocessing_scripts` folder. Contains `ave_Vol.py`, `datafile_edit_avedensity.sh`, `thermal_sim_extract.py`, and `thermal_cond_finalcalc.py`. 
- After running `in.lmp.DIR_INDEX_NPT.txt`, use `ave_Vol.py` to determine point of equilibration and obtain average densities for use in subsequent simulations
- After `ave_Vol.py`, use `datafile_edit_avedensity.sh` to modify the data file from running `in.lmp.DIR_INDEX_NPT.txt` to obtain a data file with correct average density
- Use `thermal_sim_extract.py` to extract the required data from some of the outputs of `in.lmp.DIR_INDEX_HeatFluxDecom.txt`, for use in computing $\lambda$
- Use `thermal_cond_finalcalc.py` to compute NEMD values of $\lambda$ from output of `thermal_sim_extract.py`

### 4. Jupyter notebook for computing fractional heat fluxes, training and evaluating HFD-BC model and making final plots
- Located in `Jupyter_Notebook_Final_Plots` folder
- Includes:
  - `data_tc_hfd_all.xlsx` and `TC_HFD_Corr_Final_Feb2026.ipynb`
 
### 5. Sample Results and Outputs from running the scripts in this repo.

---

## Citation
If you use the code or data herein, please cite the corresponding paper.

---

Feel free to open an issue or pull request if you have questions, suggestions, or contributions!



