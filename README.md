"Data Science Workbench"
============

This is a shell script that spins up several popular data science-y server environments on one box. This script is
tested and verified on Ubuntu 14.01.

This environment is built for a fresh install of Ubuntu 14.04. It will update/upgrade all base packages and
install all needed dependencies. Software packages installed include:

 - [R](http://www.r-project.org/)
 - [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/)
 - [Shiny-Server](http://www.rstudio.com/shiny/)
 - [Anaconda Python](https://www.continuum.io/downloads): 
        Anaconda inclues [Jupyter Notebook](http://jupyter.org/) (formerly IPython Notebook).
 - [Jupyterhub](https://github.com/jupyter/jupyterhub): A multi-user server for Jupyter Notebook.
 - [PostgreSQL Database](http://www.postgresql.org/): Because every data science box needs a decent database.

Installation
============

Download or copy the shell script and run it on your Ubuntu box under your home user:

	$ ./data_science_workbench.sh

WARNING: Don't execute as root, it needs your home directory for a couple things.

Server vs. Desktop
============

The two scripts are virtuall identical. The "Desktop" version installs a few more GUI goodies that aren't necessary for a headless setup. Additions include:

 - Rstudio IDE
 - PgAmnin3: Postgres GUI
 - Anaconda launcher: Install and launch Anaconda development tools.


Post-installation
============

Server users will be dumped into a Tmux shell since the Anaconda environment needs a new shell session to take affect.

Desktop users will have to close and re-open a new terminal window.

Once you restart, Anaconda will be your default environment for Python and Pip.

Configuration
=============

After the script finishes, you'll have a few things running on their default ports.

 - RStudio: On localhost:8787 (Username and password set in the script)
 - Shiny-Server: On localhost:3838 (No username or password)
 - Jupyterhub not started by default but you can fire it up with the command `jupyterhub`.
   On localhost:8000 (Username and password are the same as those of the Ubuntu user that ran the script.)
   
Changes in Default Behavior
=============

A few default locations and files have been altered to allow universal access by all users on the system.

 - R: The `Renviron` file has been altered to create a unified package library that is readable by all users and       Shiny-Server. The file is located at `usr/lib/R/etc/Renviron`. 
 - Anaconda: Normally stored in a users home directory, Anaconda is installed in `/opt/anaconda3`.
 - Anaconda: A path has been added to your user's `.bashrc` file to make Anaconda your default for Python and Pip.
The file is located at `home/YOUR_USERNAME`. The added path is at the bottom of the file and is `export PATH="/opt/anaconda3/bin:$PATH"`. This line must be added manually for each new user on the system. The path can    be added by going to the new user's home directory and running: `echo 'export PATH="/opt/anaconda3/bin:$PATH"' >> ~/.bashrc`

SSL Authentication?
=============

By default Jupyterhub use basic authentication, although SSL is available. To set
up SSL, see the [Jupytherhub documentation](https://github.com/jupyter/jupyterhub/blob/master/docs/getting-started.md#Security).

Shiny and RStudio Server are differant stories. Shiny open-souce edition ships with no authentication whatsoever, 
and RStudio Server only wiht basic auth. Both offer "Enterprise" editions, which offer SSL. 

The simple solution
would be to use an Apache2 reverse proxy to add SSL to both, but I have a feeling that may violate the
terms of service. I'm too lazy to read the entire TOS, so I'll just recomend you don't do it. They are both
licensed under [AGPL v3](https://opensource.org/licenses/AGPL-3.0) if anyone is interested.

Other Data Science Boxes
=============

[Data Science Box](https://github.com/drewconway/data_science_box) is based on Ubuntu 12.04 and uses IPython Notebook instead of Jupyterhub.

[Data Science Toolbox](http://datasciencetoolbox.org/) is available as either a Virtualbox image or in AWS. Again, it uses older versions of IPython Notebook but it looks as if it's under active development. 







