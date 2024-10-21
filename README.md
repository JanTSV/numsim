<div align="center">
<h3>
[Requirements](#requirements) | [How to](#how-to) | [Basics](#basics)
</h3>
</div>

# Requirements

- Unix based OS (preferrably Linux) NOTE: docker??
- `g++` compiler
- cmake (>= 3.8) and make
- VTK library (>= 7.1.1, see `.gitmodules`)
- paraview

# How to

## Get the source code

```bash
# Clone the repository
# ... via HTTPS
git clone https://github.com/JanTSV/numsim.git

# ... via SSH
git clone git@github.com:JanTSV/numsim.git

# Load the submodules (VTK)
git submodule update --init
```

## Build the project

```bash
# Optional: build VTK
# Assuming your are already in the directory of this repo
mkdir VTK/build & cd VTK/build
cmake ..
make
sudo make install
cd ../..  # go back to the repo home

# Build this project
cd build/
cmake ..
make  # this builds the src/numsim executable

# ... for the rease:
cmake -DCMAKE_BUILD_TYPE=Release .
```

# Basics

Link to the [documentation](https://numsim-exercises.readthedocs.io/en/latest/).

## How to get onto the cluster

Use ssh -X to enable X-forwarding, i.e. to be able to have graphic windows displayed on your computer. In summary:
```bash
ssh -X username@ipvslogin.informatik.uni-stuttgart.de
# enter password

ssh -X simcl1
# enter password

squeue
srun --pty bash
# now you are on a node of the cluster. the nodes have hostnames simcl1n1 - simcl1n4
```

When you are on any simcl1 or simcl1n* node, you should load the following modules, which make the respective software modules available:
```bash
module use /usr/local.nfs/sgs/modulefiles
module load gcc/10.2
module load openmpi/3.1.6-gcc-10.2
module load vtk/9.0.1
module load cmake/3.18.2
```

## Terminal (tmux)

To start a new tmux session, run
```bash
tmux
```

A new session with green border opens and you can type commands as usual. To detach from the session, type Ctrl+B → let go keys → D. To attach the next time, type
```bash
tmux at
```

### Copying files to and from the servers

```bash
# copy file to server
scp file.txt maierbn@ipvslogin:src

# copy the same file back
scp maierbn@ipvslogin:src/file.txt .

# copy a whole directory to server
scp -r numsim maierbn@ipvslogin:src

# copy the same directory back
scp -r maierbn@ipvslogin:src/numsim .
```

## Installing VTK

Check if cmake runs
```bash
cd build/

cmake ..
```


### From the numsim documentation

If VTK is missing, try to install it:
```bash
# Debian (this did not run on Ubuntu 24.04 LTS)
sudo apt install libvtk7-dev libvtk7.1
```

If that does not work, try to install it manually:
```bash
-wget https://www.vtk.org/files/release/8.2/VTK-8.2.0.tar.gz  # download source archive
-tar xf VTK-8.2.0.tar.gz && cd VTK-8.2.0         # extract files and enter directory
mkdir build && cd build                         # create build directory
cmake .. && make                                # build
sudo make install                               # install (needs password)
```