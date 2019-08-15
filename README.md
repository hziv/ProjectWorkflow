### Project Workflow (on Windows)

Step 0. Uninstall Anaconda. 

In the folder where you installed Anaconda (Example: `C:\Users\username\Anaconda3`) there should be an executable called `Uninstall-Anaconda.exe`. Double click on this file to start uninstall Anaconda.

### Step 1:
Install Miniconda. 

### Step 2:
Create a project folder on your computer.

### Step 3: 
*Note: Use Anaconda Prompt instead of Windows terminal.*

Create a `conda` environment `myenv` that lives inside the project folder.
    
    $ conda create --prefix C:\Users\UserName\...\MyProject\myenv
    
Check that the new environment has been created:

    $ conda info --envs

Activate the environment and install all the necessary dependencies:

    $ conda activate C:\Users\UserName\...\MyProject\myenv 
    $ conda install python=3.7.3 jupyter numpy pandas scipy matplotlib
    
Check that packages have been installed:

    $ conda list
    
Packages that are not available through Anaconda, can be installed using `pip`. Activate the environment and run:

    $ pip install dtaidistance 

### Step 4: 
Export conda environment into `environment.yml` file.

    $ conda env export --prefix C:\Users\UserName\..\MyProject\myenv > environment.yml
    
This will create file `environment.yml` inside `..\MyProject\myenv` folder.

### Step 5.
Please project folder and `environment.yml` file under version control.

     $ git init
     $ git add C:\Users\UserName\..\MyProject\myenv\environment.yml
     $ git commit C:\Users\UserName\..\MyProject\myenv\environment.yml -m "conda environment"
     $ git create 
     $ git push -u origin master

    
