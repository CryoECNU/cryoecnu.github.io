---
layout: page 
title: "常用计算机技术" 
description: "工欲善其事，必先利其器" 
header-img: "img/top.png" 
---

1. Softwares List (mainly for Mac) - updated: 2017-09-29

	- **Github Desktop**: [https://desktop.github.com/](https://desktop.github.com/)
	- **MarkDown IDE for Mac OS**: [https://macdown.uranusjr.com/](https://macdown.uranusjr.com/)
	- **Anaconda**: [https://www.anaconda.com/download/](https://www.anaconda.com/download/)
	- **QGIS**: [http://www.qgis.org/en/site/forusers/download.html](http://www.qgis.org/en/site/forusers/download.html)
	- **gcc & gfortran**: [http://hpc.sourceforge.net/](http://hpc.sourceforge.net/)
	- **NCL/NCAR**: [http://www.ncl.ucar.edu/Download/](http://www.ncl.ucar.edu/Download/)
	- **CDO**: [https://code.mpimet.mpg.de/projects/cdo/](https://code.mpimet.mpg.de/projects/cdo/)
	- **Panoply (Gridded data viewer)**: [https://www.giss.nasa.gov/tools/panoply/](https://www.giss.nasa.gov/tools/panoply/)
	- **Texmaker (Tex IDE)**: [http://www.xm1math.net/texmaker/](http://www.xm1math.net/texmaker/)
	- **MacTex (Latex for Mac OS)**:[http://www.tug.org/mactex/](http://www.tug.org/mactex/)

1. Install packages in Anaconda - updated: 2017-09-29

	1.	Create a **NEW** python environment
		> * Pip 9.0.1
		> * Python 2.7.13
		> * Setuptools 27.2.0
		> * Vs2008_runtime 9.00.30729.5054
		> * Vs2015_runtime 14.0.25420
		> * Wheel 0.29.0
		
	1. install pkgs using **Terminal** BY the **ORDER** of:
		> 1. conda install -y -c conda-forge basemap 
		> 1. conda install -y pandas scipy simplejson
		> 1. conda install -y -c conda-forge rasterio
		> 1. pip install pyshp pycrs shapely netcdf4
		> 1. conda install -y -c conda-forge gdal=2.0
		> 1. conda install -c anaconda statsmodels
		
		**OR specify the version**
		
		> 1. conda install -y -c conda-forge basemap=1.1 pandas=0.20.3 scipy=0.19.1 simplejson=3.11.1 gdal=2.0 rasterio=0.25.0 shapely=1.6.1 netcdf4 pyshp=1.2.12 statsmodels=0.8.0 krb5=1.14.2 pillow pkg-config gsl gcc
		
		> 1. pip install pycrs==0.1.3		
		
	1. install my package:
		> 1. git clone https://wk1984@bitbucket.org/wk1984/quick-analysis-and-visualization.git
		> 1. cd quick-analysis-and-visualization
		> 1. python setup.py install
		
	1. test:
	
		> python -c "from QuickPlots import QuickPlots"
		
		> python -c "import QuickPlots;print QuickPlots.__version__"
		
	1. Q&A:
	
		- Library not loaded: @loader_path/./libgssapi_krb5.2.2.dylib
			
			> conda install krb5
		
1. Install **MacPorts** - updated: 2017-10-10

	1. Install **Xcode**: Huge file > 5 GB 
		
		[Apple Store](https://itunes.apple.com/us/app/xcode/id497799835?mt=12)
		
		see details: [https://guide.macports.org/#installing.xcode](https://guide.macports.org/#installing.xcode)
			
	1. Install **Xcode Command Line Tools**:
	
		> xcode-select --install
	
	1. Agree to Xcode license in Terminal:

		> sudo xcodebuild -license
		
	1. Download and install MacPorts for your version of the Mac operating system:

		- [High Sierra 10.13](https://github.com/macports/macports-base/releases/download/v2.4.2/MacPorts-2.4.2-10.13-HighSierra.pkg)
		- [Sierra 10.12](https://github.com/macports/macports-base/releases/download/v2.4.2/MacPorts-2.4.2-10.12-Sierra.pkg)
		- [El Capitan 10.11](https://github.com/macports/macports-base/releases/download/v2.4.2/MacPorts-2.4.2-10.11-ElCapitan.pkg)

		Just Double-Click pkg file!
		
1. Install **CDO** by using MacPorts:

	CDO = **C**limate **D**ata **O**perators
	
	Homepage = [https://code.zmaw.de/projects/cdo](https://code.zmaw.de/projects/cdo)
	
	> sudo port install cdo
	
	To test whether it is installed rightly:
	
	> cdo -V

1.	Install **ILAMB** in Anaconda.

	- create a new env for installing ILAMB (**recommend**)
	- install all requirements:
	
		> conda install -c conda-forge -y numpy matplotlib netcdf4=1.2.4 sympy scipy mpi4py cfunits basemap
		
	- download **ilamb** from Bitbucket, then install:
	
		> git clone https://wk1984@bitbucket.org/ncollier/ilamb.git
		
		> cd ilamb
		
		> python setup.py install
		
	- test:

		> python -c "import ILAMB; print ILAMB.__version__" 

1. Install **NCL**:

Notes: It should be **consistent generation** between gcc and gfortran from http://hpc.sourceforge.net/ and "gcc-x.y.bin.tar.gz" file. e.g, *ncl_ncarg-6.4.0-MacOS_10.12_64bit_nodap_gnu530.tar.gz* needs *gcc-5.1-bin.tar.gz*. If you install any other versions of gcc/gfortran, it would notice like:
	
	> dyld: Library not loaded: /usr/local/lib/libgfortran.3.dylib
	> Referenced from: /usr/local/ncl-6.4.0/bin/ncl
	> Reason: image not found
	
- Install XQuartz from [https://dl.bintray.com/xquartz/downloads/XQuartz-2.7.11.dmg](https://dl.bintray.com/xquartz/downloads/XQuartz-2.7.11.dmg)

- For Bash environment: add three lines to ~/.bash, or ~/.bash_profile
	
	> export DISPLAY=:0.0
	
	> export NCARG_ROOT=/usr/local/ncl-6.4.0
	
	> export PATH=$NCARG_ROOT/bin:$PATH
	
	Save and Quit:
	press "esc", and input 'wq' following the ":"
	
	>:wq
	
	After that, make the change active.
	
	> source ~/.bash_profile
	
- Test whether it works well (before using NCL, you need to launch XQuartz, otherwise, it will not work!):

	> ng4ex gsun01n

The example looks like:

<center>
<p><img src="/img/ncl_test.png" align="center"></p>
</center>
-----
