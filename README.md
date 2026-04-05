# Temporal Coupling of Neural and BOLD Dynamic States Revealed by Simultaneous Resting-State EEG-fMRI

This repository contains data and code I used for analysis.

## Dataset

OpenNeuro ds006040: https://openneuro.org/datasets/ds006040/versions/1.0.1

- Original dataset informations
  - 28 Korean subjects
  - 19~42 years old
  - Consists of following tasks:
      - Resting-state / Eyes Closed
      - Resting-state / Eyes Open <-- We focused EYES OPEN RESTING-STATE 
      - checkerboard (15Hz)
      - gradCPT
      - Imagery
  - EEG data collected using 64-channel EEG system (Brain Product BrainCap MR with Multirodes)
      - Sampling rate is 5000Hz
  - fMRI data collected using 3T MRI scanner (Siemens Magnetom Prisma)
      - Repetition time (TR) is 2000ms
      - Length is 190 TRs
 
## Preprocessing details

ROI-wise time-series data are located in Data folder of this repository.

  - Among 28 subjects, we excluded 6 subjects: 7, 8, 11, 14, 28, 29 with interrupted signals during MRI ON period and excessive confounds in signal, probably due to movement.
  - Due to interrupted signals at the beginning and end of EEG, we found # of TRs to be removed at the beginning and the end. Maximum TRs across the subjects were removed to ensure consistency in length for both modalities.\
  - EEG underwent independent component analysis (ICA) to remove artifacts including muscle and eye movement, and line noise using MNE-Python.
  - EEG underwent source localization using eLORETA using MNE-Python.
  - Source-localized EEG time-series were filtered into the delta (1-4 Hz), theta (4-8 Hz), alpha (8-13 Hz), and beta (13-30 Hz) bands.
  - fMRI underwent motion correction, and global signal, white matter, cerebrospinal fluid signal regression.
  - ROI-wise time series extacted using 100-parcel Schaefer atlas from both modalities.

## Analysis + Code



