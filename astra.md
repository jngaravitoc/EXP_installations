# Installation steps to install EXP in the astra UMD machine 

### Retrieve the `main' branch from the GitHub repo:

```
git clone https://github.com/EXP-code/EXP.git
git submodule update --init --recursive
```

### Make and move to a build location:

```
mkdir build
cd build
mkdir devel 
cd devel
```

### Check out a node for building:
```
ssh astra02
```

###  Load the modules: 
```
module purge
module load openmpi/4.0.7

```

### Configure: 
```
cmake -DCUDA_USE_STATIC_CUDA_RUNTIME=on -DENABLE_CUDA=0 -DEigen3_DIR=$EIGEN_BASE/share/eigen3/cmake/ -DCMAKE_INSTALL_PREFIX=$HOME -DCMAKE_BUILD_TYPE=Devel -Wno-dev ../..
```
### Build & install:
```
make -j 16
make install 
```

### It is always a good idea to test the installation:

```
make test
```

The 18 tests ran in 79.18s.  
To set up pyEXP include in your bashrc file the following lines:

```
export PYTHONPATH=/mnt/home/nico/lib/python3.11/sute-packages
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH":/mnt/home/nico/lib
export PATH="$PATH":/mnt/home/nico/local:/mnt/home/nico/bin
```
