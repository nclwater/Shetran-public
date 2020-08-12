# Example for hotstarting a SHETran run
To run go to program folder and double click on sv4.4.6.exe. then select the rundata file in examples/dunsop-hot1 or examples/dunsop-hot2.

There are two stages to using the hotstart.

## Stage 1: Writing the hotstart file.
See the example dunsop-hot1.

The file needs to be present in the rundata file:

    28: hostart file			-------INITIAL CONDITIONS                                    
    input_output_dunsop_hot.txt                                                                 

The writing of the hotstart information then needs setting in the `frd` file:

    :FR26 - HOTSTART PARAMETERS                                                     
          F      T     0.   168.

In this case the data is written every 168 hours to the `input_output_dunsop_hot.txt` file.

The start of every output time has `time=` and each variable is named before being output. The code is:


    IF (BHOTPR) THEN  
        IF (UZNOW.GE.HOTIME) THEN  
    ! uznow=current time (hours)
    ! uznext-= next time(hours)
    ! cstore = canopy storage (mm)
    ! gethrf = surface water elevation(m)
    ! QSAzz = overland flow?
    ! QOC = overland flow
    ! DQ0ST = flow derivatives
    ! DQIST = flow derivatives
    ! DQIST2 = flow derivatives
    ! SD = snow pack depth
    ! TS = snow temperature
    ! NSMC = COUNTER USED IN ROUTING MELTWATER THROUGH SNOWPACK
    ! SMELT = water in meltwater slug?
    ! TMELT = temperature of eltwater slug?
    ! vspsi = soil water potentials
         WRITE (HOT,*) "time= ",UZNOW, UZNEXT, top_cell_no,"cstore= ", (CSTORE (IEL), IEL = NGDBGN, &
         total_no_elements),"HRF= ", (getHRF (IEL), IEL = 1, total_no_elements),"QSA= ", ( (QSAzz (IEL, K), IEL = 1, &
         total_no_elements), K = 1, 4),"QOC= ", ( (QOC (IEL, K), IEL = 1, total_no_elements), K = 1, 4), &
         "DQ0ST= ",( (DQ0ST (IEL, K), IEL = 1, total_no_elements), K = 1, 4),"DQIST= ", ( (DQIST (IEL, &
         K), IEL = 1, total_no_elements), K = 1, 4),"DQIST2= ", ( (DQIST2 (IEL, K), IEL = 1, &
         NGDBGN - 1), K = 1, 3),"SD= ", (SD (IEL), IEL = NGDBGN, total_no_elements), &
         "TS= ", (TS (IEL), IEL = NGDBGN, total_no_elements),"NSMC= ", (NSMC (IEL), IEL = NGDBGN, &
         total_no_elements),"SMELT= ", ( (SMELT (K, IEL), K = 1, NSMC (IEL) ), IEL = NGDBGN, &
         total_no_elements),"TMELT= ", ( (TMelt (K, IEL), K = 1, NSMC (IEL) ), IEL = NGDBGN, &
         total_no_elements),"vspsi= ", ( (VSPSI (j, iel), j = 1, top_cell_no), IEL = 1, total_no_elements)
            HOTIME = HOTIME+BHOTST  
        ENDIF  
    ENDIF  


## Stage 2: Reading the hotstart file
See example dunsop-hot2.

The file needs to be present in the rundata file:

    28: hostart file			-------INITIAL CONDITIONS                                    
    input_output_dunsop_hot.txt                                                                 

but in this case it needs to be copied from dunsop-hot1.

The reading of the hotstart information then needs setting in the `frd` file:

    :FR26 - HOTSTART PARAMETERS                                                     
          T      F  500.0    0.0

In this case the data is read from the `input_output_dunsop_hot.txt` file at the next time after 500 hours, which is 504.77 hours.

The meteorological data will start from this time as well.

This means the results from the simulation in dunsop-hot2 (which only starts after 504 hours) should be the same as from 504 hours in dunsop-hot1 (which runs for 1460 hours). Tests show that although they are very similar they are not identical.


Note that the hotstart file (e.g `input_output_dunsop_hot.txt`) can be edited. So for example, the output from a particular time can be selected and the time changed. So you could select the data from final time in the file and make a new hotstart file containing just this data and change the time=1 hour. Then set the hotstart to start after 0.5 hours and this data will then be used for the entire simulation. 


 

