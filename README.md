# Project Workflow (on Windows)

### Step 0. Uninstall Anaconda and install Miniconda.

In the folder where you installed Anaconda (Example: `C:\Users\username\Anaconda3`) there should be an executable called `Uninstall-Anaconda.exe`. Double click on this file to start uninstall Anaconda.

### Step 1: Create a project folder.

On your computer, create folder `MyProject`.

### Step 2: Create conda environment
*Note: Use Anaconda Prompt instead of Windows terminal.*

Create `conda` environment `myenv` that lives inside the project folder.
    
    $ conda create --prefix C:\Users\UserName\...\MyProject\myenv
    
Check that the new environment has been created (view list of all your environments):

    $ conda info --envs

Activate the environment and install all the necessary dependencies:

    $ conda activate C:\Users\UserName\...\MyProject\myenv 
    $ conda install python=3.7.3 jupyter numpy pandas scipy matplotlib
    
Check that packages have been installed (view list of all packages installed in your environment):

    $ conda list
    
Packages that are not available through Anaconda, can be installed using `pip`. Activate the environment and run:

    $ pip install dtaidistance 
    
If you want to use modules (functions) inside user created `*.py` scripts, the scripts must be saved in `C:\Users\UserName\...\MyProject\myenv\Lib\site-packages` folder.

### Step 3: Export conda environment

Export conda environment into `environment.yml` file. Activate the environment and run (note the pipe operator `>`!):

    $ conda env export > environment.yml
    
`environment.yml` file should be version controlled. It can be shared, i.e. someone else can create the exact same environment from your `environment.yml` file.
    
    conda env create -f environment.yml
    
Unfortunately, when your environment lives inside your project folder (as opposed to the default folder `\miniconda\envs\`), exporting it can be buggy.  Before exporting, make sure the environment is activated. Also, navigate to its folder `.\MyProject\myenv`. 
    
    $ '(myenv)'C:\Users\UserName\..\MyProject\myenv>conda env export --prefix C:\Users\UserName\..\MyProject\myenv > environment.yml
    
This should create file `environment.yml` inside `..\MyProject\myenv` folder. If you run into problems, see links at the bottom.

### Step 4: Version control

Navigate to your project folder and run:

     $ git init
     $ git add C:\Users\UserName\..\MyProject\myenv\environment.yml
     $ git commit C:\Users\UserName\..\MyProject\myenv\environment.yml -m "conda environment"
    
Now create a new repo on `github`. To avoid errors, do not initialize the new repository with README, license, or gitignore files. You can add these files after your project has been pushed to GitHub.

     $ git remote add origin https://github.com/username/MyProject.git
     $ git push -u origin master
     
### Step 5: Jupyter 
*(optional)*
Fire up Jupyter Notebook inside your conda environment:
    
    $ jupyter notebook
    
 create a notebook, add to `git`, commit and push. 

    
### Useful links

[Conda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/index.html) 

[Installing Python Packages from Jupyter](https://jakevdp.github.io/blog/2017/12/05/installing-python-packages-from-jupyter/)

[conda env export fails](https://github.com/conda/conda/issues/1935)
