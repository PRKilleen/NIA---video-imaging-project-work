# Apex Auditor is a program designed to extract, directly from video imaging, the calcium signal amplitudes and analyse peak intervals from live heart tissue (and how they change with drug applied). Only pixels with organised activity are included.
# Cardiotographer is a program designed to display spacial arrangement of calcium signal propagation (and how it changes with drug given).
Apex Auditor:
Bespoke program for the LCS designed to produce an analysis of the signal from 'active' / 'seemingly organised' areas of SAN tissues captured with PCO camera. 'noisy' areas and non san tissue excluded automatically. Allows for multiple files (of several gb in size) to be uploaded and will concatenate the signals from them with no manual steps required.
- simple interface (uses Tkinker) to display uploaded files and allow for settings to be changed (to optimise signal detection)
- uses numpy/scipy and vectorised calculations where possible to improve performance
- first step: a mask of included pixels is created (this uses an assumption that noisy pixel signals will have a correlation that trends towards 0 - because the noise is gaussian / random. Each pixel signal is correlated with the nearby 10x10 pixel mean signal, and with even a low threshold of correlation most of the noisy pixels can be excluded; minimal filtering required for this step.)
- second step: signal (mean) is the obtained for only these pixels
- signal is cropped by first and last troughs to mitigate accidental inclusion of 'half peaks' if the PCA capture starts half way through a peak.
- default time unit is 1 slice = 1.708 ms, but this can be changed in the interface
- pixels also excluded if brightness >500; the camera paints a timestamp at top left in very bright pixels.
- third step: peaks are found within this signal using find_peaks and data printed out for these peaks; ie: signal frequency (mean cycle length) and irregularity (standard deviation cycle length) as well as violin and 'intervalogram' plots.
- sensible settings for peak detection are used as defaults, but these settings can be changed after visualisation of signal and peak detection re-run to ensure correct peaks are captured
- fourth step: signal amplitudes can be saved as a csv ; can be opened in excel or uploaded to another program for further analysis
- 
Cardiotographer:
Bespoke program created for the LCS designed to display the shape and velocity of calcium signal propagation across the mouse sino-atrial tissue.
- simple interface (uses Tkinker) to display uploaded files
- uses numpy/scipy and vectorised calculations where possible to improve performance
- once active pixels have been identified, cross-correlation analysis is used to determine the 'lag' of each pixel from the cluster signal. A blue -> red (jet) colour scheme is then used to visually paint this relationship with pixel alpha values set to normalised cross correlation coefficient of each pixel with cluster signal.
- Both the pattern and rate of propagation (/velocity) demonstrably change between mice and between drug and control
