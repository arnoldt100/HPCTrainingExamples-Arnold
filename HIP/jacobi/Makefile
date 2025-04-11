##**************************************************************************
##* Copyright (c) 2022, Advanced Micro Devices, Inc. All rights reserved.
##**************************************************************************

# Here we include the appropiate Makefile for building on your particular machine.
include Makefile.Frontier

# ----------------------------------------------------------------------
# No other edits should be needed below this comment
# ----------------------------------------------------------------------

# Here we set the name of the binary.
BINARY=Jacobi_hip

# Here we set the dependent header files,
DEPS=Jacobi.hpp \
     defines.hpp \
     markers.h

# Here we define the object files.
OBJS=JacobiSetup.o \
     JacobiRun.o \
     JacobiMain.o \
     HaloExchange.o \
     Input.o \
     JacobiIteration.o \
     Laplacian.o \
     Norm.o

HaloExchange.o: $(DEPS) HaloExchange.hip
	$(HIPCC) $(HIP_CFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c HaloExchange.hip -o HaloExchange.o
 
Input.o: $(DEPS) Input.hip
	$(HIPCC) $(HIP_CFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c Input.hip -o Input.o

JacobiMain.o: $(DEPS) JacobiMain.hip
	$(HIPCC) $(HIP_CFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c JacobiMain.hip -o JacobiMain.o
 
JacobiRun.o: $(DEPS) JacobiRun.hip
	$(HIPCC) $(HIP_CFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c JacobiRun.hip -o JacobiRun.o

JacobiSetup.o: $(DEPS) JacobiSetup.hip
	$(HIPCC) $(HIP_CFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c JacobiSetup.hip -o JacobiSetup.o

JacobiIteration.o: $(DEPS) JacobiIteration.hip
	$(HIPCC) $(HIP_CFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c JacobiIteration.hip -o JacobiIteration.o

Laplacian.o: $(DEPS) Laplacian.hip
	$(HIPCC) $(HIP_CFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c Laplacian.hip -o Laplacian.o

Norm.o: $(DEPS) Norm.hip
	$(HIPCC) $(HIP_CFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c Norm.hip -o Norm.o

$(BINARY): $(OBJS)
	$(HIPCC) -o $(BINARY) $(OBJS) $(HIP_CFLAGS) $(CFLAGS) $(MPI_LDFLAGS) ${HIP_LDFLAGS} $(LDFLAGS) 

uninstall: 
	rm -rf ${INSTALL_DIR}/*

install:
	mkdir -p ${INSTALL_DIR}
	cp -f ${BINARY} ${INSTALL_DIR}

clean:
	rm -rf *.o ${BINARY}

realclean: clean uninstall 

all: my_rocm_path ${BINARY} install

