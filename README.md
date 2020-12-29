This package contains the Python source code for journal classification.

# Directories

The directory contents included within this distribution are:

‘./group51_ass2_impl’	
: This folder contains all other folders in the distribution and also contains two raw data files and a notebook file for generating the model

‘./group51_ass2_impl/data’		
: A directory where intermediate data will be deposited by the model including the cleaned test and train data.

‘./group51_ass2_impl/language models’		
: A directory where the autoencoder generated within the model for feature engineering will be saved

‘./group51_ass2_impl/model output’	
: A directory where the final model predictions will be stored

‘./group51_ass2_impl/models’	
: A directory where the saved pkl file for the final LSTM model will be saved

# Libraries

- google.colab (1.0.0)
- fastai (2.0.18)
- numpy (1.18.5)
- random (included in python distribution)
- os (included in python distribution)
- pandas (1.1.4)
- nltk (3.2.5)
- re (included in python distribution)
- string (included in python distribution)
- tqdm (included in python distribution)
- torch (1.6.0+cu101)
- torchvision (0.7.0+cu101)

# Building Instructions

The distribution above was built and configured to be run in the Google Collaboratory environment. Google Colab is a cloud based implementation of a Jupyter Notebook environment which boasts free access to GPU accelerated environments. It’s this GPU availability which makes Google Colab the best choice for running this model.

For implementing this distribution, unzip and drag the high level folder (“group51_ass2_impl”) containing the distribution to your Google Drive. It is recommended that this folder be copied at the top level of your Google Drive file system as this is where the script is, by default configured to run from. Note you can adjust this setting, please see the information below on changing the distribution location on your Google Drive.

Unfortunately, due to the nature of the Google Colab environment, relative file paths cannot be implemented as they normally would on a local execution of the model. Therefore, if you place the distribution at any location other than the high level Google Drive, you will need to update the file paths to ensure the code executes.

This can be done by manipulating the following two variables:
1.	drive_selection = 'My Drive/'. This variable points to your personal drive by default, you can enter a value such as ‘Shared drives/'Assignment 2/’ to instead point to a shared drive.
2.	drive_location = 'group51_ass2_impl'. This directs the script to the location of the main distribution folder on your drive, by default it is assumed this will be at the top level of your Google Drive.

# Running Instruction

Perform the following steps to run the data cleaning, feature generation, model training and prediction portions of the distribution:
1.	Navigate to the ‘Group51_Model_Script.ipynb’ on your Google Drive, right click the file and select ‘Open With’ > ‘Google Colaboratory’
2.	In Google Colab, navigate to the “run time” drop down menu and select ‘Change Runtime Type’ and ensure that the ‘Hardware accelerator’ option is set to ‘GPU’ to maximise performance
3.	Navigate to the ‘runtime’ menu, select ‘Factory reset runtime’
4.	Navigate to the ‘runtime’ menu, select ‘Run all’

# Input data format

Input data must be placed in ‘./group51_ass2_impl’ which takes two input files.

First is test_data.csv where one row corresponds to one observation and contains two columns:
1.	Column ‘test_id’, an int type column which contains positive numbers which uniquely identify each row.
2.	Column ‘abstract’, a string type column which contains one abstract from a journal article per row.

Second is the train_data_labels.csv file where one row corresponds to one observation and contains three columns:
1.	Column ‘train_id’, an int type column which contains position numbers that uniquely identify each row.
2.	Column ‘abstract’, a string type column which contains one abstract from a journal article per row.
3.	Column ‘label’, a string type column which contains one of 100 class labels corresponding to the abstract in the same row.

The notebook file will read in both of these files by default based on the location in the drive and the file names.

# Output file

The output file can be found in ‘./model output’ which contains one output file entitled ‘pred_labels.csv’. The output file contains a series of label predictions corresponding to the abstracts given in the input file ‘test_data.csv’. This output file contains two columns as follows:
1.	‘test_id’ , an int type column containing the position numbers that uniquely identify each row. Note that these column values serve as a primary key between the prediction output and the test_id column in the test_data.csv such that an abstract in the test file has a class prediction in the output file where the test_id column in both files match.
2.	‘label’, a string type column which contains one of 100 class labels corresponding to predictions for input abstracts in the test_data.csv file with matching test_id values.  

# Final remarks

As a final note on reproducibility, the Google Colaboratory environment used to generate this model made use of a Cuda enabled GPU which significantly boosted performance. Colab has multiple Nvidia GPUs available for use, however, as Colab is a free service that does not guarantee resource availability, there is no way to select a specific GPU. When using a GPU enhanced environment one will be allocated based on resource availability which may impact reproducibility, note that tests conducted to date have not found any issues with reproducibility stemming from this environment limitation. 
