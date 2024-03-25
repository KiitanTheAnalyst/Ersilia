# Model-Validation - eos6oli

# Aqueous solubility prediction
Fast aqueous solubility prediction based on the Molecule Attention Transformer (MAT). The authors used AqSolDB to fine-tune the MAT network to solubility prediction, achieving competitive scores in the Second Challenge to Predict Aqueous Solubility (SC2).
This repository contains all codes and datasets used for the validation of eos6oli model. This is the selected model used for predictions in the Model Bias and Reproducibility for the Outreachy contributors 2024. 
This model focuses on implementation of the SolTranNet tool utilizing the molecular transformer to predict aqueous solubility of compounds, an important property for drug discovery using a molecule's SMILES representation as input.

# Identifiers
* EOS model ID: `eos6oli`
* Slug: `soltrannet-aqueous-solubility`

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
- Output Type: `Float`
- Output shape: `Single`
- Interpretation: (Predicted log of solubility of the compound)

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
This will run unit tests to ensure that GPU-enabled torch was setup correctly, and the proper functioning of SolTranNet as a command line tool and within a python environment.

## WEEK 2
# Task 1 - Model Bias

# Step 1 - Model Selection
Going through the list of models provided , I chose the eos6oli model because I understood the aim and the methodology of the publication.

# Step 2 - Github Repository
I created a repository in my GitHub with appropriate structure containing necessary files used and results generated.

# Step 3 - Data Pre-Processing
I explored the reference_library dataset containing 1000 rows of SMILES provided by the mentor.
Then, I went ahead to standardise the SMILES using the codes provided in the src folder by importing it into my notebook by cloning my github repo.
I generated Inchikeys with SMILES using codes which I also saved in smiles_processing.ipynb file in the src folder.

# Step 4 - Model Predictions
I Installed, fetched and served the Ersilia Model Hub to ensure it is working smoothly, I ran predictions for this sample dataset. I saved the result of the predictions in output folder in the data folder in my repo.

# Step 5 - Model Bias Evaluation
I plotted an histogram plot with predicted results which reveals that most compounds have solubility values concentrated around -5.
I also generated morgan fingerprints with SMILES and used it to generate a scatterplot to display solubillity values with a threshold of 0.5. The distribution of colors around this plot indicates the Blue color as regions with prediction probability less than 0.5 which indicates low solubilty, and Red color as areas of high solubility with prediction probability equals or greater than 0.5

# Step 6 - Interpretation of Result
Model Information
In the eos6oli publication, soluble compound is defined as a compound with log S > -4, i.e., being able to obtain a 100 μM solution. Author also suggests that the model is useful at screening out insoluble compounds.

I calculated the logarithm of solubility (base 10), and the result generated shows 998 compounds with Log S values of -10, and 2 compounds with Log S value > -4. I also checked if compounds are being able to obtain a 100 μM solution, and results shows that only the 2 compounds whose Log S is > -4 are able to obtain a 100 μM solution.

# Step 7 - Conclusion
Comparing the model information with predictions generated, it can be inferred that the model is not biased from the results generated . The model was able effectively screen out 998 compounds that has low solubility with Log S of -10 and inability to obtain 100 μM solution. Only 2 compounds has Log S values > -4 and are able to obtain 100 μM solution.

## Task 2 - Model Reproducibility
# Step 1 - Installation of Model

# I installed rdkit which is a requirement before installing the soltrannet model in my notebook
`!pip install rdkit`
`!pip install soltrannet`

# Step 2 - Selecting Result to Reproduce
I read the publication and saw a result I could reproduce using the SC2 dataset that was used in the study.

# Step 3 - Running Predictions with Soltrannet Model
From the publication, I was able to find the github repository which has the installation and usage instructions and data used. Using the SC2 dataset that I found in the github repository they provided in the publication, In section 1,I ensured the SMILES representation was valid using rdkit library. I made predictions with the soltrannet model, and saved the output. This output can be found in output folder created in the data folder in my repo.

# Step 4 - Reproducing Figures
To ascertain reproducibility, I compared the predictions generated the Soltranet model against the actual solubility values from Author's result and re-created an histogram plot and a bar plot of false discovery rates where insolubility is LogS <= -5 and <=-6 from the publication. The result was the same indicating reproducibility.
I also went ahead to use a more categorized datasets also found on the soltrannet repository to generate false discovery rate of Insoluble compounds as seen on the publication and the output was also the same.

# Step 5 - Reproducibility in Ersilia Model Hub
Using the same SC2 dataset, in Section 2 of Model Reproducibility, I generated predictions using Ersilia model , saved the result and compared the results with Author's. I recreated an histogram and 2 plots for false discovery rates where the Insoluble LogS <= -5 and <=-6 . The results generated using Ersilia Model and the author's model was exactly the same which signifies Reproducibility.

# References
[Publication](https://pubs.acs.org/doi/10.1021/acs.jcim.1c00331)

[Soltrannet](https://github.com/gnina/SolTranNet)

[Soltranet Datasets and Figures Generations Repository](https://github.com/francoep/SolTranNet_paper)

[Ersilia Google Colab Guide](https://github.com/ersilia-os/ersilia/blob/master/notebooks/ersilia-on-colab.ipynb)

# Citation
[Original authors](https://pubs.acs.org/doi/10.1021/acs.jcim.1c00331)

[Ersilia Model Hub](https://github.com/ersilia-os/ersilia/blob/master/CITATION.cff).

