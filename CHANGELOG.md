# Changelog

**SHETRAN Updates May 2026**

**Code Improvements**

- improved channel junction convergence
- add percentage completion and other improved output to command prompt during simulation
- improved error messages and their output to the command prompt and pri file
- add -error option to command prompt options
- compiled with -O2 and and -fp:precise which leads to noticeable improvements in runtime (20%-80%, depending on model) 

**SHETRAN Updates April 2026**

**Code Improvements**

- Update code in SHETRAN-Prepare and SHETRAN so they are compatible with the latest version of the Intel ifx and GFortran compilers. Previously it only worked with the now deprecated Intel ifort compiler.
- Convert code to modern Fortran standards including removing most of the obsolescent code (e.g fixed format source code in SHETRAN-Prepare and GOTO statements in both lots of code removed).
- Make all arrays allocatable in SHETRAN-Prepare and all 2-dimensional and 3- dimensional arrays allocatable in SHETRAN. The consequence of this is there is no size limit in SHETRAN-Prepare and within SHETRAN catchments up to 1000 x 1000 grid squares can now be used (previously the limit was 400 x 400 grid squares).

**User Interface**

- Make the input into SHETRAN-Prepare a properly read XML file (previously it was called an XML file but it was read sequentially). The consequence of this is that only a single SHETRAN-Prepare executable is needed (previously there were 3 different executables). Also most tags are optional with default values used if they are not present.
- The following optional tags have been added to the XML file:

	- Adding bank cells into SHETRAN
	- Adding solute transport into SHETRAN
	- Including hours and minutes (previously only year, month and day could be added)
	- Specific storage in "Soil Properties"
	- Spatial variable initial conditions
	- Allowing metrological data to include dates (see below)
	- Channel width parameters
	- Model timestep parameters
	- Timestep for HDF output
	- The option to include a base flow boundary
	- The option to produce additional river flow text output (for internal gauges within the catchment)
	- The option to produce water table text output (to compare with measured water table depths)

- Meteorological data can now be input with (8601 format) or without dates in the first column (previously dates could not be included). If the simulation start time is different from the meteorological data start time the correct meteorological data is read. Text output from the simulation now includes dates.
- Additional output is included. This includes the following files: input*CATCHNAME_element_number.asc, input_CATCHNAME_river_location.txt, input_CATCHNAME_river_network.asc, output* CATCHNAME \_sediment*all.csv (if sediment component run), output* CATCHNAME \_sediment*fine.csv (if sediment component run), output* CATCHNAME \_contaminant.csv (if contaminant/solute component run).


