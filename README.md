# CuoidMACC-BCP2

## MACC Setup and Run
This is the minimal setup needed to run MACC on a new machine.
### 1. Create the Conda environment
From the repository root:
``` bash
conda env create -f environment.yml
conda activate macc
```
### 2. Update the C++ Makefile paths
Go to:
``` bash
cd src/assembly/cpp
```
Open the Makefile and update any machine-specific paths such as:
``` bash
MACC_HOME
PYBIND_INCLUDE
PYTHON_INCLUDE
PYTHON_EXT_SUFFIX
```
Useful commands for finding the correct values:
``` bash
pwd #repo path
python -c "import sysconfig; print(sysconfig.get_paths()['include'])" # Python include path
python -c "import pybind11; print(pybind11.get_include())" # pybind11 include path 
python -c "import sysconfig; print(sysconfig.get_config_var('EXT_SUFFIX'))" # Python extension suffix

```
Then compile:
``` bash
make #Return to the repository root:
```

### 3. Run MACC
Make sure the environment is active:
``` bash
conda activate env

# Create the results folder if not already:
# mkdir -p results/myTestRun
# Run from the repository root:
PYTHONPATH=src python - <<'PY'
from parallelization.run_structures_updated import process_folder_of_structures

results = process_folder_of_structures(
    in_folder="src/data/random_10x10x4_15blocks",
    out_folder="out/myTestRun",
    structure_prefix="random_10x10x4_15block_n",
    x_dim=10,
    y_dim=10,
    z_dim=4,
    num_structs=1,
    time_limit=300,
)

print(results)
PY
```