# Project Workflow (on Windows)

### Step 0. Uninstall Anaconda and install Miniconda.

In the folder where you installed Anaconda (Example: `C:\Users\username\Anaconda3`) there should be an executable called `Uninstall-Anaconda.exe`. Double click on this file to start uninstall Anaconda.

### Step 1: Create a project folder.

On your computer, create folder `MyProject`.

### Step 2: Create conda environment
*Note: Use Anaconda Prompt instead of Windows terminal.*

Create **empty** `conda` environment `myenv` that lives inside the project folder.
    
    conda create --prefix C:\Users\UserName\...\MyProject\myenv
    
Check that the new environment has been created (view list of all your environments):

    conda info --envs

Activate the environment and install all the necessary dependencies, incl. *python executable*:

    conda activate C:\Users\UserName\...\MyProject\myenv 
    conda install python=3.7.3 jupyter numpy pandas scipy matplotlib
    
Check that packages have been installed (view list of all packages installed in your environment):

    conda list
    
*Note:* When you clone someone else's repo from GitHub, you will create an environment from their `environment.yml` file:

    conda create --prefix C:\Users\UserName\...\MyProject\myenv --file C:\Users\UserName\..\..\environment.yml 

Packages that are not available through Anaconda, can be installed using `pip`. Activate the environment and run:

    pip install glob2
    pip install dtaidistance 

Note that for `dtaidistance` to work properly (i.e. using fast C implementation), it is best to install `cython` first, so 

    pip install cython
    
Also, finding OpenMP might be a problem when installing `dtaidistance` on Windows, so option with no OpenMP might work best:

    pip install --global-option=--noopenmp dtaidistance

To use *custom* `*.py` *scripts*, the scripts must be saved in `C:\Users\UserName\...\MyProject\myenv\Lib\site-packages` folder.

### Step 3: conda `environment.yml` file

It would be useful to produce a file listing all the packages and their versions installed inside an environment. This file can be version controlled and shared on GitHub. The convention is to create `environment.yml` file. 

When you clone someone else's repo from GitHub, you can create their environment from this file:

    conda env create -f environment.yml

To create the file, activate the environment, navigate to the environment folder and run (note the pipe operator `>`!):

    conda env export > environment.yml
    
Unfortunately, when your environment lives inside your project folder (as opposed to the default folder `\miniconda\envs\`), exporting it can be buggy.  It is important to activate it, navigate to its folder `.\MyProject\myenv` and use the `--prefix` option:
    
    '(myenv)'C:\Users\UserName\..\MyProject\myenv>conda env export --prefix C:\Users\UserName\..\MyProject\myenv > environment.yml
    
This should create file `environment.yml` inside `..\MyProject\myenv` folder. If you run into problems, see links at the bottom.

### Step 4: Version control

Navigate to your project folder and run:

     git init
     git add C:\Users\UserName\..\MyProject\myenv\environment.yml
     git commit C:\Users\UserName\..\MyProject\myenv\environment.yml -m "conda environment"
    
Now create a new repo on `github`. To avoid errors, do not initialize the new repository with README, license, or gitignore files. You can add these files after your project has been pushed to GitHub.

     git remote add origin https://github.com/username/MyProject.git
     git push -u origin master
     
### Step 5: Jupyter 
*(optional)*
Fire up Jupyter Notebook inside your conda environment:
    
    jupyter notebook
    
 create a notebook, add to `git`, commit and push. 
 
 Note that Jupyter Shell environment is determined by what is your working directory when you run `jupyter notebook` command. For more info, see below links. 
 
 The Python executable being used in the notebook can be determined by running in the notebook cell
 
    import sys
    sys.executable
    
### Step 6: Remove environment

If your environment lives inside the project folder, you have to give its full path after the `--prefix` parameter (`--name` parameter will not work):

    C:\Users\idomaingue>conda env remove --prefix .\PythonJupyterNotebooks\DTW\dtw_env
     
    Remove all packages in environment C:\Users\idomaingue\PythonJupyterNotebooks\DTW\dtw_env: 

Now check that it has been removed:

    C:\Users\idomaingue>conda info --envs
    # conda environments:
    #
    base                  *  C:\Users\idomaingue\Documents\miniconda3

The `dtw_env` folder will still be there, full of `conda-trash` files. You can manually delete it.

### Useful links

[Conda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/index.html) 

[Installing Python Packages from Jupyter](https://jakevdp.github.io/blog/2017/12/05/installing-python-packages-from-jupyter/)

[conda env export fails](https://github.com/conda/conda/issues/1935)
