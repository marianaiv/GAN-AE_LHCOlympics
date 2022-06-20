<h1 align="center">GAN-AE for LHC Olympics 2020</h1>

> GAN-AE code used for [Mariana Vivas' project](https://github.com/marianaiv/benchtools). For the original repository go to [this link](https://github.com/lovaslin/GAN-AE_LHCOlympics).

# Instructions to reproduce results
## Pre-processing datasets
To pre-process the data follow the instructions given [in this link](https://gitlab.cern.ch/idinu/lhc-olympics-preprocessing). However, some changes were made to [payload.py](https://gitlab.cern.ch/idinu/lhc-olympics-preprocessing/-/blob/master/payload.py) for it to work:
- Line 43: Delete the if statement to force the code to go through that path (I just used labeled data). Unindent line 44.
- Line 52 to 63: Comment or delete.
- Line 82 and 90: Delete the `if 'signal'` statement. Unindent lines 83 and 91.

Also, [preprocessing.py](https://gitlab.cern.ch/idinu/lhc-olympics-preprocessing/-/blob/master/preprocessing.py) was configured as suggested in the [README file of the repository](https://gitlab.cern.ch/idinu/lhc-olympics-preprocessing/-/blob/master/README.md), instead of using the default configuration in the file, with `last_event_idx` 1_100_000 and 1_000_000 for the R&D and BB1 datasets, respectively. The datasets can be downloaded from:

- [R&D dataset](https://zenodo.org/record/2629073#.XjOiE2PQhEa)
- [Black Boxes and labels](https://zenodo.org/record/4536624)

The pre-processed data files can be found [in this link](  
https://onedrive.live.com/?authkey=%21APNzARJylhUVxt0&id=2C3CDD05B333D5E2%214457&cid=2C3CDD05B333D5E2)
(but here is not the pre-processed data for the BB1 file with labels. Just the R&D dataset)

## How I used the code
The code requires Python 3.6 or greater. First, clone the repository and enter:
```
git clone 
```
Then, create a virtual enviroment from the eviroment.yml file using conda and activate it..
```
conda env create -f environment.yml
conda activate GAN-AE
```
Pre-process the data, or download it. Put it in a folder named `data`. To create the folder using the command line:
```
mkdir data
```
Train the model.
```
python train.py
```
To apply the trained model to the RnD dataset:
```
python apply.py
```
To apply the trained model to the BB1 dataset with labels:
```
python applybyme.py
```
The BumpHunter algorithm is not applied in this implementation. The aim is to get the mean ecludian distance of the classification to obtain metrics like the ROC curve. 
