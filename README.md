# physiological-synchrony-empatica

## Project Overview
This project contains code and documentation for processing and analyzing physiological data collected using the Empatica EmbracePlus wearable in a study of interpersonal motor synchrony.

## Repository structure
physiological-synchrony-empatica/
│
├── README.md
├── data/
├── code/
├── results/
├── docs/

## Current Status
This repository is currently a project skeleton, as this project and associated data and code are currently in development. 

## Data
Physiological data are collected using the Empatica EmbracePlus wearable. The wearable provides physiological measures including:
- heart rate and inter-beat interval (IBI)
- electrodermal activity (EDA)
- skin temperature
  
## Planned Analysis
The analysis will focus on physiological synchrony between participants and an experimenter during a joint drumming task. 
The pipeline includes:
1. Importing Empatica EmbracePlus data from wearables
2. Organizing data by participant, experimenter, and experimental condition (synchronized or control condition)
3. Quality control/identifying artifacts
4. Preprocessing physiological signals
5. Signal normalization
6. Quantifying physiological synchrony
7. Visualizing physiological synchrony
8. Conducting statistical analyses (including windowed cross-correlations)

### Preliminary parameters for analysis are:
- window size: 8 seconds
- step size: 2 seconds
- maximum lag: ± 4 seconds
- lag increment: 250 ms
- HR resampling: 4 Hz
- z-scoring
- These preliminary parameters may be revised as we develop this project.

## Future code and associated folders will include:
- Empatica wearable data import
- physiological signal preprocessing
- quality control
- HR/IBI processing
- windowed cross-correlations
- physiological synchrony metrics/analysis
- visualization
- statistical analyses
  
- Sample code and toolkit are provided by https://github.com/jack-fogarty/LOTUS
- example files may include: "participant_info.csv"; "experimental_condition.csv"; "EDA.csv"; "HR.csv"; "TEMP.csv"

## Sample Data
- sample datasets will be used to work on preliminary code.
- sample data for development and testing are provided by Empatica https://www.empatica.com/digital-resources. 

## Data Privacy
Raw participant data or other confidential materials will not be uploaded to GitHub. The repository will only include analysis scripts, code, and research outputs (e.g., tables, figures) as the project progresses.
