
# Purpose

A synthetic dataset to be used for testing of the cohort analysis pipeline in mosaic.

# Content

1. Multiple Mission Bio H5 files which were synthetically generated to cover various aspects of the cohort pipeline.
2. `demultiplex.csv` to be able to separate the samples processed together on Tapestri
3. `config.yaml` to run the pipeline. It also contains a few commented lines to show options that are available for different types on runs.

# Running the pipeline

1. Install mosaic using the installer available on the [Mission Bio Portal](https://portal.missionbio.com/)
2. Open the terminal and activate the mosaic enviroment using `conda activate <env-name>`,
   where `<env-name>` is the name of the mosaic environment.
3. Go to the directory of this dataset using `cd /path/to/dataset`
4. Run the pipeline using `tapestri tertiary cohort process --config config.yaml --output-folder ./output/ --overwrite`
