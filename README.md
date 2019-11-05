# Intarsis GMTSAR Automatic Processing workflow

These programs generate an automatic processing flow to monitor zones by applying GMTSAR SBAS routine.

Run inside a folder with the following required input files:
- dem.grd: Dem for the region of interest. You can download it from https://topex.ucsd.edu/gmtsar/demgen/
- SAFE_filelist: File with full path to the SLC files to use. The zips must be uncompressed in \*SAFE folders. The SLC can be outside of processing folder.
- pins.ll: File with the coordinates of the region of intererest.
- batch_tops.config: file with interferogram parameters. You can modify it with the appropiate parameters for your site.
- Intarsis.config: configuration file with some parameters for the automatization of the processing.

# Description of the routines:
## Intarsis_00_run_all
Routine to run all steps from 01 to 06. It will log everything in intarsis.runall.log. The parameters must be configured via intarsis.config.
## Intarsis_01_file_preparation
This program check all the input files, creates the folder structure and cut the SLC acording to the pins.ll file.
## Intarsis_02_allign
This program does the corregistration for each Interferometric Swath. You must input the desired swath (F1,F2 or F3) as parameter and the master master date (or create a master_image file).
## Intarsis_03_intf
This program generates the interferograms, using "parallel" (check that is installed in your system).
## Intarsis_04_mask
Creation of a coherence mask to speedup unwrap step.
## Intarsis_05_unwrap
Unwrapping of the phase.
## Intarsis_06_sbas
Generates intf.tab and scene.tab files for SBAS and runs the code
## Intarsis_09_reset_*
Some routines to remove some steps if you want to redo it.
