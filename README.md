Intarsis GMTSAR Automatic Processing workflow

These programs generate an automatic processing flow to monitor zones by applying GMTSAR SBAS routine.

Run inside a folder with the following required input files:
- dem.grd: Dem for the region of interest. You can download it from https://topex.ucsd.edu/gmtsar/demgen/
- SAFE_filelist: File with full path to the SLC files to use. The zips must be uncompressed in \*SAFE folders. The SLC can be outside of processing folder.
- pins.ll: File with the coordinates of the region of intererest.
- batch_tops.config: file with interferogram parameters. You can modify it.
