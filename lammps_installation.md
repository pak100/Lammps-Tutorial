## LAMMPS: Large-scale Atomic/Molecular Massively Parallel Simulator 

###Downloading and Installing *LAMMPS*

1. First, return to your workspace folder. 
2. Then, you are going to clone the latest version of LAMMPS from github using the following commands
```
  > git clone https://github.com/lammps/lammps.git
```
3. After downloading, you need to *compile* the LAMMPS program onto your cloud9 workspace.
4. Change your directory into the newly created *lammps* folder
```
  > cd lammps/
```
5. Then, again, change your directory into the source **src** folder.

```
 > cd src
```
6. Here you are going to add the *RIGID* package and then compile LAMMPS.

```
  > make yes-rigid
  > make mpi 
```
7. Congrats! You just installed and compiled the LAMMPS program! Now, move the new file *lmp_mpi* from the *src* folder to the main workspace.

```
> mv lmp_mpi ../..
```
8. The LAMMPS program should now work with a lammps input file. 

###Creating a LAMMPS input file. 
1. 
