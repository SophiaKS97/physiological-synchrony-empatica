# physiological-synchrony-empatica

## Project Overview
This project contains code and documentation for processing and analyzing physiological data collected using the Empatica EmbracePlus wearable in a study of interpersonal motor synchrony. The larger study examines whether drumming in synchrony with another person affects physiological synchrony, social affiliation, and preferred interpersonal distance in people with and without schizophrenia.

During the joint drumming task, both the participant and experimenter wear an Empatica EmbracePlus wearable on their non-drumming hand. Physiological signals will be compared between the participant and experimenter to quantify interpersonal physiological synchrony.

## Repository Structure
```text
physiological-synchrony-empatica/
├── README.md
├── requirements.txt
├── data/
├── code/
├── results/
└── docs/
```text

## Current Status
This repository is currently a project skeleton, as this project and associated data and code are currently in development. The initial goal is to develop and test a reproducible physiological synchrony pipeline using sample/public data before applying the workflow to our study data.

## Data
Physiological data are collected using the Empatica EmbracePlus wearable. The wearable provides physiological measures including:
- Heart rate (HR; bpm)
- Inter-beat interval (IBI; seconds or ms)
- Electrodermal activity (EDA)
- Skin temperature (in degrees)

HR/IBI will be the initial focus for development. EDA will be explored as a secondary measure, and skin temperature will initially be exploratory.

### Expected Data Structure
The final study data are expected to contain separate physiological recordings for participants and experimenters.
Example:
data/
├── raw/
│   ├── participant/
│   └── experimenter/
├── metadata/
│   ├── participant_info.csv
│   └── experimental_condition.csv
└── processed/

Example `participant_info.csv`:

| participant_id | group | experimenter_id | session |
|---|---|---|---|
| P001 | SCZ | E001 | 1 |

Example `experimental_condition.csv`:

| participant_id | session | condition | task_start | task_end |
|---|---|---|---|---|
| P001 | 1 | synchronized | TBD | TBD |

File names and data structures are preliminary and will be updated as the study dataset is finalized.

## Experimental Timeline
The physiological recording may include periods before, during, and after the joint drumming task. The primary analysis will focus on the predefined drumming period (30 seconds).

Baseline → Drumming begins → Drumming period → Drumming ends → Post-task

The analysis pipeline should use event/condition information to identify the start and end of the relevant analysis window rather than relying on a fixed timestamp whenever possible.

For each recording, the pipeline should preserve:
- Recording start time
- Task start time
- Task end time
- Experimental condition
- Participant ID
- Experimenter ID

## Analysis Unit
The primary unit of analysis is a participant–experimenter dyad within an experimental condition. Each dyad will have:
- One participant physiological recording
- One experimenter physiological recording
- One experimental condition
- Temporally aligned participant and experimenter recordings
- Physiological signals recorded during the joint drumming task
  
## Planned Analysis
The analysis will focus on physiological synchrony between participants and an experimenter during a joint drumming task.
The pipeline includes:
1. Importing Empatica EmbracePlus data from wearables
2. Organizing data by participant, experimenter, and experimental condition (synchronized or control condition)
3. Quality control/identifying artifacts
4. Preprocessing physiological signals
5. Signal normalization
6. Participant–experimenter temporal alignment
7. Quantifying physiological synchrony
8. Visualizing physiological synchrony
9. Conducting statistical analyses of physiological synchrony

## Signal Preprocessing

### HR/IBI
Potential steps:
1. Inspect raw values and missingness.
2. Convert timestamps to a common time base.
3. Resample to 4 Hz.
4. Identify implausible values/artifacts.
5. Interpolate short gaps where appropriate.
6. Detrend if necessary.
7. Z-score within participant.
8. Generate QC plots.

### EDA
Potential steps:
1. Inspect raw EDA signal.
2. Identify missing data and artifacts.
3. Apply appropriate filtering/smoothing.
4. Identify tonic/phasic components if appropriate.
5. Normalize within participant.
6. Generate QC plots.
   
### Skin Temperature
Initially treated as an exploratory measure. Preprocessing and synchrony analysis will be determined after inspecting the data.

## Physiological Synchrony
The initial approach for quantifying synchrony will use windowed cross-correlation (WCC). For each time window, the participant and experimenter signals will be compared across a range of temporal lags to estimate:
- Maximum correlation
- Lag corresponding to maximum correlation
- Synchrony over time
- Summary measures of physiological synchrony
  
### Preliminary WCC Parameters
- Window size: 8 seconds
- Step size: 2 seconds
- Maximum lag: ±4 seconds
- Lag increment: 250 ms
- HR resampling: 4 Hz
- Z-scoring

These preliminary parameters may be revised as we develop this project.
Alternative synchrony approaches may also be explored during development.

## First Working Analysis
The first goal is to successfully analyze one participant–experimenter dyad using one physiological signal.
The pipeline should:
1. Load participant and experimenter data.
2. Identify the drumming period.
3. Plot the raw signals.
4. Resample the signals to a common frequency.
5. Preprocess and z-score the signals.
6. Calculate windowed cross-correlations.
7. Extract maximum correlation and corresponding lag for each window.
8. Plot synchrony over time.
9. Save the window-level results as a CSV.

Once this workflow works for one dyad, it should be generalized to additional participants and experimental conditions.

## Software
The analysis will be developed in Python.
Planned packages include:
- Python 3
- pandas
- numpy
- scipy
- matplotlib
- seaborn

Python packages are listed in `requirements.txt`. Additional packages may be added as the pipeline is developed.

## Expected Outputs
The pipeline should ultimately produce:
### Processed Data
- Cleaned physiological signals
- Resampled signals
- Temporally aligned participant–experimenter signals
### Window-Level Synchrony Data
- Participant ID
- Experimenter ID
- Condition
- Signal
- Window start/end
- Maximum correlation
- Maximum lag
- Number of valid samples
- Quality-control indicators
  
### Figures
- Raw physiological signals
- Preprocessed physiological signals
- Participant vs. experimenter signals
- Physiological synchrony over time
- Lag over time
- Condition-level synchrony comparisons

## Sample Data
Sample data and resources are available through Empatica:
https://www.empatica.com/digital-resources

The LOTUS toolkit is also provided as a reference for developing physiological synchrony analyses:
https://github.com/jack-fogarty/LOTUS

## First Tasks
1. Data dictionary: Document variables, sampling rates, units, and timestamps.
2. Data exploration: Inspect sample Empatica data and identify data-quality issues.
3. Preprocessing: Develop standardized preprocessing for HR/IBI and EDA.
4. Temporal alignment: Develop a method for aligning participant and experimenter recordings.
5. Synchrony analysis: Implement and test windowed cross-correlation.
6. Visualization: Create plots showing physiological signals and synchrony over time.
7. Documentation: Document analysis decisions, parameters, and workflow.
8. Reproducibility: Develop an end-to-end pipeline that can be applied to new datasets.

## Data Privacy
Raw participant data or other confidential materials will not be uploaded to GitHub. The repository will only include analysis scripts, code, and research outputs (e.g., tables, figures) as the project progresses.
