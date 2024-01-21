#SUNTANSHOME=../../main
SUNTANSHOME=/home/sherry/code/suntans/main
#SUNTANSHOME=/home/mrayson/group/mrayson/testing/suntans/main
include $(SUNTANSHOME)/Makefile.in

ifneq ($(MPIHOME),)
  CC = $(MPIHOME)/bin/mpicc
  MPIDEF = 
  MPIINC = -I$(MPIHOME)
else
  CC = gcc
  MPIDEF = -DNOMPI 
  MPIINC = 
endif

OPTFLAGS = - O2 -fcommon 

ifneq ($(PARMETISHOME),)
  PARMETISINC = -I$(PARMETISHOME)/ParMETISLib
endif

LD = $(CC) -O2 -fcommon
CFLAGS = 
MATHLIB = -lm

EXEC = tidal_front
OBJS = 
SUN = $(SUNTANSHOME)/sun
INCLUDES = -I$(SUNTANSHOME) $(MPIINC) $(PARMETISINC)
DEFS = $(MPIDEF)
NUMPROCS = 2
datadir = data

all:	data

test:	data
	sh $(EXEC).sh $(NUMPROCS) 

restart:    data
	sh $(EXEC)-restart.sh $(NUMPROCS) 1

data:	state.o grid.o boundaries.o met.o
	cp state.o grid.o boundaries.o met.o $(SUNTANSHOME)
	make -C $(SUNTANSHOME)

.c.o:	
	$(LD) -c $(INCLUDES) $(DEFS) $*.c

$(SUN):	state.o grid.o boundaries.o met.o
	cp state.o grid.o noundaries.o met.o $(SUNTANSHOME)
	make -C $(SUNTANSHOME)

debug:	data
	$(MPIHOME)/bin/mpirun -np $(NUMPROCS) xterm -e gdb -command=gdbcommands.txt $(SUN)

valgrind: data
	mkdir $(datadir)
	cp rundata/* $(datadir)
	$(MPIHOME)/bin/mpirun -np $(NUMPROCS) ./$(SUN) -g -vv --datadir=$(datadir)
	$(MPIHOME)/bin/mpirun -np $(NUMPROCS) valgrind --tool=memcheck --leak-check=yes ./$(SUN) -s -vvv --datadir=$(datadir)

clean:
	rm -f $(SUNTANSHOME)/*.o
	rm -f *.o

clobber: clean
	rm -rf *~ \#*\# PI* $(EXEC) gmon.out data rundata/*~

