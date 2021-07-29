# ANDROMEDA

This directory contains the software package ANDROMEDA for exo-planet detection by Angular Differential Imaging.

CONTENTS:

- README_andromeda: this file;


- LibAndromeda: this folder contains all the sub-routines needed to run the full ANDROMEDA method, including the automatic detection and characterization module. 
The /oneralib/ subdirectory contains the routines from ONERA's in-house library that are necessary to ANDROMEDA and kindly provided by their authors. 
The /ipaglib/ subdirectory contains the routines from IPAG's in-house library that are necessary to ANDROMEDA and kindly provided by their authors. 
The /mpfitlib/ subdirectory contains the routines from ONERA's in-house library that are necessary to ANDROMEDA and kindly provided by their authors. 
The /batch/ subdirectory contains three specific batches for SPHERE-IRDIS and SPHERE-IFS for large survey processing.
The /otherfunction/ subdirectory contains other necessary functions to retrieve the companions information (if you already have these functions, you can remove this folder). 
The /template_spectrum/ subdirectory contains L-dwarf and T-dwarf templates to increase the detection capabilities for IFS data (Cantalloube et al. 2018)
The /statools/ subdirectory contains functions to make statistic on the residuals (Q-Q plots, histograms, whiteness)
The /STIMmap/ subdirectory contains functions to compute a STIM detection map after a classical speckle subtraction (e.g. PCA or LOCI)

- Example : This folder contains two data set to test ANDROMEDA
(i)   VLT/NaCo data in H-band of TYC-8979-16683-1 (inside folder '/Data_TYC8979/'), as well as a result folder ('/Results_TYC8979/') including the given results (in the subdirectory '/GivenResults/') that you should obtain by running the IDL-batch ('batchANDROMEDA_TYC8979.pro').  
    Inside these images, 15 synthetic planets have been injected (via G. Chauvin procedure at IPAG - see Chauvin et al. 2012) of known position and flux (3 separations in 5 rows of same flux - see attached User Manual).
(ii)  VLT/SPHERE-IRDIS data in K1K2 bands of HR8799 (from SVT, see Zurlo et al. 2015). The batch contains two calls, one for ADI only and one for SADI ('batch_sphere_hr8799.pro').
(iii) VLT/SPHERE-IFS data in YJ bands of 51Eri (from SHINE, see Samland et al. 2017). There are 2 batch, one for ADI only and one for SADI.


- Papers: This folder contains the first paper which theoretically describes the ANDROMEDA algorithm (Mugnier et al. 2009) and the second paper which describes its application on real on-sky data (Cantalloube et al. 2015). 
    Link_PhD_thesis_Cantalloube_2016.txt contains a link toward the PhD thesis including loads of test and explanation about ANDROMEDA.
    Demo_Andromeda_20170301.pdf contains old version demo explanation of the ANDROMEDA pacakge.
    SlideANDROMEDA.pdf is a one-slide summary of ANDROMEDA.


- UserManual: Describes the input and output of the functions and gives tips on how to solve common bugs that could appear. 
It is also recalled in this document the main principle pf the algorithm and how to read the output provided by the automatic detection module.
Note: the latter must be updated.


***IMPORTANT INFORMATION TO RUN ANDROMEDA:***
Libraries astrolib_dec09 (or newer versions) and coyote are required ! 
The other functions needed are native functions from exelvis/IDL85.
To add the andromeda library in the path please add the following in your IDL startup: 
!PATH = !PATH + ':' + expand_path('+/YourFolder/ANDROMEDA/LibAndromeda') + ':' + !PATH 


The input needed are the following :
	1-Reduced cube of images (clean) - centered between 4 pixels.
	2-The reference PSF (non-coronagraphic/off-axis or unsaturated image of the target star) - centered between 4 pixels.
	3-The parallactic angles corresponding to the image cube. NB: ANDROMEDA gives the results with respect to the 1st image. 
	4-The oversampling factor: It is computed knowing the pixel scale, the wavelength used and the telescope diameter.

The following input are needed to retrieve the photometry of the detected point source (if images above are not normalized):
	1-DIT_IMG is the exposure time of each images from the cube.
	2-DIT_PSF is the exposure time of the star PSF, non-coronagraphic or non-saturated exposure.
	3-Tnd is the TRANSMISSION of the neutral density if one used to image the star PSF (ie: For a transmission of 90%, Tnd=0.9).



The first version of this package has been made at IPAG, on January 2016.


Enjoy! :-)


F. Cantalloube, D. Mouillet and L. Mugnier


*********************************************************
History:

*2016/01/21 - ANDROMEDA_Package_v1.0 (IPAG/guepard)
-> Initial version of the package
-> UserManual not included yet

*2016/02/02 - ANDROMEDA_Package_v1.1 (IPAG/guepard + Vortex team)
-> CENTERING_MAX.PRO: Fixed, now functionnal
-> ANDROMEDA.PRO: angles_input direction modified inside the function
-> in /Examples/, add batch_sphere.pro and batch_sphere_SDI.pro 

*2016/02/17 - ANDROMEDA_Package_v1.2 (IPAG/guepard + Vortex team + Onera/DOTA-HRA)
-> Functions are fully versionned from Onera
-> UserManual 1st version released

*2016/10/01 - ANDROMEDA_Package_v1.3 (IPAG/guepard + Vortex team + Onera/DOTA-HRA)
-> DETECTION_ANDROMEDA.PRO: Modified to obtain the correct window sizes

*2017/03/05 - ANDROMEDA_Package_v2.0 (MPIA/PSF + IPAG + Vortex team + Onera/DOTA-HRA + ESO)
-> Several modifications in line with collaborators need.
-> The main modification affect the procedure detection_andromeda and detection_limit (keywords and display).
-> A specific LibAndromeda/batch/ subfolder is added to automatically post-process images reduced by the SPHERE-DC.

*2017/05/05 - ANDROMEDA_Package_v2.1 (MPIA/PSF + IPAG/guepard + Vortex team + Onera/DOTA-HRA + ESO + CRAL)
-> New function SPECTRUM_ANDROMEDA.PRO which extract the most likely spectrum from IFS data (see Examples/VLT-SPHERE/Data_IFS_51Eri/)
-> Details on ergonomics for all functions and procedures

*2017/09/10 - ANDROMEDA_Package_v2.2 (MPIA/PSF + IPAG/guepard + VIP team + Onera/DOTA-HRA + ESO + CRAL)
-> DETECTION_ANDROMEDA.PRO: Fixed the astrometry uncertainties (used to be over-estimated)
-> DETECTION_ANDROMEDA.PRO: Check the defaults and overall parameters effect 

*2018/04/26 - ANDROMEDA_Package_v2.3 (MPIA/PSF + IPAG + VIP team + ESO)
-> ANDROMEDA.PRO: Now produces five output: snr_raw (non-normalized), snr_norm (normalized), flux, stddevflux_raw, stddevflux_norm.
-> ANDROMEDA.PRO: Automated estimation of smallest possible IWA, if IWA_INPUT is too small or absent 
-> ANDROMEDA.PRO: Keyword /FAST to process larger annuli from 20 lambda/D
-> ANDROMEDA.PRO: Keyword /MAX to estimate the flux wrt the max of the psf-reference (and not the total)
-> NORMALIZE_SNR.PRO: Normalisation procedure fixed at the outer edges
-> DETECTION_ANDROMEDA.PRO: Astrometry on non-normalized SNR map if SNR > 3 (else on normalized)
-> DETECTION_ANDROMEDA.PRO: Checked accordingly to above w/ uncertainties
-> DETECTION_ANDROMEDA.PRO: Automatic definition of dist_neighbours and size_subimages
-> New function FORCED_PHOTOMETRY.PRO for DBI data

*2018/05/09 - ANDROMEDA_Package_v3.0 (MPIA/PSF + IPAG/Exoplanet + Onera/DOTA-HRA + ESO + CRAL + LAM + ROE)
-> ANDROMEDA.PRO now by default it normalizes the PSF to the max and not the total (/TOTAL is an option) 
As an output of ANDROMEDA.PRO we now have directly the contrast_map. Hence, the DIT and Tnd are now taken as an input of ANDROMEDA.PRO and not in the detection functions anymore.
Another consequence is the change in names: FLUX <-> CONTRAST for each variables.
-> NORMALIZE_SNR.PRO do not need the IWA, OWA and OVERSAMPLING inputs anymore
-> For SPHERE-IRDIS data, add a masks (in /LibAndromeda/batch/) to process the ~10 annuli close to the edge that miss half of the data due to the detector set-up.
-> ANDROMEDA.PRO now automatically computes the best IWA and OWA (not a mandatory input anymore)
-> DETECTION_ANDROMEDA.PRO, SPECTRUM_ANDROMEDA.PRO and IFS_DETECTION_LIMIT.PRO can take directly the contrast maps as an input and in that case, do not use the psf_planet_input.
-> New procedure IFS_DETECTION_LIMIT (see examples on 51 Eri data)
Please, if you use this new feature cite Cantalloube et al. (in prep)
Also, if you use the templates option, do note forget to cite the SpeX Prism library as follow:
"This research has benefited from the SpeX Prism Spectral Libraries, maintained by Adam Burgasser
at http://pono.ucsd.edu/~adam/browndwarfs/spexprism, as well as the M, L, T and Y dwarf compendium housed
at http://DwarfArchives.org and maintained by Chris Gelino, Davy Kirkpatrick, and Adam Burgasser, 
whose server was funded by a NASA Small Research Grant, administered by the American Astronomical Society."
For more info, see http://pono.ucsd.edu/~adam/browndwarfs/spexprism/library.html
As well as the two papers you can find in /LibAndromeda/template_spectrum/:
-Liu et al. 2013 for the L-dwarf template
-Gagné et al. 2015 for the T-dwarf template

*2018/05/09 - ANDROMEDA_Package_v3.1 (MPIA/PSF + IPAG/Exoplanet + Onera/DOTA-HRA + ESO + CRAL + LAM + ROE)
-> /stattools/ folder added containing procedures to test gaussianity (Q-Q plots and histograms) and whiteness (autocorrelation of the PSD) and to create ROC curves.
-> INJECT_SYNTHPLANETS.PRO: function to inject synthetic planetary companions at a given position and contrast. 
-> ANDROMEDA.PRO: bug fixed if set -angles
-> STIM_MAP.PRO: Procedure to compute the STIM-map from PCA or LOCI subtracted cubes.
-> DETECTION_ANDROMEDA.PRO: Add keyword /STIM to compute the "empirical" SNR when a STIM-map is given as an input.
-> NORMALIZE_SNR.PRO: Fix another special case
-> FITAFFINE.PRO: add output uncertainties and least-square result + compare with native IDL function LADFIT which provides the same result.
-> HIGHPASS_ANDROMEDA.PRO: modify the Fourier transform (use /OLD keyword for the old version)
-> DETECTION_ANDROMEDA.PRO: add /NaCo keyword with different constrains on the fit.
-> For the NaCo data, the Nsmooth is doubled compared to older version.
-> In batch/: Add keyword /REJECT (you must give an array as input with index -in ds9- of frames to be rejected)
To avoid error, the files are checked before opening.

*2020/01/15 - ANDROMEDA_Package_v3.2 (MPIA/PSF + IPAG/Exoplanet + Onera/DOTA-HRA + ESO + CRAL + LAM + ROE + DRT-SPHERE + Exeter Uni)
-> In batch/: Add keyword /INVANGLES to run ANDROMEDA with the inverse parallactic angles (useful for detection limits)
-> SPECTRUM_ANDROMEDA.pro: Add userposition_input to extract the spectrum at any user-defined position
-> L1norm keyword for robust estimation of the flux

