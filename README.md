# Model-Validation - eos6oli

# Model Abstract
This repository contains all codes and datasets used for the validation of eos6oli model. This is the selected model used for predictions in the Model Bias and Reproducibility for the Outreachy contributors 2024. 
This model focuses on implementation of the SolTranNet tool utilizing the molecular transformer to predict aqueous solubility of compounds, an important property for drug discovery using a molecule's SMILES representation as input.

# Repository organisation
The repository is organised in folders:
- '/data' contains all the aqsol.csv file used for predictions and figures.
- '/figures' contains the plots I have produced during the model validation process
- '/notebooks' contains the jupyter notebooks where predictions were made
- '/src' contains important functions I will use throughout the repository, to avoid typing them each time
- 'requirements.txt' lists all the required packages to run the notebooks in this repository.

# Model Characteristics
- Input: Compound
- Input shape: Single
- Task: Regression
- Output: Experimental value
- Output shape: Single (Predicted log of solubility of the compound)

# Installation Process
Getting Started:
Tested on Ubuntu 18.04.5, Ubuntu 20.04.2, Debian 10, Fedora 33, CentOS 8.3.2011, Windows 10, and Ubuntu 20.04.2 subsystem for Windows 10

1. First, install [RDKit](https://github.com/rdkit/rdkit). Installation instructions are available [here](https://github.com/rdkit/rdkit/blob/master/Docs/Book/Install.md)

2. After RDKit has finished installing, you can install SolTranNet via pip:
```
python3 -m pip install soltrannet
```
NOTE: This installation method often mismatches installation of PyTorch for enabling CUDA if it needs to install PyTorch as a dependency.

3. If you wish to do a more careful installation:
```
python3 -m pip install --install-option test soltrannet
```
This will run our unit tests to ensure that GPU-enabled torch was setup correctly, and the proper functioning of SolTranNet as a command line tool and within a python environment.


# References
[Publication](https://pubs.acs.org/doi/10.1021/acs.jcim.1c00331)

[Soltrannet](https://github.com/gnina/SolTranNet)

[Soltranet Datasets and Figures Generations Repository](https://github.com/francoep/SolTranNet_paper)

[Ersilia Google Colab Guide](https://github.com/ersilia-os/ersilia/blob/master/notebooks/ersilia-on-colab.ipynb)
