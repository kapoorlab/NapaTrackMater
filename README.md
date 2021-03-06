# NapaTrackMater
Napari Visualization tool for Trackmate > 6.0 and bTrackmate XML files for 3D + time tracks.

This repository is the bridge between the Fiji and Napari world for exporting and viewing the track XML files using [Napari track layer](https://napari.org/tutorials/fundamentals/tracks.html).

[![Build Status](https://travis-ci.com/kapoorlab/napatrackmater.svg?branch=master)](https://travis-ci.com/github/kapoorlab/napatrackmater)
[![PyPI version](https://img.shields.io/pypi/v/napatrackmater.svg?maxAge=2591000)](https://pypi.org/project/napatrackmater/)

## Installation
This package can be installed with:

`pip install --user napatrackmater`

If you are building this from the source, clone the repository and install via

```bash
git clone https://github.com/kapoorlab/NapaTrackMater/

cd NapaTrackMater

pip install --user -e .

# or, to install in editable mode AND grab all of the developer tools
# (this is required if you want to contribute code back to NapaTrackMater)
pip install --user -r requirements.txt
```

### Pipenv install

Pipenv allows you to install dependencies in a virtual environment.

```bash
# install pipenv if you don't already have it installed
pip install --user pipenv

# clone the repository and sync the dependencies
git clone https://github.com/kapoorlab/NapaTrackMater/
cd NapaTrackMater
pipenv sync

# make the current package available
pipenv run python setup.py develop

# you can run the example notebooks by starting the jupyter notebook inside the virtual env
pipenv run jupyter notebook
```

Access the `example` folder and run the cells.


## Usage

To use this repository you need to have an XML file coming either from the Fiji plugin Trackmate version>6.0 or from bTrackmate version>2.0.
Both the programs save the same XML file containing the information about your tracking session. This XML file can be used to re-generate trackscheme along with the tracks they came from, for example a typical trackscheme with tracks overlay in Fiji:


![Track Scheme](https://github.com/kapoorlab/NapaTrackMater/blob/main/Images/trackscheme.png)


In this scheme there are some cells that divide multiple times and some don't, we can view these tracks by using the tracks layer of Napari.


In Napari tracks layer view we break the dividing trajectory into components that are called tracklets. These tracklets represent the trajectory of individual daughter cell or the root cell.


More than just viewing the tracks we can extract the following special functions from them:


1) If the cells move inside a tissue we can calculate the distance of the cells in a track from the tissue boundary for the root track and the following tracklets after a division event, this gives a cell localization plot which shows the starting and the ending distance of each tracklet.
Check the [notebook](https://github.com/kapoorlab/NapaTrackMater/blob/main/examples/CellFateDetermination.ipynb).


2) If the cells had an intensity oscillation we can compute the frequency of such oscillation for each tracklet of the track by Fourier transforming the intensity over time.
Check the [notebook](https://github.com/kapoorlab/NapaTrackMater/blob/main/examples/FrequencyOscillations.ipynb).

## Example
To try the provided notebooks we provide an example dataset of C. elegans from the [tracking challenge](http://celltrackingchallenge.net/3d-datasets/), download the hyperstacks of the Raw, segmentation and the mask image from [here](https://drive.google.com/drive/folders/1-50SicoUQIxoVlH_aJyycbymICgxZyr8?usp=sharing). We created the [csv file](https://github.com/kapoorlab/NapaTrackMater/tree/main/examples/data/save) using this [notebook](https://github.com/kapoorlab/NapaTrackMater/blob/main/examples/BTrackMateLocalization.ipynb). After that we used the jar provided in [this repo](https://github.com/kapoorlab/DeepLearningTracking/blob/main/BTrackMate-2.0.0.jar) and installed it in Fiji to do the tracking of 12000 cells in 3D (after removing cells below a certain size) and kept 54 tracks. In the tracking process we automatically exculde the tracklets whose track duration is less than 10 timeframes. After that we save the xml file of the tracks. This xml file can be opened for track visualization and analysis using the notebooks provided int he example.

Now you can try either of the two notebooks provided: 

Notebook 1 ) To view the intensity oscillations of the cells, click on this [notebook](https://github.com/kapoorlab/NapaTrackMater/blob/main/examples/FrequencyOscillations.ipynb). We seperate the visualization and analysis of dividing and non-dividing trajectories, in the cell of dividing trajectories you will see the Napari tracks layer with their ID for all the dividing tracks only along with the image, segmentation and mask layers. To view the tracks you can use the time slider to see the tracks alongside the cells. To hide some of the tracks or image layers you can use the visibility toggle on the left widget of Napari. In the left down there is a trackbox widget which contains the track ids. Using this dropdown menu you can choose your trackid and display the intensity over time of all the tracklets of this track and Fourier transform (in logscale) of each tracklet showing the period of oscillation of each tracklet of the track.

![FFT Non Dividing Track](https://github.com/kapoorlab/NapaTrackMater/blob/main/Images/FFTNonDividing.png)
![FFT Dividing Track](https://github.com/kapoorlab/NapaTrackMater/blob/main/Images/FFTDividing.png)

Example of publication where such oscillations in intensity were found: Collaboration: [Ines Lahmann, Varun Kapoor, Stephan](https://europepmc.org/article/med/30862660)

Notebook 2) To view the cell localization in a track with respect to the tissue boundary click on this [notebook](https://github.com/kapoorlab/NapaTrackMater/blob/main/examples/CellFateDetermination.ipynb)
Again we divide the notebook into analysis of dividing and non-dividing tracjectories. In the plots we now show the distance of the cells in the track to the boundary and plot the starting end end distance of the parent (in green) and the daughter cells (in red).

![Distance Non Dividing Track](https://github.com/kapoorlab/NapaTrackMater/blob/main/Images/DistanceNonDividing.png)
![Distance Dividing Track](https://github.com/kapoorlab/NapaTrackMater/blob/main/Images/DistanceDividing1.png)
![Distance Dividing Track](https://github.com/kapoorlab/NapaTrackMater/blob/main/Images/DistanceDividing2.png)
## Requirements

- Python 3.9 and above.


## License

Under MIT license. See [LICENSE](LICENSE).

## Authors

- Varun Kapoor <randomaccessiblekapoor@gmail.com>
- Claudia Carabana Garcia
