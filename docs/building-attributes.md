## Introduction

Identify building height from a photo
Building-Height is a system that can determine the attributes of historical buildings in England. 
The building part can be defined just by uploading a photo.

Working with geo datasets and image metadata to visualize 3d buildings showing building attributes, such as heights, volumes.

* building layer polygon extrusion depicts the 3D building
* creates 2 geojson layers (using deck.gl)
* building height attribute from ordnance survey
* polygon of building footprints from ordnance survey
* lidar data from environment agency for 3d terrain
* creates a 3D building on a map canvas (using mapbox-gl) after taking a geojson file as input.

The goal is to create a terrain map of southeast England using point cloud datasets (appendix a) where building polygons will be extruded on a map with real world coordinates.

#### Point Cloud

<video width="640"  controls>
    <source src="/media/media_2024-05-04 06-15-43-building-height-upload-single-image-point-cloud.mp4" type="video/mp4">
</video>


### Upload an image
You can upload or capture from your camera with active GPS

#### Image metadata will be displayed
Extracted metadata from the image you uploaded will be displayed

#### Building height will be identified
The building height, map location of the building and its attributes will be displayed

#### 3D Navigation

* Pan	Mouse Left
* Rotate	Mouse Right
* Shift + Mouse Left
* Top-down Camera	T
* Perspective Camera	P
* Driver Camera	D
* Recenter Camera	R

<img src="/media/media_map-navigation-shortcuts.png" width="353" height="352" /> 

### Showcase
Create a link to a showcase which contains exif data extracted from photos collected in mappics galleries via api.

<video width="640"  controls>
    <source src="/media/media_2024-05-04 06-19-35-building-height-showcase-api.mp4" type="video/mp4">
</video>

* New button Showcase
* Function fetch all exif data via api from images for a particular gallery (first one heritage-trail-Farnham) this will be a stream as shown in streetscape.gl
* Fetch all polygons via api (already works)
* Exclude all buildings (already works for 1no. building)

```
curl -X 'GET' \
  'https://api.buildingshistory.co.uk/api/v1/images/?gallery_id=985e3f6d-09f1-4a0f-8cbf-060514ecb860' \
  -H 'accept: application/json' \
  -H 'X-CSRF-TOKEN:
```
#### Gallery
buildingshistory gallery (current)

### TODO
(out of date)https://api.buildingshistory.co.uk/api/v1/galleries/?slug%3Dheritage-trail-farnhamgallery_id%20985e3f6d-09f1-4a0f-8cbf-060514ecb860

<img src="/media/media_gallery-new-homes.png" width="650" height="339" />

[<u>https://buildingshistory.co.uk/galleries/new-homes/</u>](https://buildingshistory.co.uk/galleries/new-homes/
)
### Creating a terrain map
Go [<u>Enviroment Agency website</u>](https://environment.data.gov.uk/survey), which contains Lidar data for the United Kingdom.

Search for the area in which you would like to create the terrain map, below show a results for Farnham in Surrey

<img src="/media/media_environment-data-gov-uk-survey.png" width="650" height="339" />

Available tiles used in this project

* lidar_composite_dtm-2022-1-SU84nw
* lidar_composite_dtm-2022-1-SU84ne

The surface (basemap) terrain would be covered by ordnance survey tiles, field of view (FOV) would be from street view showing camera and building with real coordinates. 

<img src="/media/media_terrain-map.png" width="650" height="339" />

(figure1)

Buildingshistory.co.uk shows concept but not using real world coordinates, has a terrain and basemap. 

<img src="/media/media_terrain-map-camera-wrong.png" width="650" height="339" />

(figure2).

#### create a rgb Mbtile (PNG) 
for our tileserver of SU84NW to either geoserver to tilesserver-g with Arcgis 

<img src="/media/media_terrain-map-digital-terrain-model.png" width="650" height="339" />
(figure 3) 

### Deck-GL

#### cameraGPSData 
(GPSImgDirection) to position initialViewState  -20m behind, show if a person was taking photo of building
```
    const exif3dCameraLayer = new ScenegraphLayer({
      id: "exif3d-camera-layer",
      data: cameraGPSData,
      scenegraph: url,
      getPosition: (d) => d.coordinates,
      getColor: (d) => [203, 24, 226],
      getOrientation: (d) => [0, -d.bearing, 90],
      opacity: 1,
    });
```
#### hover over 
pink camera shows image hoverover from building-height.co.uk
<img src="/media/media_attributes-hoverover.png" width="650" height="339" />

#### draw lidar
<img src="/media/media_attributes-draw-laz.png" width="650" height="339" />



(figure 1)

#### API/ Database
* geojson for map of 1 building
* building height and toid
```
            "properties": {
                "RelHMax": 13.1,
                "TOID": "osgb1000014525478",
                "_symbol": 4
```
3.	Would like to add post this geojson into su_building table 
<img src="/media/media_database-su-buildings.png" width="650" height="339" />


### Geoserver
#### cache OS tiles 
What to use cached tiles from geoserver
Replace https://api.os.uk/maps/raster/v1/zxy/Outdoor_3857/{z}/{x}/{y}.png?key=wXtior9ubP6EFLYP5l6isfWZYiKqOlf7

Can you configure geoserver to work {z}/{x}/{y}.png, started to set it up on geoserver this morning.
Followed https://blog.ianturton.com/2021/07/22/Cascading-OS-Map-Tiles.html 

### References

#### Terrain
* [<u>https://deck.gl/docs/api-reference/geo-layers/terrain-layer</u>](https://deck.gl/docs/api-reference/geo-layers/terrain-layer)
* [<u>https://github.com/tilezen/joerd/blob/master/docs/formats.md#terrarium</u>](https://github.com/tilezen/joerd/blob/master/docs/formats.md#terrarium) terrarium with extension png in Web Mercator projection, 256x256, 260x260, 512x512, and 516x516 tiles
* [<u>https://environment.maps.arcgis.com/home/user.html?user=ea.geomatics.admin</u>](https://environment.maps.arcgis.com/home/user.html?user=ea.geomatics.admin)

#### Deck-GL

* [<u>OrbitController</u>](https://deck.gl/docs/api-reference/core/orbit-controller)
* [<ul>https://github.com/aurora-opensource/streetscape.gl</u>](https://github.com/aurora-opensource/streetscape.gl)

### Technology Stack
* React-mapgl
* Exif-extractor
* Mapboxgl
* Deckgl
    * PolygonLayer (buildings)
    * IconLayer (camera)
    * GeoJsonLayer
    * ScenegraphLayer
    * OrbitController