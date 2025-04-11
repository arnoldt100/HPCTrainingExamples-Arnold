##**************************************************************************
##* Copyright (c) 2022, Advanced Micro Devices, Inc. All rights reserved.
##**************************************************************************

include Makefile.Frontier

# # Flags
CFLAGS=-O3 -g -ggdb -fPIC -std=c++11 -march=native -Wall
CFLAGS+=-I$(ROCM_PATH)/roctracer/include -I${ROCM_PATH}/include/roctracer
LDFLAGS=-L$(ROCM_PATH)/lib/ -lroctx64 -lroctracer64
HIPFLAGS=-lamdhip64

# Here set the name of the binary and the directory
# to install the binary.
BINARY="Jacobi_hip"

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
	$(HIPCC) $(HIPCFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c HaloExchange.hip -o HaloExchange.o
 
Input.o: $(DEPS)  Input.hip
	$(HIPCC) $(HIPCFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c Input.hip -o Input.o

JacobiMain.o: $(DEPS)  JacobiMain.hip
	$(HIPCC) $(HIPCFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c JacobiMain.hip -o JacobiMain.o
 
JacobiRun.o: $(DEPS)  JacobiRun.hip
	$(HIPCC) $(HIPCFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c JacobiRun.hip -o JacobiRun.o

JacobiSetup.o: $(DEPS)  JacobiSetup.hip
	$(HIPCC) $(HIPCFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c JacobiSetup.hip -o JacobiSetup.o

JacobiIteration.o: $(DEPS)  JacobiIteration.hip
	$(HIPCC) $(HIPCFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c JacobiIteration.hip -o JacobiIteration.o

Laplacian.o: $(DEPS)  Laplacian.hip
	$(HIPCC) $(HIPCFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c Laplacian.hip -o Laplacian.o

Norm.o: $(DEPS)  Norm.hip
	$(HIPCC) $(HIPCFLAGS) ${MPI_CFLAGS} $(CFLAGS) -c Norm.hip -o Norm.o

$(BINARY): $(OBJS)
	$(MPILD) $(CFLAGS) -o $(BINARY) $(OBJS) $(LDFLAGS)

uninstall : 
	rm -rf ${INSTALL_DIR}/*

clean:
	rm -rf *.o ${BINARY} ${INSTALL_DIR}/*

realclean: clean uninstall 

all: my_rocm_path ${BINARY}

