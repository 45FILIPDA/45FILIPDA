Setting Python PATH (Adjust)
----------------------
> Setting Python PATH

Path_python3.9 = /Applications/QGIS.app/Contents/MacOS/bin/python3.9

### Options 1
> Setting PATH from vim in Terminal :

    - sudo vim .bash_profile
    - Enter Button (i)
    - export PATH="/Applications/QGIS.app/Contents/MacOS/bin:$PATH"
    - Enter Button (esc)
    - :wq

> Chack bash_profile RUN in Terminal : # RUN bash_profile Again

    - source ~/.bash_profile
    - echo $PATH

### Options 2
>  Setting PATH from vim in Terminal :

    - sudo vim /etc/paths
    - Enter Button (i)
    - /Applications/QGIS.app/Contents/MacOS/bin
    - Enter Button (esc)
    - :wq

    หากไฟล์ swap เดิม (/etc/.paths.swp) ยัง ค้างอยู่ ในระบบ! (มันไม่ได้ถูกลบเองตอนออก) ไฟล์ swap เก่าเลยทำให้ตอนเข้าใหม่ขึ้นเตือนแบบนี้อีกครั้ง
        วิธีแก้ที่ตรงจุด:
            กด D เพื่อลบไฟล์ swap ทิ้ง (แล้วจะเข้าไฟล์ได้ตามปกติ ไม่มีปัญหาอีก)
        หรือถ้าต้องการลบด้วยมือ (ใช้ Terminal พิมพ์ลบเองก็ได้) :
            sudo rm /etc/.paths.swp


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
