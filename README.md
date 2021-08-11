# CESM2.1.0-SCAM-RCE
## Background
## How to run SCAM RCE in CESM2.1.0?
1. Get [CESM2.1.0](https://escomp.github.io/CESM/versions/cesm2.1/html/downloading_cesm.html), whose path is hereafter [cesm2_1_0].
2. Put InputFiles wherever you like, whose path is hereafter [inputfiles].
3. Put scam_rcemip in [cesm2_1_0]/components/cam/cime_config/usermods_dirs/.
4. 

The InputFiles directory includes all the input data files and can be categorized into several different groups:
* SST*.nc: uniformly global SST data, currently with three SST values – 295, 300, and 305 K – as required in RCEMIP.
* *init*.nc: initial condition files which have uniformly global data of state; can choose either RCEMIP analytical profiles or RCEALT (ALTernative) profiles  
* *iop*.nc: IOP data files which carry the same data of state as in the corresponding *init*.ncfiles; the current available running period is 1200 days (can easily be extended).
* *solar*.nc: these files is basically used to fix the solar constant to 551.58 W/m2; the one with “CAM6” is for SCAM6.
* RCEMIPozone*.nc: the analytical ozone profile following RCEMIP protocols; the one with “L26” is for SCAM5, “L32” is for SCAM6.
* aero_zero.nc: this one is used to zero all the aerosol fields in SCAM5.

Also there is this NCLscripts directory, which includes all the NCL scripts for generating II, III, and V.
SCAM5/SCAM6 directory, in which *_single/*_loop shell scripts are used to run a single simulation/loop simulations, and the scam5_rcemip/scam6_rcemip directories include the user-modified source code for SCAM5/SCAM6. The details of modifications can be found in the attached slides (“RCEMIP_SCAM5&6_CESM2”).

## Details of the SCAM-RCE configuration
The current SCAM-RCE configuration in CESM2.1.0 is based on the RCEMIP protocols in Wing et al. (2018), along with additional modifications as options. The RCEMIP protocols and their corresponding parts in CESM2.1.0 are described as follows.
### aaa
 
