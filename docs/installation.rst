Installation
===============

SNAF consists of two major analysis components. The first is unbiased splicing quantification in the software AltAnalyze (Python2) which accurately identities and quantifies alternative splicing events
from RNA-Seq aligned BAM files. The second component is the separate prediction of MHC-bound peptides (T-antigen) and altered surface proteins (B-antigen) from the observed splicing
events. Hence, the installation of SNAF requires two steps, including the download of necessary dependencies and gene models.

Step 1: AltAnalyze
--------------------

A docker image can be downloaded from DockerHub and run using one line of code::

    # build the image
    docker pull frankligy123/altanalyze:0.7.0.1


Alternatively, lots of HPC on university or institution use Singularity instead of docker::

    # pull the image, you may need singularity/3.1 if you run into any error
    singularity build --sandbox altanalyze/ docker://frankligy123/altanalyze:0.7.0.1


Step 2: SNAF
--------------

SNAF is a python3 package and has been tested on python=3.7, we recommend to use the latest developer version instead of stable release (maybe outdated), you
might also need to make sure git is loaded to the env::

    pip install git+https://github.com/frankligy/SNAF.git@e23ce39512a1a7f58c74e59b4b7cedc89248b908


Step 3: Reference Dataset
---------------------------

The reference datasets include gene sequences, exon intron coordinates and other information, such as a human membrane protein database. Downloading all of
these files will save significant time compared to resorting to REST API while calling::

    curl -o download.tar.gz http://altanalyze.org/SNAF/download.tar.gz
    tar -xzvf download.tar.gz

Step 4: (Optional) Install netMHCpan4.1 and TMHMM2.0
-------------------------------------------------------

.. note::

    It is highly recommended to install this two tools. Check the Video tutorial 
    for this step: `Install netMHCpan4.1 and TMHMM2.0 for SNAF <https://www.youtube.com/watch?v=KrAzbR5mRIQ>`_. If you still need help, please directly send me an email and we
    can figure something out.

By default, SNAF uses MHCflurry to predict which peptides will undergo MHC presentation, however, users can optionally install 
netMHCpan4.1 to be used instead. TMHMM2.0 is used for topology prediction in the B-antigen membrane protein workflow if installed. If not installed, results may be less accurate. 
These tools can be downloaded from the authors source websites to get the latest version 
(`netMHCpan4.1 <https://www.cbs.dtu.dk/service.php?NetMHCpan>`_, `TMHMM2.0 <https://services.healthtech.dtu.dk/service.php?TMHMM-2.0>`_). SNAF will ask you
to provide software_path (where do you install these two softwares) when running corresponding steps, that's how these two softwares will be used in SNAF.

Testing installation
-------------------------------------------------------

I provided a dummy input file in the test folder at GitHub, and the script you can executate to test if you can get the exact same result in the result output folder,
if everything goes well, then congratulations, the installation is successful, please contact me if you run into any issue, I am happy to help!


