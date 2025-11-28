---
title: CON²PHYS
icon: fas fa-wave-square
order: 4
toc: true
---

## Sections

- [Overview & goals](#overview--goals)
- [Brainhack format](#brainhack-format)
- [Dataset](#dataset)
- [Questions & tasks](#questions--tasks)
- [How to prepare](#how-to-prepare)

---

## Overview & goals

This year's Pre-COSYNE Brainhack is inspired by CON²PHYS (CONceptual CONsistency in electroPHYSiology).
This project stems from the convinction that systems neuroscience shows signs of conceptual fragmentation: terms like "representation" or "functional
connectivity" are central to our research, yet their meanings shift across subfields and labs. Do these differences
make a difference? That's the question that CON²PHYS sets out to answer.
CON²PHYS is a collaborative meta-science experiment that quantifies how differences in implementation, from concept to code, affect results in concrete ways. 
Its goal is to reveal how the many arbitrary algorithmic and parameter choices involved in operationalizing concepts such as "spike-spike correlations",
"functional connectivity", or "dimensionality" can lead to divergent outcomes. Participants will analyze the same
electrophysiology dataset and, using their own methodological assumptions, answer a set of deliberately underspecified multiple-choice questions
that map to core systems neuroscience concepts. The approach is designed to simulate how the
community would implement these concepts in a real research setting.

## Brainhack format

In this year's pre-COSYNE brainhack, you will answer 4 of the 15 questions that are part of CON²PHYS, using the exact same data as the full project. 
You'll work in teams of 3–4, balanced in terms of prior electrophysiology experience and coding skills. During the hackathon, there will be presentations
given by Research Software Engineers (RSEs) on how to increase reproducibility of our science with better and more standardized code.
The goal is not necessarily to "find the right answer", but to take stock of the (potential) lack of consensus that might emerge and, through
active discussion, try to find practical ways on how to address this issue.

## Dataset

The dataset consists of 18 compressed files, each corresponding to one of the 18 mice included in the dataset.
The data includes single-unit activity (SUA) and local field potentials (LFP) recorded using a Neuropixels probe during a behavioral task.
Task details and electrode placements are intentionally kept minimal to reduce biases and minimize workload. 
The data has been collected from 3 simultaneously recorded brain areas.
Every recording includes LFP (≥20 channels) and SUA (≥5 units, total of 1449 units) signals from each brain area.
The length of the recordings varies between 55 and 101 minutes.

For each mouse, the following data is provided:  

- 📋 [Trial Data](#trial-data)
- 🧠 [Brain Area](#brain-area)
- ⚡ [Spikes](#spikes)
- 🔍 [Clusters](#clusters)
- 🌊 [Waveforms](#waveforms)
- 🌀 [Local Field Potentials (LFP)](#local-field-potentials-lfp)

---

#### Trial Data (`.xlsx`) {#trial-data}

A spreadsheet containing trial-specific information, all aligned with the ephys data:
- **`trial_start`** (s): Trial onset.
- **`stim_start`** (s): Stimulus presentation.
- **`outcome`** (s): Reward or punishment time.
- **`trial_end`** (s): Trial conclusion (the trial length is variable).
- **`Variable A`**: Binary qualitative behavioral variable.
- **`Variable B`**: Binary qualitative behavioral variable.
- **`Variable C`**: Qualitative behavioral variable (1–3).

---

#### Brain Area (`.npy`, `.mat`) {#brain-area}

- **`[1 × num_units]`** array with integer values (1–3), indicating the brain area in which a unit has been recorded.  
- **`[1 × num_units]`** array with integer values for cluster IDs.  

---

#### Spikes (`.npy`, `.mat`) {#spikes}

- **`[1 × num_spikes]`** array with spike times (s).  

---

#### Clusters (`.npy`, `.mat`) {#clusters}

- **`[1 × num_spikes]`** array linking each spike to a cluster ID.  

---

#### Waveforms (`.npy`, `.mat`) {#waveforms}

- **`[num_units × 128]`** array of average waveforms for each unit, recorded at 30 kHz on the best detection channel.  
- The order of waveforms matches that of cluster IDs and brain areas in `brain_area`.  

---

#### Local Field Potentials (LFP) (`.npy`, `.mat`) {#local-field-potentials-lfp}

- `lfp1`, `lfp2`, `lfp3` each contain `[num_channels × timestamps]` arrays of LFP signals.  
- The number of channels varies from brain area to brain and from mouse to mouse. The minimum number of channels per brain area is 20.  
- Channels within a brain area are contiguous in space, but channels from different brain areas are not.  
- Channels within a brain area are ordered from the deepest to the most superficial with respect to the brain surface.  
- The dataset comprises one channel every two that have been recorded on the Neuropixel probe. The vertical spacing between recording sites is 20µM  
- The signal has been recorded with an external reference and has already undergone a preprocessing pipeline.  
- Sampling rate: 500 Hz.  


## Questions

In this hackathon, you will work on four questions of the fifteen that make up the full CON²PHYS project.\
For each question, you will:
- choose one categorical answer from the options below  
- briefly describe your analysis  
  (inclusion/exclusion criteria, analysis steps, statistics, and any key results)  

---

**Which brain area (if any) has the highest density of ripples (i.e. "hippocampal" ripples traditionally occurring during sharp wave-ripples)?**  

- Brain area 1  
- Brain area 2  
- Brain area 3  
- Not enough data / no differences  

---

**In which brain area are pairwise spike train interactions strongest at the 100 ms timescale?**  

- Brain area 1  
- Brain area 2  
- Brain area 3  
- Not enough data / no differences  

---

**Which brain area pair has the strongest directed functional connectivity?**  

- Brain area 1 ⇒ Brain area 2  
- Brain area 3 ⇒ Brain area 2  
- Brain area 3 ⇒ Brain area 1  
- Not enough data / no differences  

---

**During which trial segment is variable C best decoded?**  

- Trial start ⇒ Stim start  
- Stim start ⇒ Outcome  
- Outcome ⇒ Trial end  
- Not enough data / no differences  

## How to prepare

Download and unzip the dataset before the hackathon. 
This is crucial: time for answering the questions will be limited, 
and you do not want to waste it downloading or unpacking data during the event.
Set up your coding environment in advance (see below).

#### Data and code

- Data (Python format, ~29 GB) is here XXX  
- Data (Matlab format, ~29 GB) is here XXX  
- Python code snippets to check that you downloaded and unzipped the full dataset correctly,  
  and to load / trialize the data, are here XXX  



#### Coding environment (suggested setup)

You are free to use any coding environment you prefer during the hackathon  
(e.g. your usual Python or Matlab setup).  

The configuration below is only a suggestion.  
It provides a ready-to-use Python environment with Anaconda / Miniconda,  
ensuring that the example notebooks run smoothly.  



#### Python environment

1. Install **Miniconda / Anaconda**  

   https://www.anaconda.com/download  

2. Create the environment using the provided `environment.yml` file:  

   ```conda env create -f environment.yml```
   
3. Check that everything runs correctly by starting Jupyter and opening the example notebooks.

For electrophysiological data analysis, you are welcome to use your favourite packages and pipelines. 
If you have never done it before, we recommend installing these packages:
- neurodsp (pip install neurodsp) digital signal processing toolbox (for neural time series)
- mne (pip install mne) digital signal processing toolbox (for neurophysiological data)
- pynapple (pip install pynapple) general neurophysiological data analysis
