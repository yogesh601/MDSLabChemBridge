# MDSLabChemBridge AI-Tool
## Installation and User Guide

MDSLabChemBridge AI-Tool is an R/Shiny-based cheminformatics application for molecular descriptor generation, feature engineering, dimensionality reduction, clustering, and chemical-space visualization.

This guide provides fresh-installation instructions for **Windows and Linux** users.


### Windows Security / Antivirus

During installation, Windows Security or third-party antivirus software may occasionally block R/Python components, downloaded files, or package installation scripts.

If this occurs:

1. Open **Windows Security → Virus & threat protection → Protection history** and check whether a file was blocked or quarantined.
2. Verify that the blocked file originates from an official source such as the R project, Python, RStudio/Posit, or the official MDSLabChemBridge GitHub repository.
3. If the file is confirmed to be legitimate, allow or restore the file according to your organization's security policy.
4. If necessary, real-time protection may be temporarily paused during the specific installation step. **Turn it back on immediately after the installation is completed.**
5. Do **not** permanently disable Windows Security, Windows Defender, or other antivirus protection.
6. On institutionally managed computers, contact your IT administrator if security policies prevent installation.

> **Security note:** Do not disable antivirus protection permanently. Always verify the source of downloaded files before allowing blocked files or changing security settings.

The official MDSLabChemBridge repository is:

https://github.com/yogesh601/MDSLabChemBridge
---

# 1. System Requirements

| Software | Recommended Version |
|---|---|
| Operating System | Windows 10/11 or Linux |
| R | Latest compatible version |
| RStudio | Latest version |
| Python | **3.9.10** |
| NumPy | **1.26.4** |
| Java | Required by some cheminformatics packages |

> **Important:** Python 3.9.10 and NumPy 1.26.4 are recommended for compatibility with the current application.

---

# 2. Windows Installation

## 2.1 Install Python

Download Python 3.9.10 for Windows:

https://www.python.org/downloads/windows/

During installation:

1. Start the Python installer.
2. Select **Add Python to PATH**.
3. Continue with the default installation.
4. Finish the installation.

Verify from Command Prompt:

```bash
python --version
```

Expected:

```text
Python 3.9.10
```

If the command is not recognized, restart Command Prompt/RStudio after installing Python.

## 2.2 Install R

Download R for Windows:

https://cran.r-project.org/bin/windows/base/

Install R using the default settings.

## 2.3 Install RStudio

Download RStudio:

https://posit.co/downloads/

Install RStudio after installing R and then launch RStudio.

## 2.4 Install Java

Java is required by some cheminformatics packages used by MDSLabChemBridge.

If Java is not already installed, install a suitable Java version and restart RStudio.

## 2.5 Download MDSLabChemBridge

Open:

https://github.com/yogesh601/MDSLabChemBridge

Select **Code → Download ZIP**, then extract the repository.

**Check there should be these files**

	. R (folder)
	. DESCRIPTION (file)
	. MDSLabChemBridge (File)
	. NAMESPACE
  
**Inside R folder check these files**

	. .Rhistory (file)
	. app_function.R (file)


For example:

```text
C:/MDSLabChemBridge
```

or:

```text
D:/MDSLabChemBridge
```

Use the actual folder location on your computer.

## 2.6 Install Required R Packages

Open RStudio and run:

```r
install.packages(c(
  "reticulate",
  "shiny",
  "shinyWidgets",
  "rcdk",
  "fingerprint",
  "tidyverse",
  "DT",
  "bslib",
  "shinycssloaders",
  "plotly",
  "uwot",
  "caret"
))
```

## 2.7 Verify R Packages

```r
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

If these commands run without errors, the required R packages are installed.

## 2.8 Create the Python Virtual Environment

MDSLabChemBridge uses a dedicated Python virtual environment named `r-reticulate`.

Find your Python 3.9 executable. A typical Windows location is:

```text
C:/Users/YOUR_USERNAME/AppData/Local/Programs/Python/Python39/python.exe
```

Create the environment without installing NumPy:

```r
reticulate::virtualenv_create(
  envname = "r-reticulate",
  python = "C:/Users/YOUR_USERNAME/AppData/Local/Programs/Python/Python39/python.exe",
  packages = NULL
)
```

Replace `YOUR_USERNAME` with your Windows username.

## 2.9 Activate the Virtual Environment

```r
reticulate::use_virtualenv(
  "r-reticulate",
  required = TRUE
)
```

## 2.10 Install NumPy 1.26.4

The current application requires NumPy **1.26.4**. Do not use NumPy 2.x for this environment.

The following approach avoids hard-coding the virtual-environment location:

```r
python_exe <- reticulate::virtualenv_python(
  "r-reticulate"
)

system2(
  python_exe,
  c(
    "-m",
    "pip",
    "install",
    "--force-reinstall",
    "numpy==1.26.4"
  )
)
```

## 2.11 Verify NumPy

```r
reticulate::use_virtualenv(
  "r-reticulate",
  required = TRUE
)

reticulate::py_run_string(
  "import numpy; print(numpy.__version__)"
)
```

Expected:

```text
1.26.4
```

## 2.12 Install MDSLabChemBridge

Example:

```r
devtools::install(
  "C:/MDSLabChemBridge",
  upgrade = FALSE,
  force = TRUE
)
```

If the repository is elsewhere, change the path accordingly.

For example:

```r
devtools::install(
  "D:/MDSLabChemBridge",
  upgrade = FALSE,
  force = TRUE
)
```

## 2.13 Launch MDSLabChemBridge

```r
library(MDSLabChemBridge)
launch_MDSLabChemBridge()
```

The Shiny application should open in your default browser or R.

## Delete any old, broken versions first if you tried installing in the wrong way and restart the installation again.
```r
if ("MDSLabChemBridge" %in% installed.packages()) {
  remove.packages("MDSLabChemBridge")
}
```
---

# 3. Linux Installation

The following instructions are intended primarily for **Ubuntu/Debian-based Linux systems**.

## 3.1 Install System Dependencies

Open a terminal and run:

```bash
sudo apt update
```

Then:

```bash
sudo apt install -y \
  r-base \
  python3 \
  python3-pip \
  python3-venv \
  default-jre \
  build-essential \
  libcurl4-openssl-dev \
  libssl-dev \
  libxml2-dev \
  libfontconfig1-dev \
  libharfbuzz-dev \
  libfribidi-dev \
  libfreetype6-dev \
  libpng-dev \
  libtiff5-dev \
  libjpeg-dev
```

Verify:

```bash
R --version
python3 --version
java -version
```

> **Note:** Package names can differ between Linux distributions. The commands above are for Ubuntu/Debian-based systems.

## 3.2 Install RStudio

Download the latest RStudio Desktop for Linux:

https://posit.co/downloads/

For Ubuntu/Debian, download the `.deb` package and install it with:

```bash
sudo apt install ./rstudio-*.deb
```

Then start RStudio.

## 3.3 Install Python 3.9

MDSLabChemBridge recommends **Python 3.9.10**.

Check whether Python 3.9 is available:

```bash
python3.9 --version
```

Find its executable:

```bash
which python3.9
```

For example:

```text
/usr/bin/python3.9
```

> **Important:** The exact Python path depends on your Linux distribution. Do not assume `/usr/bin/python3.9` exists.

## 3.4 Install Required R Packages

Open RStudio and run:

```r
install.packages(c(
  "reticulate",
  "shiny",
  "shinyWidgets",
  "rcdk",
  "fingerprint",
  "tidyverse",
  "DT",
  "bslib",
  "shinycssloaders",
  "plotly",
  "uwot",
  "caret"
))
```

## 3.5 Verify R Packages

```r
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

## 3.6 Create the Python Virtual Environment

If `which python3.9` returns `/usr/bin/python3.9`, run:

```r
reticulate::virtualenv_create(
  envname = "r-reticulate",
  python = "/usr/bin/python3.9",
  packages = NULL
)
```

If your Python 3.9 executable is located elsewhere, replace the path accordingly.

## 3.7 Activate the Virtual Environment

```r
reticulate::use_virtualenv(
  "r-reticulate",
  required = TRUE
)
```

Verify:

```r
reticulate::py_config()
```

## 3.8 Install NumPy 1.26.4

```r
python_exe <- reticulate::virtualenv_python(
  "r-reticulate"
)

system2(
  python_exe,
  c(
    "-m",
    "pip",
    "install",
    "--force-reinstall",
    "numpy==1.26.4"
  )
)
```

## 3.9 Verify NumPy

```r
reticulate::py_run_string(
  "import numpy; print(numpy.__version__)"
)
```

Expected:

```text
1.26.4
```

## 3.10 Download MDSLabChemBridge

Using Git:

```bash
git clone https://github.com/yogesh601/MDSLabChemBridge.git
```

Then:

```bash
cd MDSLabChemBridge
```

Alternatively, download the ZIP file from GitHub and extract it.

## 3.11 Install MDSLabChemBridge

If the repository is located at:

```text
/home/YOUR_USERNAME/MDSLabChemBridge
```

run:

```r
devtools::install(
  "/home/YOUR_USERNAME/MDSLabChemBridge",
  upgrade = FALSE,
  force = TRUE
)
```

Replace `YOUR_USERNAME` with your Linux username.

## 3.12 Launch MDSLabChemBridge

```r
library(MDSLabChemBridge)
launch_MDSLabChemBridge()
```

The Shiny application should open in your browser.

---

# 4. Running Your First Analysis

Once the application opens:

1. Upload your molecular dataset.
2. Select the appropriate analysis/preprocessing options.
3. Start the calculation.
4. Wait until descriptor calculation is complete.
5. Explore the generated descriptors and statistical analyses.
6. Use PCA and UMAP for chemical-space visualization.
7. Download the results as required.

For an initial test, a small SDF dataset is recommended.

---

# 5. Large Datasets

Processing time increases with the number and complexity of molecules and descriptors.

As a general guide:

- **10 compounds:** suitable for an initial test
- **100 compounds:** moderate calculation time
- **1,000 compounds:** may require several minutes

Actual runtime depends on molecular complexity, number of descriptors, CPU/RAM, Python environment, and cheminformatics engine performance.

For large datasets, allow the application sufficient time to complete the calculation.

---

# 6. Troubleshooting

## 6.1 Python is not detected

Run:

```r
reticulate::py_config()
```

You can also check:

```r
system("python --version")
```

On Linux:

```bash
which python3.9
```

Make sure the selected Python version is compatible with the application.

## 6.2 NumPy version is incorrect

Check:

```r
reticulate::py_run_string(
  "import numpy; print(numpy.__version__)"
)
```

The expected version is:

```text
1.26.4
```

If required, reinstall NumPy using the command in the platform-specific installation section.

## 6.3 Virtual environment cannot be found

Run:

```r
reticulate::virtualenv_list()
```

You should see:

```text
r-reticulate
```

Then activate it:

```r
reticulate::use_virtualenv(
  "r-reticulate",
  required = TRUE
)
```

## 6.4 R package installation fails

Try installing the packages individually to identify which package is causing the error.

Some packages may require additional system dependencies, especially on Linux.

## 6.5 Java-related errors

Verify Java:

```bash
java -version
```

On Windows, restart RStudio after installing Java.

On Linux, make sure a Java runtime is installed and available in the system PATH.

## 6.6 Windows security or institutional restrictions

Some Windows security settings or organizational policies may interfere with package installation or executable files.

Check the Windows security notification and make sure RStudio is allowed to access the required files.

If the computer is institutionally managed, contact your system administrator if software installation is restricted.

Do not disable security protections globally unless this is required by your organization's IT/security policy.

---

# 7. Quick Start After Installation

After the initial installation, activate the Python environment and launch the application.

```r
library(reticulate)

reticulate::use_virtualenv(
  "r-reticulate",
  required = TRUE
)

library(MDSLabChemBridge)

launch_MDSLabChemBridge()
```

---

# 8. Fresh Installation Checklist

## Windows

- [ ] Install Python 3.9.10
- [ ] Add Python to PATH
- [ ] Install R
- [ ] Install RStudio
- [ ] Install Java
- [ ] Download MDSLabChemBridge
- [ ] Extract the repository
- [ ] Install required R packages
- [ ] Verify R packages
- [ ] Create `r-reticulate`
- [ ] Activate `r-reticulate`
- [ ] Install NumPy 1.26.4
- [ ] Verify NumPy
- [ ] Install MDSLabChemBridge
- [ ] Launch the application
- [ ] Upload an SDF file
- [ ] Run the analysis

## Linux

- [ ] Install R
- [ ] Install RStudio
- [ ] Install Python 3.9
- [ ] Install Java
- [ ] Install Linux system dependencies
- [ ] Install required R packages
- [ ] Verify R packages
- [ ] Create `r-reticulate`
- [ ] Activate `r-reticulate`
- [ ] Install NumPy 1.26.4
- [ ] Verify NumPy
- [ ] Download/clone MDSLabChemBridge
- [ ] Install MDSLabChemBridge
- [ ] Launch the application
- [ ] Upload an SDF file
- [ ] Run the analysis

---

# 9. Support

For questions, bug reports, or feature requests, please open an issue in the GitHub repository:

https://github.com/yogesh601/MDSLabChemBridge

Thank you for using **MDSLabChemBridge AI-Tool**.
