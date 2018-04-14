# Arrythima Classification using Neural Networks

Recognizes ECG beats using an artificial neural network.

Built as a university project for a DSP course.

Uses the [MIT-BIG ECG database](https://www.physionet.org/physiobank/database/mitdb/). Currently classifies the beats into only two superclasses.

## Usage
### Prerequisites
* MATLAB
* Python3
* [The MIT-BIH Arrhythmia Database](https://www.physionet.org/physiobank/database/mitdb/)
* [WFDB Toolbox for MATLAB](https://physionet.org/physiotools/matlab/wfdb-app-matlab/)

### 1. Install dependencies
You need to get [MATLAB](https://en.wikipedia.org/wiki/MATLAB) and [Python 3](https://www.python.org/downloads/)

### 2. Download the database
[See PhysioNet for instructions on how to download the database](https://www.physionet.org/faq.shtml#downloading-databases).

__Make sure you save the records in folder named mitdb in the root directory of the project.__

### 3. Install the WFDB Toolbox
[See Physionet for instructions on downloading and installing the toolbox](https://physionet.org/physiotools/matlab/wfdb-app-matlab/).

### 4. Install Pipenv and python dependencies
First, install Pipenv using pip
```bash
pip install pipenv
```
If you don't want to use pip, see [Pipenv docs for other methods](https://docs.pipenv.org/).

Next install the project dependencies
```bash
pipenv install
```
### 5. Preprocess the data
Start matlab and navigate to the project directory.

Now choose how many samples you want to choose around each beat peak.

The variables `window_l - window_t + 1` should be equal to that value.

`window_l` values will be taken before the peak and `window_t` after the peak.

To denoise the signals and extract the beats, execute the following commands:

```matlab
window_l = 63;
window_t = 64;
dataset = prep_dataset(window_l, window_t); % This will take some time to finish
```

After the command finishes, you should find a file named `mitdb_window63_64.mat` in the project directory.

Next, you need to extract the features for the beats.
You need to choose the number of intervals the beat will be divided to when computing statistical features, this will influence the number of features. A larger number results in more features.

```matlab
statistical_intervals = 8;
extract_features(dataset, statistical_intervals); % This also takes time
```

After the command finishes, you should find a file named 
`mitdb_dataset_interv8.mat` in the project directory.

This file will be used by the python code.

### 6. Train and test the network

Open a terminal, navigate to the project directory and run:

```bash
pipenv run jupyter-notebook
```

This should open your browser, select `MIT Arrhythmia Classification.ipynb` from the page.

That's it!

## Built With
* MATLAB
* Python
* WFDB Toolbox
* SciPy
* scikit-learn
and many more...

## Acknowledgements
* [PhysioNet](https://physionet.org)
Seriously, these guys are awesome!
* [@mondejar](https://github.com/mondejar/)
Most of the data wrangling was copied from [this repo](https://github.com/mondejar/ecg_classification) and modified slightly.
* [Generic Features for Biosignal Classification](https://www.academia.edu/2768075/Generic_Features_for_Biosignal_Classification)
Ideas for features
