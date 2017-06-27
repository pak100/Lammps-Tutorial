## VMD: TopoTools
* This tutorial will explain how to get an input file ready for the lammps program. 
* There are two things that you need to be able to use all the features of this tutorial
    * A functional VMD program (see VMD.md to download and install VMD)
    * A packmol output file

### Periodic Boundary Conditions: These simulate an infinite system

1. First, load an packmol output file into the VMD program by selecting **New Molecule** in the VMD main window.
2. After loading an output file, select the **Extensions** and scroll down to the **Tk Console**. The Tk Console behaves like a terminal accepting input commands. 
3. To find out what the periodic boundaries are, use the command `pbc get`. The first three numbers of this output will be the x, y, and z perimeters. 
4. You should get 0.0, 0.0, 0.0 for a standard packmol output file. To change these so x,y, and z all are "120" use the following command
```
    > pbc set "120 120. 120."
```
This sets the x, y, z parameters for the peridoic boundaries. 
5. Now, check your periodic boundaries using the command `pbc box`. This command should put a blue box around the atoms.
6. If the box is not around the atoms, you can move the atoms to move inside the box using the following commands
```
    >set sel [atomselect top "all"]
    # atomselect1
    >$sel moveby "10 10 10"
```
This moves the atoms by the x,y, and z numbers specified in the quotations. 

### Combining Two Packmol Output Files into one File
1. Load the first output file into VMD by selecting **New Molecule** in the VMD main window.
2. Then, head to the **Tk Console** by selecting **Extensions** and clicking **Tk Console**. This opens a terminal that accepts commands to manipulate the atoms. 
3. Find out what the periodic boundary conditions are by using the following commands. 
```
    > pbc get
    # {0.00000 0.00000 0.00000 90.000 90.000 90.000}
```
* With that command it will output numbers in brackets. The first three numbers are the x, y, z periodic boundary conditions for you simulation. 
4. Now set the periodic boundaries with the following commands. 
```
    > pbc set "100 100 100"
``` 
5. Now, load the second output file into VMD with the same method as step 1. 
6. Again, go to **Tk console** and find out what the periodic boundary conditions are for the second packmol file. 
7. Now, use the `pbc get` command to get the peridoic boundary conditions for the latest file. 
8. Set the peridoic Boundary conditions to match the conditions from the first file. 
9. After setting the periodic boundary conditions for both input files, you now need to merge them into one file. Use the follwoing commands to merge the two files with **part1.xyz** representing your first file and **part2.xyz** as your second file.  

```
    >set midlist {}
    >set mol [mol new part1.xyz waitfor all]
    #1 
    >mol addfile [part1.xyz]
    #1
    > lappend midlist $mol
    #1
    > set mol [mol new part2.xyz waitfor all]
    #2
    >mol addfile [part2.xyz]
    #2
    >mol addfile part2.xyz $mol
    #2
    >lappend midlist $mol
    #1 2 
    >set mol [::TopoTools::mergemols $midlist]
    # 3
    >animate write xyz merged.xyz $mol
    #1
    >animate write pdb merged.pdb $mol
```
* You can control the name of your file in the animate file **merged.xyz** will be the new file name. 

### Preparing a Input File for Lammps 
1. Load the file into VMD by selecting **New Molecule**
2. Then select **Extensions** scrolling down to the **Tk Console**. This will open a terminal in a new window. 
3. Use the following commands to prepare an input file for lammps
```
    >topo writelammpsdata filename.input
```
4. Now you can use the new file you created as an input file into the Lammps program. 
