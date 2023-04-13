# Installation Steps

In order to build arkouda and arkouda-njit on M1/M2 Macbooks you need to follow the steps given below:

1. Install Anaconda Navigator. Ensure it is pointed to in your `PATH`

**NOTE: Install the Graphical Installer for M1 Macbooks and NO other installers.**

Link - [https://repo.anaconda.com/archive/Anaconda3-2023.03-MacOSX-arm64.pkg](https://repo.anaconda.com/archive/Anaconda3-2023.03-MacOSX-arm64.pkg)

2. `git clone` arkouda and arkouda-njit and download Chapel. Extract the tar chapel file with `tar xzf chapel-1.28.0.tar.gz` .
3. Create an anaconda environment from the `arkouda-env-dev.yml` from within arkouda base repo.
4. To `Makefile.paths` within arkouda base add in `$(eval $(call add-path,$(eval $(call add-path,/Users/narenkhatwani/anaconda3/envs/arkouda-env-dev))))` . Where the path is your system’s absolute path to the arkouda-dev environment you just created.
5. Comment out `CHPL_RE2` lines in `CHPL_HOME/util/quickstart/setchplenv.bash`.
6. Fire up a Terminal and run `source CHPL_HOME/util/quickstart/setchplenv.bash` 
7. Run  the following lines in the terminal 

```bash
export CHPL_LLVM=system
export CHPL_TARGET_CPU=none
export CHPL_RE2=bundled
export CHPL_GMP=system
```

8. Activate your conda environment that you created earlier using `conda activate arkouda-env-dev` 
9. Head to the arkouda directory in the terminal and run `make` 
10. If arkouda was successfully built you will see something like:

```bash
11 createTaskFunctions                  0.007    0.003    0.018    0.028   0.0  289.830 100.0
   5 cleanup                              0.021    0.000    0.004    0.025   0.0  289.855 100.0
   9 checkNormalized                      0.002    0.000    0.013    0.015   0.0  289.870 100.0
   7 flattenClasses                       0.000    0.000    0.005    0.005   0.0  289.875 100.0
   3 readExternC                          0.000    0.000    0.005    0.005   0.0  289.880 100.0
   4 expandExternArrayCalls               0.000    0.000    0.004    0.005   0.0  289.885 100.0
     startup                              0.000    0.000    0.000    0.000   0.0  289.885 100.0
     driverCleanup                        0.000    0.000    0.000    0.000   0.0  289.885 100.0

     total time                         283.186    0.465    6.234  289.885
```

11. Head to the arkouda-njit directory from the terminal and run `make` If it was built successfully, you will see something like:

```bash
9 checkNormalized                      0.007    0.000    0.059    0.067   0.0  377.675 100.0
   2 checkUast                            0.048    0.001    0.007    0.057   0.0  377.732 100.0
   5 cleanup                              0.033    0.000    0.009    0.042   0.0  377.774 100.0
   7 flattenClasses                       0.000    0.000    0.008    0.008   0.0  377.782 100.0
   3 readExternC                          0.000    0.000    0.007    0.007   0.0  377.789 100.0
   4 expandExternArrayCalls               0.000    0.000    0.007    0.007   0.0  377.796 100.0
     startup                              0.000    0.000    0.000    0.000   0.0  377.796 100.0
     driverCleanup                        0.000    0.000    0.000    0.000   0.0  377.796 100.0

     total time                         364.693    0.756   12.348  377.796
```

12. Now you need to create a symbolic link between arkouda and arkouda-njit, run this 

```bash
ln -s /Users/narenkhatwani/Desktop/arkouda-4/arkouda-njit arkouda_njit
```
13. Head to the arkouda directory and run `./arkouda_server nl -1` in the terminal

## Some errors that I faced, what the issue was, and how did I resolve them

## Running arkouda-contrib

In order to build arkouda-contrib on M1/M2 Macbooks you need to follow the steps given below:

1. Head to the arkouda-contrib directory on your machine
2. Run the following command

```bash
python3 module_configuration.py --ak_loc=/complete/path/to/arkouda/ --pkg_path=/complete/path/to/arkouda-
contrib/arkouda_distance_wserver/
```

1. The output after running the above command the output will be a command which you need to run next, the command starts with the phrase `cp`

DO NOT RUN THE COMMAND BELOW, ITS JUST AN EXAMPLE

Example:

```bash
cp /complete/path/to/arkouda/ServerModules.cfg ~/TmpServerModules.cfg.1660849671
ARKOUDA_SERVER_USER_MODULES=" /complete/path/to/arkouda-contrib/arkouda_distance_wserver/server/DistanceCalcMsg.chpl" ARKOUDA_CONFIG_FILE=~/TmpServerModules.cfg.1660849671 ARKOUDA_SKIP_CHECK_DEPS=true make -C /complete/path/to/arkouda
```
