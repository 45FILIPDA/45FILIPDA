Setting Python PATH (Adjust)
----------------------
> Python PATH

Path_python3.9 = /Applications/QGIS.app/Contents/MacOS/bin/python3.9

In Terminal :
sudo vim .bash_profile #กำหนดPathที่ค้นหาในvim
	> i #เพื่อinsertลงvim
	> export PATH="/Applications/QGIS.app/Contents/MacOS/bin:$PATH"
	> esc
	> :wq
source ~/.bash_profile #ให้Terminalรันbash_profileใหม่
echo $PATH #เช็คว่าpathที่สืบค้นโปรแกรม

sudo vim /etc/paths
	> i #เพื่อinsertลงvim
	> /Applications/QGIS.app/Contents/MacOS/bin
	> esc
	> :wq

Chack Package
----------------------
  Use Python from Qgis and install Package

-   GeoPandas, rasterio, shapely, ee, geemap, matpoltlib, xml.etree.elementtree, folum, h3, scikit learn and seaborn
  
install All Package Used : 

> Use pip for Install Package in Terminal:

    pip install geopandas
    pip install rasterio
    pip install shapely
    pip install ee
    pip install geemap
    pip install matplotlib
    pip install elementpath
    pip install folum
    pip install h3
    pip install scikit-learn
    pip install seaborn

import Package
----------------------
Import Package For Used:

    import os
    import sys
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    import matplotlib.image as img
    import matplotlib.lines as mlines
    from matplotlib.colors import ListedColormap
    import seaborn as sns
    import earthpy as et 
    from qgis.analysis import QgsZonalStatistics
    from qgis.core import QgsVectorLayer,QgsRasterLayer
    import time
    import shutil
    import contextlib
    import install
    import geopandas as gpd
    import  scipy.signal.signaltools
    
    def _centered(arr, newsize):
        # Return the center newsize portion of the array.
        newsize = np.asarray(newsize)
        currsize = np.array(arr.shape)
        startind = (currsize - newsize) // 2
        endind = startind + newsize
        myslice = [slice(startind[k], endind[k]) for k in range(len(endind))]
        return arr[tuple(myslice)]

    scipy.signal.signaltools._centered = _centered
    import statsmodels.api as sm
    from statsmodels.formula.api import poisson
    from statsmodels.formula.api import glm
    import scipy

