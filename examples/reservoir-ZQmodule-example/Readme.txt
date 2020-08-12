Shetran-Reservoir Module Example
********************************

This is a standard Shetran simulation except between two river channels (links) the downstream flow is defined by an upstream head and an external lockup table. 

This can be carried out for several such examples within a catchment.

To run the module create the custom ZQ file (e.g. input_cockeratscalehill-500m_customZQs.txt) and modify the rundata file so this is called in unit 51:

51: Weir data
input_cockeratscalehill-500m_customZQs.txt

Full details will be located in the Shetran website documentation:

https://research.ncl.ac.uk/shetran/Documentation.htm

