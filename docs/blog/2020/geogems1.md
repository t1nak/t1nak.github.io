
# Table of Contents
* [Examples (in jupyter notebook)](#Examples-%28run-in-jupyter-notebook%29)

	* [1. Start geogems and load images](#first-bullet)
        * [Show wet and dry season from sentinel 2 images for Malawi](#firstb-bullet)
            * [Dry season](#Dry-season)
            * [Wet season](#Wet--season)
	* [2. Load landcover satellite images](#second-bullet)



```python
!pip search geogems
```

    geogems (0.1.2)  - GEMS friction surface helper functions
      INSTALLED: 0.1.2 (latest)


# Show Wet and Dry season sentinel images for Malawi


```python
import ee
import geogems  
# ee.Authenticate() #uncomment for first run to authorise with google 
ee.Initialize()

area= 'Malawi'
lat = -12.8018637
lon = 33.4752805

#time series 
dry_season = ('2019-05-01' , '2019-10-30') 
wet_season = ('2019-11-01', '2020-04-30')

#load the earth engine helper functions
geography_object = geogems.map.ee_helper()
#load the map 
map_malawai=geography_object.show(lat, lon, 6.5)

```

    Latitude -12.8018637, longtitude 33.4752805, zoom 6.5



```python

#get earth engines objects (bounds and sentinet images)
bounds=geography_object.get_country_polygon_by_name(ee, area) #pass in country name
image_dry,image_wet,trueColor_palette= geography_object.\
                                        get_sentinel_dry_wet_season(dry_season,wet_season ,ee,bounds)

# show map 
map_malawai
# 
 
```

    Malawi  polygon returned as FeatureCollection
     Sentinuel images returned



    Map(bottom=17834.0, center=[-12.8018637, 33.4752805], controls=(WidgetControl(options=['position'], widget=HBo…

![wet season](https://warehouse-camo.ingress.cmh1.psfhosted.org/afe8c02839ece956d3fe507fb45017b8d865841e/68747470733a2f2f6769746875622e636f6d2f74316e616b2f67656f67656d732f626c6f622f6d61696e2f706963732f73656e74696e656c5f7765745f736561736f6e2e706e673f7261773d74727565)

```python
#Add image
map_malawai.addLayer(image_wet, trueColor_palette, '2019 Dry season true color');
map_malawai.addLayerControl()  
```


```python

#load modis landcover
maplc_malawai=geography_object.show(lat, lon, 6.5)

image_lc,legend= geography_object.get_Modis_MCD12Q1_landcover_2013_01_01(ee,bounds)


```

```python
maplc_malawai
```

    Map(center=[-12.8018637, 33.4752805], controls=(WidgetControl(options=['position'], widget=HBox(children=(Togg…


![image](https://warehouse-camo.ingress.cmh1.psfhosted.org/de3ba43fc8eb9586a1c774ebfbbece563cbcc9bd/68747470733a2f2f6769746875622e636f6d2f74316e616b2f67656f67656d732f626c6f622f6d61696e2f706963732f6d6f6469735f6c632e706e673f7261773d74727565)

```python
 
maplc_malawai.addLayer(image_lc, {}, 'MODIS Land Cover')
maplc_malawai.add_legend(legend_title="MODIS Global Land Cover", legend_dict=legend)
 
```
