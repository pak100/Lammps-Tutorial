## Packmol: Building the Initial Configurations for Your Molecular Dynamics Simulation 
---

### Registering and Installing Packmol 

1. First, register at [packmol.com](http://www.ime.unicamp.br/~martinez/packmol/download.shtml), giving your **name**, your **institution**, and your **email**.  
2. After registering, you can install the packmol.tar.gz file.  

```bash
    > curl -L http://www.ime.unicamp.br/~martinez/packmol/packmol.tar.gz > packmol.tar.gz
    # % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 # Dload  Upload   Total   Spent    Left  Speed
# 100  175k  100  175k    0     0   108k      0  0:00:01  0:00:01 --:--:--  108k
```
---

### Compiling  Packmol

1. Once you have installed the packmol.tar.gz file, you will need to install **fortran**. 
2. The following commands will install gfortran onto your blank workspace. 

```bash 
    > sudo apt-get update 
    # Reading package lists... Done 
```  

3. Now you can install **fortran**.  

```
    > sudo apt-get install -y gfortran

```
5. Next, you need to *expand* your tar file (packmol.tar.gz). 

```
    > tar -xzf packmol.tar.gz. 
```
6. Now, change your directory into the packmol directory. 

```
    > cd packmol/
```
7. From here, you need to compile the source code and link it into an executable file, using the command `make`. You should get the output that 
**packmol was successfully built**.

```
    > make
    # packmol successfully built
```

---
### Testing Packmol 

1. Once you have installed packmol, you need to create your first **input file**, which sets the initial positions of all the atoms in your simulation. First, make sure you are in the packmol directory, then create the file.  

```
    > touch argon.inp
```
2. Now you need to open that file and create its contents. This will allow you to edit the file on a new tab. 

```
    > c9 open argon.inp
```
3. You are now going to set the limitations on the input file by writing the following lines. Spacing and capitalization both affect the input into packmol.
```
tolerance 2.0  
filetype xyz  
output argon.xyz  

structure argon1.xyz  
 number 108
 inside box -20 -20 -20 20 20 20
end structure
```
* The `tolerance` sets the limit on how close atoms can be built together. It is `2.0` for 2.0 Å (angstroms)  
* The `filetype` sets the type of files that this simulation will run. We are going to use the xyz file type.  
* The `output` will create an output file named after what is written after the command. In this case, `output.xyz`.  
* After a line break, the `structure` command uses the information from the **argon1.xyz** file (which you will create next). The program builds from the first three (random) coordinates taken from this file.  
* Each line within the `structure` block is indented by *exactly one space*.
* The `number` sets the number of atoms built from packmol.
* The `inside box` builds the atoms in a 3Dimensional box with coordinates (-x, -y, -z, x, y, z).
* Finally, `end structure` stops running the program.
4. After you have finished writing the limitations save the file with **command S**. 

5. Now you need to create the `argon1.xyz` file, which contains the random coordinates of one atom.

```
    > touch argon1.xyz
    > c9 open argon1.xyz
```
6. Similarly to before, copy and write the following lines into the `argon1.xyz` file.  

```
1  
Argon  
Ar 2 10 8 
```
* The numbers after the `Ar` are the x, y, and z coordinates of your first atom. Feel free to use different numbers, but make sure they are not above or below the box size of -20 and 20. 
7. Save the file again with **command S**. 
8. Now, you can run your input script with packmol. 
```
    > ./packmol < argon.inp
```
9. If the run was a success, then it will give you the running time on the last output line. 
10. Congrats! You just ran your first packmol input file. The packmol program created an **output** file called ``argon.xyz`` (specified on your input script), which contains the coordinates all for the atoms. 

(Still need to add exactly what you should see in the output file to give validation that the observation is correct)