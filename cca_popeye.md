# Installation steps to install EXP in the flatiron popeye machine 

### Retrieve the `main' branch from the GitHub repo:

```
git clone https://github.com/EXP-code/EXP.git
git submodule update --init --recursive
```

### Make and move to a build location:

```
mkdir build
cd build
```

### Check out a node for building
```
srun -p cca --nodes=1 --ntasks=16 --pty $SHELL
```

###  Load the modules from modules/2.3-20240529: 
```
module purge
module load cmake/3.27.9
module load gcc/11.4.0
module load openblas/threaded-0.3.26
module load eigen/3.4.0
module load openmpi/4.0.7
module load hdf5/mpi-1.12.3
module load cuda/12.3.2
module load python/3.10.13
module load fftw/3.3.10
```

### Configure: 
```
cmake -DCUDA_USE_STATIC_CUDA_RUNTIME=on -DENABLE_CUDA=0 -DEigen3_DIR=$EIGEN_BASE/share/eigen3/cmake/ -DCMAKE_INSTALL_PREFIX=$HOME -DCMAKE_BUILD_TYPE=Release -DCMAKE_CUDA_FLAGS="-arch=compute_60 -code=sm_60,sm_70,sm_80 -std=c++17" -Wno-dev ..
```
### Build & install
```
make -j 24
make install 
```


