
---
title: "Setup your home directory"
author: "Dr. Eyal Soreq" 
start: true
date: "07/06/2021"
teaching: 60
exercises: 0
questions:
objectives:
- Learn how to setup your home directory again :)
keypoints:

---



# Setup your home directory 

This pipeline is intended to setup your home directory for both the SYS_2021 and MCN_2021 courses

## Start by deleting anything that shouldn't be there  


```bash
%%bash
cd ~
rm -rf archive Background Code Data Notebooks Presentation Report sandbox setups test Tmp
```

## Confirm that fsl folder exists 
if it doesn't download and unpack 


```bash
%%bash
if [[ ! -d ~/fsl ]]
then
  echo "FSL does not exists on your filesystem." 
  mkdir -p  ~/{temp,fsl}
  FSL_TAR=fsl-6.0.4-centos7_64.tar.gz
  echo "Downloading FSL using wget" 
  wget -O ~/temp/$FSL_TAR https://fsl.fmrib.ox.ac.uk/fsldownloads/$FSL_TAR
  echo "Unpacking " 
  tar -xf ~/temp/$FSL_TAR -C ~/ &
else
  echo "FSL exists on your filesystem."
fi
```

    FSL exists on your filesystem.


## Create a `.profile` file to make terminal FSL ready 


```bash
%%bash
tee ~/.profile << END
echo "running my .profile"
source /opt/conda/etc/profile.d/conda.sh
export FSLDIR=$HOME/fsl
export PATH=$PATH:$FSLDIR/bin
export FSLOUTPUTTYPE=NIFTI_GZ
END
```

    echo "running my .profile"
    source /opt/conda/etc/profile.d/conda.sh
    export FSLDIR=/home/jovyan/fsl
    export PATH=/opt/conda/bin:/opt/conda/condabin:/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/bin
    export FSLOUTPUTTYPE=NIFTI_GZ


# Make a MCN_2021 and SYS_2021 folders 


```bash
%%bash
cd ~
mkdir -p {MCN_2021,SYS_2021} 
```

# Check which environments are available


```bash
%%bash
conda env list 
```

    # conda environments:
    #
    SYS_2021                 /home/jovyan/envs/SYS_2021
    base                  *  /opt/conda
    


# Check available kernels


```bash
%%bash
jupyter kernelspec list 
```

    Available kernels:
      sys_2021     /home/jovyan/.local/share/jupyter/kernels/sys_2021
      bash         /opt/conda/share/jupyter/kernels/bash
      ir           /opt/conda/share/jupyter/kernels/ir
      julia-1.6    /opt/conda/share/jupyter/kernels/julia-1.6
      python3      /opt/conda/share/jupyter/kernels/python3
      xpython      /opt/conda/share/jupyter/kernels/xpython


# Define a local envs directory 


```bash
%%bash
if [[ ! -d ~/envs ]]
then
  mkdir -p ~/envs
fi 
conda config --add envs_dirs ~/envs
```

    Warning: '/home/jovyan/envs' already in 'envs_dirs' list, moving to the top


# Write `.condarc` file to double check this is fine 


```python
%%writefile ~/.condarc 
channels:
  - defaults
  - conda-forge
envs_dirs:
  - /home/jovyan/envs
ssl_verify: true
```

    Overwriting /home/jovyan/.condarc


# Create an empty bash kernel for FSL 


```python
!echo y | conda create --name FSL_sandbox --no-default-packages
```

    Collecting package metadata (current_repodata.json): done
    Solving environment: done
    
    
    ==> WARNING: A newer version of conda exists. <==
      current version: 4.10.0
      latest version: 4.10.1
    
    Please update conda by running
    
        $ conda update -n base conda
    
    
    
    ## Package Plan ##
    
      environment location: /home/jovyan/envs/FSL_sandbox
    
    
    
    Proceed ([y]/n)? 
    Preparing transaction: done
    Verifying transaction: done
    Executing transaction: done
    #
    # To activate this environment, use
    #
    #     $ conda activate FSL_sandbox
    #
    # To deactivate an active environment, use
    #
    #     $ conda deactivate
    


# Register that kernel to the jupyter enviorment 


```python
! python -m ipykernel install --user --name=FSL_sandbox
```

    Installed kernelspec FSL_sandbox in /home/jovyan/.local/share/jupyter/kernels/fsl_sandbox


# Confirm that it exists 


```bash
%%bash
jupyter kernelspec list 
```

    Available kernels:
      fsl_sandbox    /home/jovyan/.local/share/jupyter/kernels/fsl_sandbox
      sys_2021       /home/jovyan/.local/share/jupyter/kernels/sys_2021
      bash           /opt/conda/share/jupyter/kernels/bash
      ir             /opt/conda/share/jupyter/kernels/ir
      julia-1.6      /opt/conda/share/jupyter/kernels/julia-1.6
      python3        /opt/conda/share/jupyter/kernels/python3
      xpython        /opt/conda/share/jupyter/kernels/xpython


# Change kernel json to point to bash and have fsl env variables 


```python
%%writefile ~/.local/share/jupyter/kernels/fsl_sandbox/kernel.json
{
 "argv": [
  "/opt/conda/bin/python",
  "-m",
  "bash_kernel",
  "-f",
  "{connection_file}"
 ],
 "codemirror_mode": "shell",
 "display_name": "FSL_sandbox",
 "env": {
     "PS1": "$",
     "FSLDIR":"$HOME/fsl",
     "PATH":"$PATH:$FSLDIR/bin",
     "FSLOUTPUTTYPE":"NIFTI_GZ"
},
 "language": "bash"
}
```

    Overwriting /home/jovyan/.local/share/jupyter/kernels/fsl_sandbox/kernel.json


# Create a python kernel for MCN_2021 (with FSL support)
This section is long and can take upto 60 minutes 

<h2 style="background-color:red;color:white;padding:2%;">USE A BASH TERMINAL</h2>


# Step 1 Create MCN_2021
`conda create --name MCN_2021`

# Once this step has finished 
We need to confirm that we have (at least) `FSL_sandbox` and `MCN_2021` conda environments
and that the `MCN_2021` is active, i.e. has a little  `*` to it's name. 
We will register it to the ipykernel at the same time 

# Step 2 Activate and register it 
~~~bash
. ~/.profile 
conda activate MCN_2021
conda env list
python -m ipykernel install --user --name=MCN_2021
~~~

# And confirm 


```python
! jupyter kernelspec list
```

    Available kernels:
      fsl_sandbox    /home/jovyan/.local/share/jupyter/kernels/fsl_sandbox
      mcn_2021       /home/jovyan/.local/share/jupyter/kernels/mcn_2021
      sys_2021       /home/jovyan/.local/share/jupyter/kernels/sys_2021
      bash           /opt/conda/share/jupyter/kernels/bash
      ir             /opt/conda/share/jupyter/kernels/ir
      julia-1.6      /opt/conda/share/jupyter/kernels/julia-1.6
      python3        /opt/conda/share/jupyter/kernels/python3
      xpython        /opt/conda/share/jupyter/kernels/xpython


# Update kernel to include env variables 


```python
%%writefile ~/.local/share/jupyter/kernels/mcn_2021/kernel.json
{
 "argv": [
  "/opt/conda/bin/python",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "Python (MCN_2021)",
  "env": {
     "FSLDIR":"/home/jovyan/fsl",
     "PATH":"$PATH:/home/jovyan/fsl/bin",
     "FSLOUTPUTTYPE":"NIFTI_GZ"
},
 "language": "python"
}
```

    Overwriting /home/jovyan/.local/share/jupyter/kernels/mcn_2021/kernel.json


# MCN_2021 should now be included in your kernel list 
Switch to it using the right top kernel menu 
And run the following code in the terminal (can take about 5-30 minutes)

~~~bash
conda activate MCN_2021

pip install --user nipype  
pip install --user nibabel 
pip install -U --user nilearn
pip install -U --user joblib
pip install -U --user sklearn

pip install --user nitime 

#we install niwidgets to do interactive plots. 
#It needs an earlier nibabel version (2.5.2) 
pip install --user nibabel==2.5.2 --use-feature=2020-resolver
pip install --user -U niwidgets 

#We also want nipy (which also relies on earlier version of numpy, so we install it in the end)
pip install nipy

#We also want a specific scikit-learn version
pip install scikit-learn==0.22.0
~~~

# Test instellation

Open your notebook and confirm that everything works 


```python
import warnings
warnings.filterwarnings('ignore')
import nipype
import nibabel as nib
import sklearn as skl
import nilearn as nil
import niwidgets as niw
import numpy as np
import scipy

print(f"nipype version {nipype.__version__}")
print(f"nibabel version {nib.__version__}")
print(f"sklearn version {skl.__version__}")
print(f"nilearn version {nil.__version__}")
print(f"niwidgets version {niw.__version__}")
print(f"numpy version {np.__version__}")
print(f"scipy version {scipy.__version__}")
```

# Now install the SYS_2021
- start by creating the self contained setup file 


```python
%%writefile ~/SYS_2021/setup.sh
tee ~/SYS_2021/SYS_2021.yml << END
name: SYS_2021
channels:
  - conda-forge
dependencies:
  - python==3.9
  - numpy
  - pandas
  - scipy
  - statsmodels
  - pingouin
  - scikit-learn
  - matplotlib
  - seaborn
  - plotly
  - pip
  - ipykernel
  - nb_conda_kernels
  - pip: 
    - nibabel

prefix: /home/jovyan/envs/SYS_2021

END

conda env create --file ~/SYS_2021/SYS_2021.yml
conda activate SYS_2021
python -m ipykernel install --user --name SYS_2021 --display-name "Python (SYS_2021)"
```

- Run the setup file 


```python
!source ~/SYS_2021/setup.sh
```

- Test that everything is working by switching to the SYS_2021 kernel 


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib inline
%load_ext autoreload
%autoreload 2
```

- Export a yml snapshot to allow you to recreate the setup on a different computer 


```python
!conda env export --name SYS_2021 > ~/SYS_2021/env_07062021.yml
```
