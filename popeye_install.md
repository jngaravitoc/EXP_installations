Retrieve main branch from github repo:

git clone https://github.com/EXP-code/EXP.git
git submodule update --init --recursive

Make and move to a build location:

mkdir build
cd build

Check out a node for building
srun -p cca --nodes=1 --ntasks=16 --pty $SHELL


Load up the modules
module purge
module load cmake
module load gcc/10.2.0
module load openblas/0.3.15-threaded
module load eigen/3.4.0
module load openmpi/4.0.6
module load hdf5/1.10.7
module load cuda
module load python3

Configure: 

cmake -DCUDA_USE_STATIC_CUDA_RUNTIME=off -DENABLE_CUDA=1 -DEigen3_DIR=$EIGEN_BASE/share/eigen3/cmake/ -DCMAKE_INSTALL_PREFIX=$HOME -DCMAKE_BUILD_TYPE=Release -DCMAKE_CUDA_FLAGS="-arch=compute_60 -code=sm_60,sm_70,sm_80 -std=c++17" -Wno-dev ..

Build & install
make -j24
make install 



