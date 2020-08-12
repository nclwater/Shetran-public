This catchment has 1024,1030 and 1060 errors. Previously it crashed after about 828 hours. 

There is now a reduction in timestep length if one of the above errors occurs and it runs OK

Changes to code:

sglobal.f90 
***********
L 147
LOGICAL :: ISERROR

LOGICAL :: ISERROR2


L326
!**SB 07072020 reduce timestep if there are errors 1024,1030,1060
ISERROR = .FALSE.

ISERROR2 = .FALSE.

L401
!**SB 07072020 reduce timestep if there are errors 1024,1030,1060
IF ((ERRNUM.EQ.1024).OR.(ERRNUM.EQ.1030)) THEN
    ISERROR=.TRUE.
ENDIF
IF (ERRNUM.EQ.1060) THEN
    ISERROR2=.TRUE.
ENDIF


rest.f90
********
L797
!**SB 07072020 reduce timestep if there are errors 1024,1030,1060
IF (ISERROR2) THEN
    UZNEXT = max(0.0003,uznext/10.0)
ELSEIF (ISERROR) THEN
    UZNEXT = max(0.0003,uznext/100.0)
ENDIF
ISERROR2 = .FALSE.
ISERROR = .FALSE.

OCmod2.f90
**********
L1125
IF(.not.aok) CALL ERROR(WWWARN, 1060, PPPRI, 0, 0, 'OC flow criteria could not be met')