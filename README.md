# Basics

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
