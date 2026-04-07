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
          - For EEG, xx_desc-anc0qrsrm_xx : QRS artifacts removed (done by data provider) was used. 
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

  - Among 28 subjects, we excluded 6 subjects: 7, 8, 11, 14, 28, 29 with interrupted signals during MRI ON period and motion artifacts.
  - Due to interrupted signals at the beginning and end of EEG, we found # of TRs to be removed at the beginning and the end. Maximum TRs across the subjects were removed to ensure consistency in length for both modalities.
  - EEG was resampled to 250 Hz for initial cleaning and finally to 50 Hz for source analysis. A 60 Hz notch filter and a 1 Hz high-pass filter (for ICA) were applied. Data were re-referenced to a Common Average Reference (CAR).
  - Independent Component Analysis (ICA) was performed (15 components) to manually identify and remove remaining eye movement, ECG, and muscle artifacts. A moving average detrending (10s window) was applied to the cleaned signal.
  - Cortical sources were estimated using eLORETA based on the fsaverage template. A 3-layer BEM model and an ad-hoc noise covariance matrix were utilized.
  - Time-series were extracted from 100 ROIs of the Schaefer atlas. The source-localized signals were band-pass filtered into Delta (1-4 Hz), Theta (5-8 Hz), Alpha (8-12 Hz), and Beta (13-24 Hz). Note: The Beta band was capped at 24 Hz to respect the Nyquist limit of the 50 Hz sampling rate.

## Analysis + Code



