## VMD: Visualize Molecular Dynamics

### Downloading and installing *VMD*

---

1. Head to the [VMD website](http://www.ks.uiuc.edu/Research/vmd/) and click **Downloading VMD** on the left menu. 
2. Click the second option or LINUX_64 OpenGL, CUDA, OptiX, OSPRay. 
3. Now, you need to **register** with VMD in order to get the tarball file to download. 
4. Once, you agree to their terms and conditions, your tarball file should start downloading shortly afterwards. 
5. Now change your directory out of the `cloud9-vnc` directory back into the `workspace`.
```
    > cd ..
```
5. Now, using the cloud9 menu options clicking *file* and *upload local files*, select recent downloads and select the **vmd-1.9.3.bin.LINUXAMD64-CUDA8-OptiX4-OSPRay111p1.opengl.tar.gz**.
6. You need to expand the tarball file
```
    > tar -xf vmd-1.9.3.bin.LINUXAMD64-CUDA8-OptiX4-OSPRay111p1.opengl.tar.gz
```
7. This will create a new directory called `vmd-1.9.3`. Change your directory into the directory.

```
    > cd vmd-1.9.3
```
8. Once you are in the directory, configure the program with the following command. If successful, will return a message listing the configuration options.
```bash
    > ./configure 
    # using configure.options: LINUXAMD64 OPENGL OPENGLPBUFFER FLTK TK ACTC CUDA IMD LIBSBALL XINERAMA XINPUT LIBOPTIX LIBOSPRAY LIBTACHYON VRPN NETCDF COLVARS TCL PYTHON PTHREADS NUMPY SILENT ICC
```
9. Now, change you directory into the `src` directory and make install the program. Since this runs in Cloud9, the installer will use bash. If successful, will output a congratulatory message.

```bash
    > cd src
    > sudo make install
    # Info: /bin/csh shell not found, installing Bourne shell startup script instead
    # Make sure /usr/local/bin/vmd is in your path.
    # VMD installation complete.  Enjoy!
```
10. You should get a success output. This means VMD can be run on cloud9 with the command `vmd`. 
11. To test the installation, run vmd. You should get a vmd-specific console prompt. Type `quit` at the prompt to exit vmd.
```bash
    > vmd
    # vmd > quit
    # Info) VMD for LINUXAMD64, version 1.9.3 (November 30, 2016)
    # Info) Exiting normally.
```
    
## Installing No-VNC into Cloud9

 1. As you probably know now, cloud9 is a *cloud* computer, but it does not have a screen, which we will need to manipulte the atoms on **VMD**.  
 2. In order to make sure that cloud9 has the right graphics processing, you will need to install **Mesa**

```bash
    > sudo apt-get install libglu1-mesa-dev freeglut3-dev mesa-common-dev

````
3. Now, you can clone the **no-Vnc** from github

```
    > git clone https://github.com/garcias/cloud9-vnc.git

```
4. Now, *change directories* into the newly created **cloud9-vnc** dicrectory 

```
    > cd cloud9-vnc\
```
5. Now you need to fully **install** No-vnc. Once you are in the directory run the next command to install the program. 
```
    > ./install.sh
```
* It takes a minute, but you should get a final **done.** in the last output line. 

6. **firefox.conf** contains the phrase `firefox` twice at the end of the file. Create a file named **vmd.conf** with the same content, but with `firefox` replaced with `vmd`. You can open the file, make the changes, and save as **vmd.conf**; or use `sed` substitution.
```bash
    > sed s/firefox/vmd/g firefox.conf > vmd.conf
```
7. Check the new file by opening it (or with `tail -3 vmd.conf`). The last three lines should look like:
```
    [program:vmd]
    command=vmd
    environment=DISPLAY=":99"
```


### Using VMD

1. Change your directory out of the `vmd-1.9.3`, and go back into the `cloud9-vnc` directory. This is where you will do most of the work with VMD, in the `cloud9-vnc` directory. 

```
    > cd ..
    > cd cloud9-vnc/
```
2. Run the **No-VNC** program with **VMD** attached, using the following command. 

```
    > ./run.sh vmd.conf
```
3. This will create a stream of output lines that will always continue until you are done using **no-vnc**. You need to click on the second line, where there is a web address. For example, I would click `https://novncintovmd-usr.c9users.io:8080/vnc.html`.
```
    VNC client running at https://novncintovmd-pak100.c9users.io:8080/vnc.html
```
4. Clicking the web address should create a new tab and clicking **connect**, you should soon see the **VMD** program working on a mirrored screen. 
5. Now, you can start to use **VMD** to look at your packmol or other molecular dynamics files. 
