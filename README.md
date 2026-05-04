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
  - The outputs of `in.lmp.DIR_INDEX_HeatFluxDecom.txt` contain the instantaneous heat fluxes as described in the reference paper. Time averaging the instantaneous heat fluxes (post equilibration) and dividing by the imposed heat flux gives the fractional heat fluxes Q'


### 3. Postprocessing Scripts
- Located in the `Postprocessing_scripts` folder. Contains `ave_Vol.py`, `datafile_edit_avedensity.sh`, `thermal_sim_extract.py`, and `thermal_cond_finalcalc.py`. 
- After running `in.lmp.DIR_INDEX_NPT.txt`, use `ave_Vol.py` to determine point of equilibration and obtain average densities for use in subsequent simulations
- After `ave_Vol.py`, use `datafile_edit_avedensity.sh` to modify the data file from running `in.lmp.DIR_INDEX_NPT.txt` to obtain a data file with correct average density
- Run `in.lmp.DIR_INDEX_HeatFluxDecom.txt`
- Then use `thermal_sim_extract.py` to extract the required data from some of the outputs of `in.lmp.DIR_INDEX_HeatFluxDecom.txt`, for use in computing $\lambda$
- Use `thermal_cond_finalcalc.py` to compute NEMD values of $\lambda$ from output of `thermal_sim_extract.py`
- Some of the outputs from running `in.lmp.DIR_INDEX_HeatFluxDecom.txt` include averaged instantaneous heat fluxes needed for computing fractional heat fluxes for HFD-BC

### 4. Jupyter notebook for computing fractional heat fluxes, training and evaluating HFD-BC model and making final plots
- Located in `Jupyter_Notebook_Final_Plots` folder
- Includes:
  - `data_tc_hfd_all.xlsx` and `TC_HFD_Corr_Final_Feb2026.ipynb`
  -  `TC_HFD_Corr_Final_Feb2026.ipynb` takes in some of the outputs from running `in.lmp.DIR_INDEX_HeatFluxDecom.txt` and computes the fractional heat fluxes, trains the HFD-BC model, then shows how to apply HFD-BC to other systems using the fitted parameters
  -   `data_tc_hfd_all.xlsx` contains input data for use along with `TC_HFD_Corr_Final_Feb2026.ipynb`
 
### 5. Sample Results and Outputs from running the scripts in this repo.
- Located in `Results_and_Outputs` folder


Note: For some new system, all that is needed to use the HFD-BC method is to obtain the fractional heat fluxes and NEMD computed $\lambda$ following the guidance above.
$N_H$ and $N_{non-H}$ can easily be determined by the user for their specific system. For mixtures, follow the guidance in the reference paper. 
The given all the required fractional heat fluxes, the uncorrected NEMD computed $\lambda$, $N_H$ and $N_{non-H}, the HFD-BC corrected $\lambda$ can easily be computed using equations 5 and 6 as described in the reference paper.

---

## Citation
If you use the code or data herein, please cite the corresponding paper.

---

Feel free to open an issue or pull request if you have questions, suggestions, or contributions!



