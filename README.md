# CESM2.1-SCAM-RCE

## Background
The Single Column Atmosphere Model (SCAM) is a single column model version of the Community Atmosphere Model (CAM). The overview and application of SCAM can be found in [Gettelman et al. (2019)](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2018MS001578).

<br/>

## Running SCAM RCE in CESM2.1
1. Get the code of [CESM2.1](https://escomp.github.io/CESM/versions/cesm2.1/html/downloading_cesm.html) and put it wherever you like (hereafter [CESMDIR]), and check [how to run SCAM](https://www.cesm.ucar.edu/models/simpler-models/scam/index.html) in CESM2.
2. Download [InputFiles](https://drive.google.com/drive/folders/1bqDhl-QVqwJ8yAXcvm1pQ6LY22HumSti?usp=sharing) and put it wherever you like (hereafter [INPUTDIR])
3. Copy both **scam5\_rcemip** (in **SCAM5** directory) and **scam6\_rcemip** (in **SCAM6** directory), which are the RCE modified source code for SCAM5 and SCAM6, respectively, to [CESMDIR]/components/cam/cime_config/usermods_dirs/.
4. In **SCAM5** or **SCAM6** directory, edit the shell script **scam\*\_rcemip\_single** (for a single run) or **scam\*\_rcemip\_loop** (for simultaneously multiple runs or parameter sweep experiments). Particular focuses include:
   * the job setting information such as project account, timewall, and queue;
   * the machine and compiler;
   * the paths of [CESMDIR], [INPUTDIR], [CASEDIR] (where the run case and output should be), and [MODSDIR] (where the modified source code sits - basically the path mentioned in 3);
   * the names of run case [CASENAME] and baseline run [BASECASENAME] when using **scam\*\_rcemip\_loop**;
   * the run case setting, including number of vertical levels [NL], time step [DT], sea surface temperature [SST], and period of simulation [LT];
   * the customized setting such as output fields.
5. Execute the modified shell script **scam\*\_rcemip\_single** or **scam\*\_rcemip\_loop**.

The [InputFiles](https://drive.google.com/drive/folders/1R5Ft5n3R49048YFHD8RwYDntCwYMD-X3?usp=sharing) folder includes all the required input data files and can be categorized into several different groups:
* **SST\*.nc**: uniformly global SST data, currently with three SST values – 295, 300, and 305 K – as required in RCEMIP.
* **\*init\*.nc**: initial condition files which have uniformly global data of state; can choose either RCEMIP analytical profiles or RCEALT (ALTernative) profiles.
* **\*iop\*.nc**: IOP data files which carry the same data of state as in the corresponding **\*init\*.nc** files; the current available running period is 1200 days (can easily be extended).
* **\*solar\*.nc**: these files are basically used to fix the solar constant to 551.58 W/m2; the one with "CAM6" is for SCAM6.
* **RCEMIPozone\*.nc**: the analytical ozone profile following RCEMIP protocols; the "L26" and "L32" are for SCAM5 and SCAM6, repsectively.
* **aero\_zero.nc**: this one is used to zero all the aerosol fields in SCAM5.

Additionally, there is this **NCLscripts** directory, which includes all the NCL scripts for generating **\*init\*.nc**, **\*iop\*.nc**, and **RCEMIPozone\*.nc**.

<br/>

## Details of the SCAM-RCE configuration
The current SCAM-RCE configuration in CESM2.1.0 is based on the RCEMIP protocols in [Wing et al. (2018)](https://gmd.copernicus.org/articles/11/793/2018/), along with additional modifications as options. The RCEMIP protocols and their corresponding parts of modified code in CESM2.1.0 are descibed in [RCEMIP_SCAM5&6_CESM2.pdf](https://github.com/ihursmas/CESM2.1-SCAM-RCE/blob/main/RCEMIP_SCAM5%266_CESM2.pdf).
 
