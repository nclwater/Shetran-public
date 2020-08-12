# Daryl ZQ Module (Stage-discharge relationship at Weir)

Contains the source code changes need to add this module

## ZQmod.f90

New Module

## OCmod2.f90

L5
!!ZQ Module 200520 
USE ZQmod,     ONLY : ZQtable
USE AL_D,      ONLY : ZQweirsill,ZQTableRef

L641


!!ZQ Module 200520 
DOUBLEPRECISION              :: dzu
DOUBLEPRECISION              :: weirsill

L672

!!ZQ Module 200520 
ELSEIF (NTYPE.EQ.12) THEN
    !print*,ZQTableRef,zi(hi)
    CALL ZQTable(ZQTableRef,ZI(HI),Q(LO))
    weirsill=ZQWeirSill(ZQTableRef)
    DZU = DIMJE(ZI(HI), weirsill)
    DQ(LO,HI)=50.0*1.5*sqrt(dzu)                            ! This works for Crummock. Stability during step changes should be tested e.g. for a small area reservoir
    DQ(LO,LO)=0
    write(779,*) zi(hi),Q(lo),dq(lo,hi)
!!ZQ Module 200520 end

## OCQDQMOD.F90

L3
ZQ Module 200520
! new variables     NoZQTables,ZQTableRef,ZQTableLink,ZQTableFace

USE AL_D ,     ONLY : DQ0ST, DQIST, DQIST2, NOCBCC, NOCBCD, NoZQTables,ZQTableRef, ZQTableLink,ZQTableFace

L94
INTEGER                         :: i

L182
!***ZQ Module 200520
                    do i=1,NoZQTables
                    if (((ielu.eq.ZQTableLink(i)).and.(iface.eq.ZQTableFace(i))).or.((jel.eq.ZQTableLink(i)).and.(jface.eq.ZQTableFace(i)))) then
                       ZQTableRef=i
                       ntype=12
                    endif
                    enddo
 !!***ZQ Module 200520 end

## AL_D.90
 L59
 !ZQ Module 200520
! new variables     zqd,NoZQTables,ZQTableRef,iszq,ZQTableLink,ZQTableFace,ZQweirSill
!----------------------------------------------------------------------*

L109
zqd = 51

L114
NXP1,NYP1,NXM1,NYM1,NXEP1,NYEP1,NoZQTables,ZQTableRef

L138
BEXTS1,BHOTPR,BHOTRD,BEXSY,BEXCM, ISTA,isextradis,iszq


L148
INTEGER, DIMENSION(:), ALLOCATABLE               :: ZQTableLink,ZQTableFace ! These store the metadata for a single ZQtable in the ZQ file

L163
DOUBLEPRECISION,    DIMENSION(:), ALLOCATABLE              :: ZQweirSill 


## frmod.f90
L5
!ZQ Module 200520 new variables iszq,zqd

L23
EPD, FRD, HOTIME, HOT, TAH, TAL, ISTA,isextradis,iszq, &


L28
SF, SMD, SD, TIMEUZ, TS, TIM, TMAX, TTH, UZVAL, VHT, VED, VSE,TOUTPUT,zqd                  

L54
USE ZQmod,    ONLY : ReadZQTable

L1283
!***ZQ Module 200520
if (iszq) call ReadZQTable

L1695-1739
!***ZQ Module 200520 change log file to unit 52 and read DO 100 I = 10, 51 (was 50)
iszq=.true but false is no text present

