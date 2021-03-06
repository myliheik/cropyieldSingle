# Technical Report

This repository includes codes that are used to reshape histogram files from Sentinel-2 single image time series into analysis ready format and 
build neural network models to predict crop yield.

Here is a visual representation of the workflow:

![Workflow](img/WP2-workflow.png)

Prerequisites: Sentinel-2 image data is preprocessed with codes in github.com/lukefi/cropyield . For machine learning, the data should be divided into training and test set. 

## Reference data

As a reference data, we will have historical crop yields per hectare on farm-level from around 6,000 Finnish agricultural holdings participating the annual Finnish crop production survey. Note that this is condidential information and available only for statistical production purposes with disclosure agreement. The crop species included in this study are winter wheat, spring wheat, oat, malting barley, feed barley, and autumn rye.

## Python environment

Python version used is Python 3.8.6. The codes will probably also work on earlier versions as well. Tensorflow version used is 2.3.1.

The file requirements.txt may be used to create a virtual Python environment using:

conda create --name env_name --file requirements.txt

## Workflow

### 1. python/histo2stack.py

This code stacks all histogram files in a directory into one numpy array file.

RUN:

python histo2stack.py -i /Users/user/Documents/myCROPYIELD/scratch/project_2001253/histo_test1110_2016 -n 32 -o /Users/user/Documents/myCROPYIELD/dataStack -f test1110_2016.pkl 

WHERE:

-i is the input directory where are histograms in .csv files.

-n is the number of bins in histograms.

-o is the given output directory

-f is the given output filename

The programme will write results into output_dir_temp.

### 2. python/stack2ARD.py

This code stacks all numpy array files into one numpy array file. This programme finally converts data into machine learning ready format.

RUN:

python stack2ARD.py -o /Users/myliheik/Documents/myCROPYIELD/dataStack -f test1110 

WHERE:

-o is the output directory (same as previously for histo2stack.py)

-f is a characterizing name name of the data set

### 3. python/run3DNeuralNet.py

This code trains LSTMsingle and RNNsingle models and calculates predictions for a test set.

## Funding acknowledgements

This work was supported by the European Union (grant 831735 — 2018-FI-CROPYIELD).

![Funded by Eurostat](img/Eurostat_logo_RGB_200-small.png)
