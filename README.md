# SMMPPI
SMMPPI: tool to predict PPI modulators
-------------------------------------------------------------------------

To use the program, de-compress the program file with following command:   
tar -xvf SMMPPI_Program.tar.gz
cd SMMPPI_Program

-------------------------------------------------------------------------

##Pre-requisite Installations

The SMMPPI program requires following softwares to be installed 
 
1.WEKA 
2.Rdkit 
3.R program 


To install weka, run the follwing commands:
wget --no-check-certificate https://sourceforge.net/projects/weka/files/weka-3-8/3.8.1/weka-3-8-1.zip 
unzip weka-3-8-1.zip 


Rdkit and R can be installed using anaconda by pasting following commands
in the terminal (in the SMMPPI_Program directory)

conda create -c rdkit --prefix rdkit_env rdkit R 
conda activate ./rdkit_env 


If your system doesn't have conda installed, then first install
conda (https://docs.continuum.io/anaconda/install/linux/)
alternatively, rdkit and R can be installed from their source
codes ("https://github.com/rdkit/rdkit/archive/Release_XXXX_XX_X.tar.gz" & 
"https://cran.r-project.org/doc/manuals/r-release/R-admin.html") 

#############################################################################################################################################

##Running the program

After sucessfull installations,
before using the program, don't forget to activate the rdkit_env
(if rdkit installed with conda).

Run the following commands 
conda activate ./rdkit_env
cd ./scripts


To use the General SMMPPI Predictor, run the follwing command

./search_Gen_PPIM sample.smi prefix

  where,
    sample.smi  - query compound smiles file
    out_dir   - prefix for output directory name

** A test query smiles file is provided (sample.smi : containing Compound ID and smiles seperated with tab)


For the General SMMPPI Predictor,
3 additional classifiers are also provided based on benchmarking done with 3 different methods of splitting the train-test data (see manuscript):

	1. search_Gen_PPIM_modulators_Random_Split :    Based on randomly dividing the train-test sets
	2. search_Gen_PPIM_modulators_AVE_Split:        Based on AVE-calculation method of dividing the train-test sets
	3. search_Gen_PPIM_modulators_Realistic_Split : Based on clustering based method of dividing the train-test sets

For prediction of General PPIMs, any of these 3 classifiers can also be chosen (e.g. - Random-split method) and run the following command
./search_Gen_PPIM_modulators_Random_Split comp.smi prefix


To use the PPI family specific SMMPPI Predictors, run the following command 
./search_XXX comp.smi prefix
 
  where,
   search_XXX - predictor script for given PPI family 
                (e.g.- 'search_Bromodomain_Histone_modulators' script for searching Bromodomain-Histone modulators)
   comp.smi   - query compound smiles file 
   out_dir    - prefix for output directory name 

##############################################################################################################################################

##Results

The output directory contains 
  1.score.txt : contains Compound IDs, Smiles, Predictor Score, Status
                   (Positive : Potential PPIM of concerned family;
                   Negative : Not a potential PPIM of concerend family)
  2.selected_img : contains images of compounds predicted positive by Predictor







