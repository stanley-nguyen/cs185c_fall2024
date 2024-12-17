# Hemispheres Effect on Temperature and Currents

For this project, I am investigating the effects of the Northern and Southern hemispheres on ocean currents and sea surface temperature. The question that will be asked is:

*How would ocean currents and sea surface temperature levels be affected if the Northern and Southern hemispheres were flipped?*

## Project Description
My region of interest is the North Atlantic Gyre. I will construct a model spanning this area and run my simulation two times, one with the flipped hemispheres and one with the normal hemispheres. I anticipate the concentration of warm water will be greater on the east side of the North Atlantic Ocean and the direction of the North Atlantic Gyre will reverse.

For initial conditions, I will use the ECCO Version 5 Model from 2016. I will construct boundary and external forcing conditions from the output of this model. The results will be analyzed from a time series of temperature and velocity in the North Atlantic Ocean created from the two models. Two movies will be created for visualization. The first movie will have the initial conditions and the second movie will have the flipped hemispheres.

## Reproducing Model Results
The following steps outline how to construct the model files, configure and run the model, and assess the model results.

### Step 1: Create the Model Files
Several input files need to be created to run the model. Generate the following list of files using the notebooks indicated in parentheses:
- Model Grid (notebooks/Creating the Model Grid.ipynb)
- Bathymetry (notebooks/Creating the Bathymetry.ipynb)
- Initial Conditions (notebooks/Creating the Initial Conditions.ipynb)
- External Forcing Conditions (notebooks/Creating the External Conditions.ipynb)
- Boundary Conditions (notebooks/Creating the Boundary Conditions.ipynb)
The model files should be placed into the  `input` directory.

### Step 2: Create the Model Files for the Southern Hemisphere variant
Additional input files need to be created to run the southern hemisphere variant of the model. Generate the following list of files using the notebooks indicated in parentheses:
- Bathymetry SH (notebooks/southern_hemisphere/Creating the Bathymetry (SH).ipynb)
- Initial Conditions SH (notebooks/southern_hemisphere/Creating the Initial Conditions (SH).ipynb)
- External Forcing Conditions SH (notebooks/southern_hemisphere/Creating the External Conditions (SH).ipynb)
- Boundary Conditions SH (notebooks/southern_hemisphere/Creating the Boundary Conditions (SH).ipynb)
The model files should be placed into the  `input_southern` directory.

### Step 3: Add files to the computing cluster
Once the input files have been created, the model files can be transferred to the computing cluster. Begin by cloning a copy of [MITgcm](https://github.com/MITgcm/MITgcm) into your scratch directory and make a folder for the configuration, .e.g.
```
mkdir MITgcm/configurations/atl_hemispheres
```
Then, use the `scp` command to send the `code`, `input`, `input_southern`, and `namelist` directories to your configuration directory. 

### Step 4: Compile the model
Once all of the files are on the computing cluster, the model can be compiled. Make a `build` directory in the configuration directory and run the following lines:
```
../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make
```

### Step 5.1: Run the model normally
After the compilation is complete, run the model normally. Move to the run directory, link everything from `input` and `code`, and the submit the job script:
```
sbatch cs185c.slm
```

### Step 5.2: Run the model in the southern hemisphere
Next, run the model in the southern hemisphere to complete the experiment. Link everything from `input_southern` and `code` to a directory called `run_southern`. Then, edit the `data` file to point to `ATL_southern_bathymetry.bin`. Then, submit the job script again to rerun the model.

### Step 6: Analyze the Results
There are two notebooks provided for analysis:
1. Analyzing Model Results

   `notebooks/Assessing Model Results.ipynb`
   
   This notebook serves to assess the spatial and temporal variations in the temperature field for the model ran in the Northern Hemisphere. It generates the visualization `Atlantic Sea Surface Temperature.mp4` provided in the figures directory.
   
   `notebooks/southern_hemisphere/Assessing Model Results (SH).ipynb`
   
   This notebook serves to assess the spatial and temporal variations in the temperature field for the model ran in the Southern Hemisphere. It generates the visualization `Atlantic Sea Surface Temperature (SH).mp4` provided in the figures directory.

3. Answering the Science Question
   
   `notebooks/Answering the Science Question.ipynb`
   
   This notebook analyzes the difference between the two models to address the science question posed above.
