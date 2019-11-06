# Intarsis GMTSAR Automatic Processing workflow

These programs generate an automatic processing flow to monitor zones by applying GMTSAR SBAS routine.

Run inside a folder with the following required input files:
- dem.grd: Dem for the region of interest. You can download it from https://topex.ucsd.edu/gmtsar/demgen/ . Altitudes must be in WGS84 heights (ellipsoidal heights). GMTSAR can use higher resolution DEMs but it must be in EPSG:4326 and netCDF format.
- SAFE_filelist: File with full path to the SLC files to use. The zips must be uncompressed in \*SAFE folders. The SLC can be outside of processing folder.
- pins.ll: File with the coordinates of the region of intererest.
- batch_tops.config: file with interferogram parameters. You can modify it with the appropiate parameters for your site.

Optional files
- Intarsis.config: (recommended) configuration file with some parameters for the automatization of the processing.
- orbits.list: list of orbit files. If it is not provided the gmtsar will download from ASF. But if the machine does not have Internet access or ASF server is down it can be provided and Intarsis will use.


# Description of the routines:
## Intarsis_00_run_all
Routine to run all steps from 01 to 06. It will log everything in intarsis.runall.log. The parameters must be configured via intarsis.config.
## Intarsis_01_file_preparation
This program check all the input files, creates the folder structure and cut the SLC acording to the pins.ll file.
## Intarsis_02_allign
This program does the corregistration for each Interferometric Swath. You must input the desired swath (F1,F2 or F3) as parameter and the master master date (or create a master_image file).
## Intarsis_03_intf
This program generates the interferograms, using "parallel" (check that is installed in your system).
## Intarsis_04a_merge
(Optional step) Merge two or three swaths together before the unwrap
## Intarsis_04b_mask
(Optional step) Creation of a coherence mask to speedup unwrap step.
## Intarsis_05_unwrap
Unwrapping of the phase.
## Intarsis_06_sbas
Generates intf.tab and scene.tab files for SBAS and runs the code
## Intarsis_09_reset_*
Some routines to remove some steps if you want to redo it.


# Other tools
## Sentinel1_orbit_downloader (https://github.com/krasny2k5/sentinel1_orbit_downloader)
This program will download the orbit archive from ESA Sentinel-1 QC server and store in the same folder as the program. It is recommended to speed up the processing since it is faster than download the fil from asf server, however the orbit archive is quite big (about 15Gb as Dec 2019).

## update_gmt5sar
Small script to download, compile and install GMTSAR. It is recommended for updates, not for initial installation because the first compilation can have unmet depedencies problems.
