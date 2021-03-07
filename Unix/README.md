# bash-reference

This repository contains references, utilities and information about related to Unix scripting and processes.  It largely focuses on bash shell scripting in a UNIX/Linux environment.

- [x] Create script/steps for copying bin/ directory locally
- [ ] Create readme/steps for creating/updating the startup files (e.g. .bashrc)

Folders/Concepts included in this repository:

## Working with this repository

Steps to clone, update and use this repository.

* To clone this directory run the following.

```bash
git clone https://github.com/DavidHartman-Personal/kb-bash.git
```

## Windows Subsystem for Linux (WSL)

To add the bin/ folder and set up the various helper scripts/functions, the following steps should be completed.
1. Optionally remote the current root location of the bin/ folder
2. Copy the bin/ folder from this repository to the target location.
3. Recursively set permissions to 750 for bin/ objects.
4. Add bin/ folder to the PATH environment variable if not currently included.
5. Source the import_functions.sh script to make functions available.

The above steps are included in the [setup_bin.sh](setup_bin.sh) script in this repository.

# Resources/Reference
* [GNU Main Bash page](https://www.gnu.org/software/bash/manual/)
* [Bash reference text file](https://www.gnu.org/software/bash/manual/bash.txt)
* [Bash Reference Manual](https://tiswww.case.edu/php/chet/bash/bashref.html)
