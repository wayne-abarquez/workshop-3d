Integrating data
================


Cropping and reprojecting
-------------------------

We are only interested with a small extend of the downloaded data. The zone of interest are in the directory zones.

Moreover we want to have data in the same coordinate system (namely EPG:3946).

To get the extend we are interested in can be obtained with:

    ogrinfo -al zones |grep Extent

the result is:

    Extent: (1841372.165967, 5174640.031139) - (1844890.870163, 5176327.053583)

For vector data, we use ogr2ogr to carry out both operations (cropping and reprojection):

    ogr2ogr -clipdst 1841372.165967 5174640.031139 1844890.870163 5176327.053583 -t_srs EPSG:3946 roofs.shp fpc_fond_plan_communaut_fpctoit.shp
    ogr2ogr -clipdst 1841372.165967 5174640.031139 1844890.870163 5176327.053583 -t_srs EPSG:3946 arrondissements.shp adr_voie_lieu.adrarrond.shp
    ogr2ogr -clipdst 1841372.165967 5174640.031139 1844890.870163 5176327.053583 -t_srs EPSG:3946 velov_stations.shp jcd_jcdecaux.jcdvelov.shp

For raster data we use gdalwarp:

    gdalwarp -of gtiff -t_srs EPSG:3946 -te 1841372.165967 5174640.031139 1844890.870163 5176327.053583 MNT2009_Altitude_10m_CC46.tif  mnt.tif
    gdalwarp -of gtiff -t_srs EPSG:3946 -te 1841372.165967 5174640.031139 1844890.870163 5176327.053583 Carte_agglo_Lyon_NO2_2012.tif  N02.tif
