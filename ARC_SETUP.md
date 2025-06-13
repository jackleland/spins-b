Two repos:
1. https://github.com/jackleland/spins-b - forked with some bug fixes
2. https://github.com/jackleland/maxwell-b - gpu maxwell solver, running but not on ARC (yet)

Instructions:
1. Log in to arc
2. (optional) you probably want to get an interactive node to speed things up, which you can do with `srun -p interactive --pty /bin/bash`. This by default gives you a whole node, which is 28 cores.
3. `module load Mamba`
4. if you've not used mamba before you'll need to do `mamba init` and then restart from step 2
5. `mamba create -n spins-b python=3.8`
6. `mamba activate spins-b`
7. Do a quick check to make sure we're using the correct pip, with `which pip` which should point to something like `~/.conda/envs/spins-b/bin/pip`
8. `cd` into the spins-b repo
9. `make install`

That should get you a basic working version of spins-b installed with the direct solver (i.e. cpu). I'll try and finish off porting the GPU solver to ARC next week!

To give everything a try you can run the `examples/goos/bend90/bend90_simple.py` script, which I've modified to get working without the cubic interpolation (which has an error I've not been able to get to the bottom of).

To run it, simply use
``` bash
bend90_simple.py run FOLDER_NAME
```
and then to view the output/save a figure use:
``` bash
bend90_simple.py view FOLDER_NAME
```
where FOLDER_NAME has been changed for the name of the folder you want to save to.


I've also put the progress I made towards recreating Olly's 1d grating from PIRL in a notebook at `examples/interactive_colab/grating_1d_modified.ipynb` but it doesn't actually run anything without having some kind of optimisation to work towards. Things I would try:
- have it optimise some meaningless part of the sim window for 1 step and then view the output
- interface directly with the solver, i.e. capture the files it sends to the solver somehow and modify them to get the output you want.

to-do:
- [ ] Working GPU solver in SIngularity container
- [ ] start jupyter server from ARC and feed through to local browser
