Cuyahoga County Age Ma
====================

Map of number of Cleveland residents by census tract. 


# Converting ESRI shapefile to TopoJSON format

Make sure that ogr2 and TopoJSON are installed properly, see "Let's make a map!" (http://bost.ocks.org/mike/map/) for further instructions



 ``` tl_2013_39_tract.shp``` (via http://catalog.data.gov/dataset/tiger-line-shapefile-2013-state-ohio-current-census-tract-state-based)
 ``` cuyahoga-youth2.csv ``` 
  
Take the census tract data for Cuyahoga County, ID 035

``` ogr2ogr -f GeoJSON -where "COUNTYFP = '035'" input35.json tl_2013_39_tract.shp ```

Add attributes to the GeoJSON file, mapping the id property from the shapefile (originally) to the column title in the csv file

```bash 
topojson \
-o outputYouth.json \
-e cuyahoga-youth2.csv \
--id-property=+NAME,+CensusTract \
-p total00=+total00 \
-p total10=+total10 \
--input35.json 
```

Note: delete tract 9900, as it represents the lake itself and does not contain useful information (to the best of my knowledge).
