include ../../common/make.config

# C compiler
CC = g++
CC_FLAGS = -g -O2 

all: bp_cpu bp_gpu

bp_cpu: backprop.o imagenet.o facetrain.o
	$(CC) $(CC_FLAGS) backprop_ocl.cpp backprop.o imagenet.o facetrain.o -o $@ -I$(OPENCL_INC) -L$(OPENCL_LIB) -lOpenCL

bp_gpu: backprop.o imagenet.o facetrain.o
	$(CC) $(CC_FLAGS) backprop_ocl.cpp backprop.o imagenet.o facetrain.o -o $@ -I$(OPENCL_INC) -L$(OPENCL_LIB) -lOpenCL -DUSE_GPU

backprop: backprop.o imagenet.o facetrain.o
	$(CC) $(CC_FLAGS) backprop_ocl.cpp backprop.o imagenet.o facetrain.o -o backprop -I$(OPENCL_INC) -L$(OPENCL_LIB) -lOpenCL

%.o: %.[ch]
	$(CC) $(CC_FLAGS) $< -c

backprop.o: backprop.c 
	$(CC) $(CC_FLAGS) backprop.c -c

facetrain.o: facetrain.c
	$(CC) $(CC_FLAGS) facetrain.c -c

imagenet.o: imagenet.c
	$(CC) $(CC_FLAGS) imagenet.c -c

clean:
	rm -f *.o *~ backprop *.linkinfo bp_gpu bp_cpu
