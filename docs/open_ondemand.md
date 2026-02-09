---
title: Open OnDemand
description: Graphical VNC interface
published: true
date: 2024-11-21T15:26:05.051Z
tags: 
editor: markdown
dateCreated: 2023-08-30T14:12:51.739Z
---

# Open OnDemand

Open OnDemand VNC (Virtual Network Computing) is now available on BMRC. It allows you to access BMRC cluster computing resources via your web browser through a graphical interface. It is especially useful for running graphical applications such as an RStudio, Jupyter or Matlab. It is cross-platform, so it functions on desktops, laptops, tablet computers and even smart phones.

> Before starting using the RStudio through VNC, please follow instruction on setting up the [R environment](/using_r), which includes instruction on setting up ~/.Rprofile.
{.is-warning}


> To be able to use Jupyter Lab/Notebook sessions through Open OnDemand, please install a suitable [Python virtual environment](/python_venv) before attempting to run them. Also, inside each virtual environment, install Jupyter Notebook using `pip install --force notebook`. If you intend to run Jupyter Lab, also install corresponding Python libaries with `pip install --upgrade jupyterlab` command. In addition, prepare a script file with commands that load any required modules and activate your Python virtual environment. For example, a `~/jupyter.sh` file containing:
{.is-warning}

`For gompi/foss-2020a/GCC/GCCcore-9.3.0 toolset:`

```
module load Python/3.8.2-GCCcore-9.3.0
source ~/devel/venv/Python-3.8.2-GCCcore-9.3.0/skylake/bin/activate
```

`For gompi/foss-2022b/GCC/GCCcore-12.2.0 toolset:`

```
module load Python/3.10.8-GCCcore-12.2.0
source ~/devel/venv/Python-3.10.8-GCCcore-12.2.0/skylake/bin/activate
```

Open OnDemand is accessibe at https://ondemand00.bmrc.ox.ac.uk:12000 through your favorite browser (Chrome, Firefox or Safari).

> To log in to the server, enter your BMRC user name and then your BMRC password immediately followed by 6-digit second authentication factor in the same password field.  
{.is-info}

Once logged in, you will see a selection of icons of pre-installed apps. If you do not see them, click on the `OnDemand@BMRC` menu in the top left corner.

> If after entering in your user name and password+authentication code you see `Bad request. Requested resource does not exist` page, shorten the page's url to the https://ondemand00.bmrc.ox.ac.uk:12000 and retry. This should bring up the dashboard page with the pinned apps, if your password and authentication code were correct. 
{.is-warning}

# Jupyter Notebooks/Lab

Once you have installed your [Python virtual environment](/python_venv) and any required Python libraries, you can click on the Jupyter app icon. 

This will open a form, where you can select a suitable partition, specify a script with commands that load the required modules and activate Python virtual environment, for example, `~/jupyter.sh`, as described above, specify CPU and memory requirements for your session. When ready, click on the `Launch` button. This will submit a Slurm job (as if running an srun command) to the queue, and when the job is running, you can connect to it by clicking on the `Connect to Jupyter` button. This will open a Jupyter session in a separate browser tab. You can close the Jupyter session tab and reopen it by clicking the `Connect to Jupyter` button again. The Slurm job will continue running in the background. To terminate the Slurm job, click on the `Delete` button. This will stop the job and disconnect any associated open Jupyter session tabs from the cluster.  

> When running Jupyter Lab session in Open OnDemand VNC, it is important not to select any kernel that you have prepared for Jupyter Lab session in RStudio server, like, for example, a kernel called Python-3.8.2. For Jupyter Lab session in Open OnDemand VNC, always choose the `Python 3 (ipykernel)` kernel.
{.is-warning}

# Free RStudio version

To be able to run the RStudio (KIR) app, it is important to first set up the [R environment](/using_r) and ~/.Rprofile and install any required libraries.

> Please also ensure that the right module trees/paths are set up for use with `module use` command in your ~/.bashrc file. This can be achieved by including `source /well/kir/config/modules.sh` line right after the `# User specific aliases and functions` line in your ~/.basrc file. 
{.is-warning}

To start an RStudio session, click on the RStudio (KIR) app icon. This will open a form, where you can select a suitable RStudio module, queue partition, specify a script with commands that load any additional modules (this can be also achieved after the RStudio session started by running module load commands in the RStudio's Terminal), fill in the job parameters, such as CPU and memory requirements, and click on the `Launch` button to submit a Slurm job to the queue. When it is running, you can connect to it by clicking on the `Connect to RStudio` button. This will open an RStudio session in a separate browser tab. You can close the RStudio session tab and reopen it by clicking the `Connect to RStudio` button again. The Slurm job will continue running in the background. To terminate the Slurm job before it runs out of requested time, click on the `Delete` button. This will stop the job and disconnect any associated open RStudio session tabs from the cluster.  

> An advantage of running RStudio in this way is that you can request required resources from the cluster - you can run as heavy calculation as you want within RStudio without affecting other users. 
{.is-info}

# Remote Desktop

This app allows you to open a graphical remote desktop to access the file system and launch other graphical software, for example, MATLAB. It can be also used for developing Python GUIs with, for example, Tkinter.

To run Remote Desktop, click on the Remote Desktop app. This opens a parameter selection screen. Select the required resources (number of CPUs and amount of memory). When the session starts, select the high compression and high image quality on the sliding bars and click on `Launch Remote Desktop` button.

In the Remote Desktop screen, click on the MATE Terminal icon (top left corner).

