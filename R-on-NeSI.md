# Using R on NeSI

First, let's check for the most recent R module:

Log in to NeSI, (if via Jupyter you can upload your script via drag and drop, otherwise use scp from your local command line).
    module spider R/4

This looks for modules of R that are version 4.X

Load the preferred module (preference for one built with gimkl)
    module load R/4.3.1-gimkl-2022a

Check your R script to see if there are specific libraries that you need to have installed. If there are, we need to enter an R environment to install these - they'll remain available next time you use R.

Check whether you have an Rpackages directory already in place in your project directory.
If not, you may need to make it:
    mkdir /nesi/project/PROJECTCODE/Rpackages/4.3.1/

Now make that directory available to R:
    export R_LIBS=$R_LIBS:/nesi/project/PROJECTCODE/Rpackages/4.3.1/

Now let's start our R environment:
    R

The command line will change to an R-environment.
Now let's install packages:
    install.packages("PACKAGE_NAME". lib="/nesi/project/PROJECTCODE/Rpackages/4.3.1")
If the above doesn't work, change the . to a , (can't remember which is correct)

When you finish installing your packages, you can exit the R environment:
    q()

To run an R or Rmarkdown script on NeSI, you probably need to add the R_LIBS line to the start of the script so it knows where to look for your installed packages - I don't remember properly how that works for markdown so recommend googling to double check.

Now you only need to have the R module loaded, no need to enter an R environment.

Navigate to where your script is
    cd DIRECTORY

Render Rmarkdown via command line
    Rscript -e "rmarkdown::render('FILENAME.Rmd')"

For regular .R scripts, you can use
    Rscript FILENAME.R

Don't forget to close the module when you're finished
    module purge