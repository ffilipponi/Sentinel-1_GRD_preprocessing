# Sentinel-1 GRD preprocessing

## Introdution
Standard workflow for the preprocessing of Sentinel-1 GRD satellite data. The workflow is a 'xml' processing graph to process Sentinel-1 GRD using the command line graph processing framework in SNAP software. Sentinel-1 GRD products can be spatially coregistered to Sentinel-2 MSI data grids, in order to promote the use of satellite virtual constellations by means of data fusion techniques. Optionally a speckle filtering can be applied to the input image.

## Features
The preprocessing workflow consists of seven processing steps, it applies a series of standard corrections:
* Apply Orbit File
* Thermal Noise Removal
* Border Noise Removal
* Calibration
* Speckle filtering (optional)
* Range Doppler Terrain Correction
* Conversion to dB

## Examples
The processing graph can be run from command line using the SNAP GPT.

Here are some examples of command line
```
# Process to 20 m without speckle filtering
gpt S1_GRD_preprocessing.xml -Presolution=20 -Porigin=10 -Pfilter='None' -Pdem='SRTM 3Sec' -Pcrs='GEOGCS["WGS84(DD)", DATUM["WGS84", SPHEROID["WGS84", 6378137.0, 298.257223563]], PRIMEM["Greenwich", 0.0], UNIT["degree", 0.017453292519943295], AXIS["Geodetic longitude", EAST], AXIS["Geodetic latitude", NORTH]]' -Pinput=S1A_IW_GRDH_1SDV_20160228T051920_20160228T051956_010142_00EF52_AB5E.SAFE -Poutput=S1A_IW_GRDH_1SDV_20160228T051920_20160228T051956_010142_00EF52_AB5E.dim

# Process to 10 m with 'Refined Lee' speckle filtering
gpt S1_GRD_preprocessing.xml -Presolution=10 -Porigin=5 -Pfilter='Refined Lee' -Pdem='SRTM 3Sec' -Pcrs='GEOGCS["WGS84(DD)", DATUM["WGS84", SPHEROID["WGS84", 6378137.0, 298.257223563]], PRIMEM["Greenwich", 0.0], UNIT["degree", 0.017453292519943295], AXIS["Geodetic longitude", EAST], AXIS["Geodetic latitude", NORTH]]' -Pinput=S1A_IW_GRDH_1SDV_20160228T051920_20160228T051956_010142_00EF52_AB5E.SAFE -Poutput=S1A_IW_GRDH_1SDV_20160228T051920_20160228T051956_010142_00EF52_AB5E.dim
```
Description of command line options:
* -Pinput		input Sentinel-1 GRD '.SAFE' file
* -Poutput		outut Sentinel-1 GRD preprocessed file (BEAM-DIMAP format)
* -Presolution	set target spatial resolution
* -Porigin		allows to snap output grid to Sentinel-2 data grid, should be set to half the size of spatial resolution set using the 'Presolution' option
* -Pfilter		defines the speckle filter to be used (only supported speckle filters available in SNAP, 'None' does not apply any speckle filtering)
* -Pdem			set the DEM to be used for terrain correction

## References
Filipponi, F. (2019). Sentinel-1 GRD Preprocessing Workflow. In Multidisciplinary Digital Publishing Institute Proceedings (Vol. 18, No. 1, p. 11).
