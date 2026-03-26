# MDSLabChemBridge
**MDSLabChemBridge** is an integrated R/Python for high-throughput  cheminformatics. It bridges PaDEL, Mordred, CDK, and RDKit into a single  standardized reporting framework, with MDSLab custom descriptor calculation add-on.

# * FOLLOW THE INSTRUCTIONS FOR INSTALLATION *******

# ******** Installation ************

# Download the package zip file #

Steps:

1. MDSLabChemBridge.zip
2. Unzip the folder MDSLabChemBridge.zip
3. Check there should be these files
   
	. R (folder)  
	. DESCRIPTION (file)  
	. MDSLabChemBridge (File)  
	. NAMESPACE
   
5. Inside R folder check these files.
	. .Rhistory (file)  
	. app_function.R (file)
   
7. Check if your R has installed devtools, if not, then install the package
8. Delete any old, broken versions first if you tried installation in wrong way
```(r)
if ("MDSLabChemBridge" %in% installed.packages()) {
  remove.packages("MDSLabChemBridge")
}
```
* Restart R session

7. Install from the SOURCE (not the library)
# This command converts your source files into a valid R library
```(r)
devtools::install("C:/MDSLabChemBridge", upgrade = "never", force = TRUE)     # for example, if your package unzip folder is in the C drive "C:/MDSLabChemBridge"
```

* Restart R session

8. If the above command doesn't work, then try this command. This command automatically installs the package AND all missing libraries
```(r)
devtools::install_local("MDSLabChemBridge.zip", upgrade = "always")
```

9. Run the package in your R/Rstudio
```(r)
library(MDSLabChemBridge)
launch_MDSLabChemBridge()
```
10. The GUI Shiny-App will open. 


Note:   If above installation fails then install directly from GitHub using the command below:

# Install from the local zip file
```(r)
install.packages("C:/Users/YourName/Downloads/MDSLabChemBridge.zip", 
                 repos = NULL, 
                 type = "win.binary") # Use "source" if it's a source zip

```


# ******** Thank You***********

# ****** Have fun with the Package *******************



# Library Required #
```(r)
  library(reticulate)
  library(shiny)
  library(shinyWidgets) 
  library(rcdk)
  library(fingerprint)
  library(tidyverse)
  library(DT)
  library(bslib)
  library(shinycssloaders)
  library(plotly)
  library(uwot)
  library(caret)
```
__________________________________________________________________
