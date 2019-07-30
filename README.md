# README #

### Tissue Fluidity Vertex Model ###

##### as detailed in : #####
#### Tissue fluidity promotes epithelial wound healing, Nature Physics (2019) ####

### Authors / Contributors ###

* Michael F Staddon (University College London)
* Shiladitya Banerjee (University College London)

#### created at the University College London ####

### System Requirements ###

This system requires Surface Evolver 2.70 which can be downloaded at: http://facstaff.susqu.edu/brakke/evolver/evolver.html

### QUICKSTART GUIDE ###

Create a new directory for the simulation, containing the "wound_healing.fe", "wound_creation.secmd", parameters.inp", and "dynamics.secmd" files. 

The "wound_healing.fe" file is the main Surface Evolver file, containing the tissue geometry, energy definitions, and code to run the simulation.

The "parameters.inp" file contains the system parameters. These are input non-dimensional except for time, which is in seconds.

The "dynamics.secmd" file contains general simulation commands which numerically solve the dynamics of the system, and record simulation statistics.

The "wound_healing.secmd" file contains simulation commands for creating the wound.

Create folders "/output/", for simulation statistics, and "/output/images/", for simulation images, in the directory.

Run the simulation. On Windows double clicking the "wound_healing.fe" file should run it. On mac use the command line e.g.,
```
> evolver wound_healing.fe
```

During running, the simulation records statistics, such as the occurence of intercalations before and after wounding, the wound area, and cell shapes. Once the simulation has completed, the following output files will have been created, where %s is the "output_name" variable:

* "output/%s_tissue_energy.csv" is a table with the following columns: simulation step, cell id, initial wound distance, current wound distance, cell energy.

* "output/%s_unwounded_t1s.csv" and "output/%s_wounded_t1s.csv" are tables recording occurences of T1s before and after wounding. "T1 Count" indicates the number of T1s that an edge has undergone, while "Last T1" shows the time since the last T1.

* "output/%s_wound_cells.txt" contains information on cell shapes. It records the vertices of the cells that were in the first 3 rows around the wound at the time of ablation. The first four columns show: time step, cell id, initial wound distance, current wound distance. The next columns show vertex positions, alternating between x and y coordinates e.g x0, y0, x1, y1... where x0 is the x position of the vertex[0].

* "output/%_wounded_stats.csv" contains wound area and number of junctions over time.

* "output/images/%s_%06d.ps" //post script images of the simulation, recorded every "image_interval" time steps, where %06d is the current timestep.

Simulations should take between 10 - 30 minutes on an average computer.

## Simulation Parameters ##

Simulation parameters may be changed in the "parameters.inp" file. Alternatively, values can be overwritten in the simulation file by writing them under the line "read "parameters.inp";" e.g.,
```
read "parameters.inp";
edge_tension := -0.06;
```
allowing several simulation files with different parameters in the same folder.

|Variable name              |Type   |Default value  |Units  |Description                        |
|-------------              |:----: |:-------------:|:-----:|-----------------------------------|
|**Tissue properties**|||||
|kappa|float|1|-|Cell elastic modulus|
|A0|float|1|-|Preferred cell area|
|gamma|float|0.04|-|Cell contractility|
|pzero|float|0|-|Cell preferred shape index (unused in paper)|
|edge_tension|float|0.00|-|Mean cell line tension|
|sigma_m|float|0.025|-|Cell line tension standard deviation|
|tau_m|float|150|s|Line tension recovery time|
|**Dynamic properties**|||||
|dt|float|3|s|Time step|
|viscosity|float|30|s|System viscosity|
|Lmin|float|0.05|-|Length under which T1s can occur|
|**Division properties**|||||
|mean_division_rate|float|2.25|1/hr|Mean % cells dividing per hour|
|min_division_age|float|10000|s|Time for cell division to complete|
|**Wound properties**|||||
|wound_tension|float|0.08|-|Mean purse-string tension|
|wound_area_decay|float|60|s|Time scale for wound area term to decay|
|wound_radius|float|1.33|-|Wound radius|
|**Other properties**|||||
|random_seed|int|1|-|Random seed|
|output_interval|int|1|-|Timesteps between wound area recording|
|cell_output_interval|int|10|-|Timesteps between cell shape recording|
|img_output_interval|int|20|-|Timesteps between image recording|

### Reproduction instructions ###

By varying parameters and random seeds, the main results of the simulations can be reproduced using this code and analysing the output files.

### Contribution guidelines ###

* Email: shiladitya.banerjee@ucl.ac.uk

### Who do I talk to? ###

* Michael Staddon (michael.staddon.16@ucl.ac.uk)
* Shiladitya Banerjee (shiladitya.banerjee@ucl.ac.uk)
