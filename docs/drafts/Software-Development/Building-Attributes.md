---
title: TypeScript Deck.GL
description: Web Console it’s possible to connect and check the data uploaded from the smartphone (Android and iOS).
---

## Introduction TODO
See also [[TypeScript-PHP]] page which discusses the development of the backend in PHP and frontend in TypeScript, to be able use the techologies listed here.

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

## TerrainLayer (deck.gl)

https://deck.gl/docs/api-reference/geo-layers/terrain-layer

import {TerrainLayerDemo} from '@site/src/doc-demos/geo-layers';

<TerrainLayerDemo />

The `TerrainLayer` reconstructs mesh surfaces from height map images, e.g. [Mapzen Terrain Tiles](https://github.com/tilezen/joerd/blob/master/docs/formats.md), which encodes elevation into R,G,B values.

When `elevationData` is supplied with a URL template, i.e. a string containing `'{x}'` and `'{y}'`, it loads terrain tiles on demand using a `TileLayer` and renders a mesh for each tile. If `elevationData` is an absolute URL, a single mesh is used, and the `bounds` prop is required to position it into the world space.


import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs groupId="language">
  <TabItem value="js" label="JavaScript">

```js
import {Deck} from '@deck.gl/core';
import {TerrainLayer} from '@deck.gl/geo-layers';

const layer = new TerrainLayer({
  elevationDecoder: {
    rScaler: 2,
    gScaler: 0,
    bScaler: 0,
    offset: 0
  },
  // Digital elevation model from https://www.usgs.gov/
  elevationData: 'https://raw.githubusercontent.com/visgl/deck.gl-data/master/website/terrain.png',
  texture: 'https://raw.githubusercontent.com/visgl/deck.gl-data/master/website/terrain-mask.png',
  bounds: [-122.5233, 37.6493, -122.3566, 37.8159],
});

new Deck({
  initialViewState: {
    longitude: -122.4,
    latitude: 37.74,
    zoom: 11
  },
  controller: true,
  layers: [layer]
});
```

  </TabItem>
  <TabItem value="ts" label="TypeScript">

```ts
import {Deck} from '@deck.gl/core';
import {TerrainLayer} from '@deck.gl/geo-layers';

const layer = new TerrainLayer({
  elevationDecoder: {
    rScaler: 2,
    gScaler: 0,
    bScaler: 0,
    offset: 0
  },
  // Digital elevation model from https://www.usgs.gov/
  elevationData: 'https://raw.githubusercontent.com/visgl/deck.gl-data/master/website/terrain.png',
  texture: 'https://raw.githubusercontent.com/visgl/deck.gl-data/master/website/terrain-mask.png',
  bounds: [-122.5233, 37.6493, -122.3566, 37.8159],
});

new Deck({
  initialViewState: {
    longitude: -122.4,
    latitude: 37.74,
    zoom: 11
  },
  controller: true,
  layers: [layer]
});
```

  </TabItem>
  <TabItem value="react" label="React">

```tsx
import React from 'react';
import DeckGL from '@deck.gl/react';
import {TerrainLayer} from '@deck.gl/geo-layers';

function App() {
  const layer = new TerrainLayer({
    elevationDecoder: {
      rScaler: 2,
      gScaler: 0,
      bScaler: 0,
      offset: 0
    },
    // Digital elevation model from https://www.usgs.gov/
    elevationData: 'https://raw.githubusercontent.com/visgl/deck.gl-data/master/website/terrain.png',
    texture: 'https://raw.githubusercontent.com/visgl/deck.gl-data/master/website/terrain-mask.png',
    bounds: [-122.5233, 37.6493, -122.3566, 37.8159],
  });

  return <DeckGL
    initialViewState={{
      longitude: -122.4,
      latitude: 37.74,
      zoom: 11
    }}
    controller
    layers={[layer]}
  />;
}
```

  </TabItem>
</Tabs>


##### Installation

To install the dependencies from NPM:

```bash
npm install deck.gl
# or
npm install @deck.gl/core @deck.gl/mesh-layers @deck.gl/geo-layers
```

```ts
import {TerrainLayer} from '@deck.gl/geo-layers';
import type {TerrainLayerProps} from '@deck.gl/geo-layers';

new TerrainLayer(...props: TerrainLayerProps[]);
```

To use pre-bundled scripts:

```html
<script src="https://unpkg.com/deck.gl@^9.0.0/dist.min.js"></script>
<!-- or -->
<script src="https://unpkg.com/@deck.gl/core@^9.0.0/dist.min.js"></script>
<script src="https://unpkg.com/@deck.gl/mesh-layers@^9.0.0/dist.min.js"></script>
<script src="https://unpkg.com/@deck.gl/geo-layers@^9.0.0/dist.min.js"></script>
```

```js
new deck.TerrainLayer({});
```

#### Properties

When in Tiled Mode, inherits from all [TileLayer](./tile-layer.md) properties. Forwards `wireframe` property to [SimpleMeshLayer](../mesh-layers/simple-mesh-layer.md).



#### Data Options

 `elevationData` (string | string[], required) {#elevationdata}

Image URL that encodes height data.

- If the value is a valid URL, this layer will render a single mesh.
- If the value is a string, and contains substrings `{x}` and `{y}`, it is considered a URL template. This layer will render a `TileLayer` of meshes. `{x}` `{y}` and `{z}` will be replaced with a tile's actual index when it is requested.
- If the value is an array: multiple URL templates. See `TileLayer`'s `data` prop documentation for use cases.


`texture` (string | null, optional) {#texture}

Image URL to use as the surface texture. Same schema as `elevationData`.

- Default: `null`


`meshMaxError` (number, optional) {#meshmaxerror}

Martini error tolerance in meters, smaller number results in more detailed mesh..

- Default: `4.0`

 `elevationDecoder` (object, optional) {#elevationdecoder}

Parameters used to convert a pixel to elevation in meters.
An object containing the following fields:

- `rScaler`: Multiplier of the red channel.
- `gScaler`: Multiplier of the green channel.
- `bScaler`: Multiplier of the blue channel.
- `offset`: Translation of the sum.

Each color channel (r, g, and b) is a number between `[0, 255]`.

For example, the Mapbox terrain service's elevation is [encoded as follows](https://docs.mapbox.com/help/troubleshooting/access-elevation-data/#decode-data):

```
height = -10000 + ((R * 256 * 256 + G * 256 + B) * 0.1)
```

The corresponding `elevationDecoder` is:

```ts
{
  "rScaler": 6553.6,
  "gScaler": 25.6,
  "bScaler": 0.1,
  "offset": -10000
}
```

The default value of `elevationDecoder` decodes a grayscale image:

```ts
{
  "rScaler": 1,
  "gScaler": 0,
  "bScaler": 0,
  "offset": 0
}
```


 `bounds` (number[4], optional) {#bounds}

Bounds of the image to fit x,y coordinates into. In `[left, bottom, right, top]`.
`left` and `right` refers to the world longitude/x at the corresponding side of the image.
`top` and `bottom` refers to the world latitude/y at the corresponding side of the image.

Must be supplied when using non-tiled elevation data.

- Default: `null`


#### `loadOptions` (object, optional) {#loadoptions}

On top of the [default options](../core/layer.md#loadoptions), also accepts options for the following loaders:

- [TerrainLoader](https://loaders.gl/modules/terrain/docs/api-reference/terrain-loader)
- [ImageLoader](https://loaders.gl/modules/images/docs/api-reference/image-loader) if the `texture` prop is supplied

Note that by default, the `TerrainLoader` parses data using web workers, with code loaded from a [CDN](https://unpkg.com). To change this behavior, see [loaders and workers](../../developer-guide/loading-data.md#loaders-and-web-workers).


#### Render Options

#### `color` (Color, optional) {#color}

Color to use if `texture` is unavailable. Forwarded to `SimpleMeshLayer`'s `getColor` prop.

- Default: `[255, 255, 255]`

#### `wireframe` (boolean, optional) {#wireframe}

Forwarded to `SimpleMeshLayer`'s `wireframe` prop.

- Default: `false`

#### `material` (Material, optional) {#material}

Forwarded to `SimpleMeshLayer`'s `material` prop.

- Default: `true`


#### Sub Layers

The `TerrainLayer` renders the following sublayers:

* `tiles` - a [TileLayer](./tile-layer.md). Only rendered if `elevationData` is a URL template.
* `mesh` - a [SimpleMeshLayer](../mesh-layers/simple-mesh-layer.md) rendering the terrain mesh.



Source

[modules/geo-layers/src/terrain-layer](https://github.com/visgl/deck.gl/tree/master/modules/geo-layers/src/terrain-layer)

## TerrainLoader (deck.gl)

The `TerrainLoader` reconstructs mesh surfaces from height map images, e.g. [Mapzen Terrain Tiles](https://github.com/tilezen/joerd/blob/master/docs/formats.md), which encodes elevation into R,G,B values.

| Loader                | Characteristic                                |
| --------------------- | --------------------------------------------- |
| File Extension        | `.png`, `.pngraw`                             |
| File Type             | Binary                                        |
| File Format           | Encoded height map                            |
| Data Format           | [Mesh](/docs/specifications/category-mesh) |
| Supported APIs        | `load`, `parse`                               |
| Decoder Type          | Asynchronous                                  |
| Worker Thread Support | Yes                                           |
| Streaming Support     | No                                            |

#### Usage

```typescript
import {ImageLoader} from '@loaders.gl/images';
import {TerrainLoader} from '@loaders.gl/terrain';
import {load, registerLoaders} from '@loaders.gl/core';

registerLoaders(ImageLoader);

const data = await load(url, TerrainLoader, options);
```

#### Options

| Option                     | Type            | Default   | Description                                                                                                                                   |
| -------------------------- | --------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `terrain.meshMaxError`     | `number`        | `10`      | Mesh error in meters. The output mesh is in higher resolution (more vertices) if the error is smaller.                                        |
| `terrain.bounds`           | `array<number>` | `null`    | Bounds of the image to fit x,y coordinates into. In `[minX, minY, maxX, maxY]`. If not supplied, x and y are in pixels relative to the image. |
| `terrain.elevationDecoder` | `object`        | See below | See below                                                                                                                                     |
| `terrain.tesselator`       | `string`        | `auto`    | See below                                                                                                                                     |
| `terrain.skirtHeight`      | `number`        | `null`    | If set, create the skirt for the tile with particular height in meters                                                                        |

#### elevationDecoder

Parameters used to convert a pixel to elevation in meters.
An object containing the following fields:

- `rScale`: Multiplier of the red channel.
- `gScale`: Multiplier of the green channel.
- `bScale`: Multiplier of the blue channel.
- `offset`: Translation of the sum.

Each color channel (r, g, and b) is a number between `[0, 255]`.

For example, the Mapbox terrain service's elevation is [encoded as follows](https://docs.mapbox.com/help/troubleshooting/access-elevation-data/#decode-data):

```
height = -10000 + ((R * 256 * 256 + G * 256 + B) * 0.1)
```

The corresponding `elevationDecoder` is:

```
{
  "rScale": 6553.6,
  "gScale": 25.6,
  "bScale": 0.1,
  "offset": -10000
}
```

The default value of `elevationDecoder` decodes a grayscale image:

```
{
  "rScale": 1,
  "gScale": 0,
  "gScale": 0,
  "offset": 0
}
```

#### tesselator

The choices for tesselator are as follows:

`auto`:

- Chooses [Martini](https://github.com/mapbox/martini) if possible (if the image is a square where both height and width are powers of 2), otherwise uses [Delatin](https://github.com/mapbox/delatin) instead, which has no input image limitations.

`martini`:

- Uses the [Martini](https://github.com/mapbox/martini) algorithm for constructing a mesh.
- Only works on square 2^n+1 x 2^n+1 grids.
- Generates a hierarchy of meshes (pick arbitrary detail after a single run)
- Optimized for meshing speed rather than quality.

`delatin`:

- Uses the [Delatin](https://github.com/mapbox/delatin) algorithm for constructing a mesh.
- Works on arbitrary raster grids.
- Generates a single mesh for a particular detail.
- Optimized for quality (as little triangles as possible for a given error).

## Types of Mapzen Terrain Tiles

Mapzen Terrain Tiles provide worldwide basemap coverage sourced from [SRTM](www.openstreetmap.org) and other open data projects with several different data formats and varying levels of processing.

The following formats are available, with full details below:

* `terrarium` with extension `png` in Web Mercator projection, 256x256, 260x260, 512x512, and 516x516 tiles
* `normal` with extension `png` in Web Mercator projection, 256x256, 260x260, 512x512, and 516x516 tiles
* `geotiff` with extension `tif` in Web Mercator projection, 512x512 tiles
* `skadi` with extension `hgt` in unprojected latlng, 1°x1° tiles

Need help displaying raster tiles in a map? We have several [examples](build-a-map.md) using Mapzen raster tiles to style in your favorite graphics library including Tangram.

### Terrarium

**Terrarium** format _PNG_ tiles contain raw elevation data in meters, in Web Mercator projection (EPSG:3857). All values are positive with a 32,768 offset, split into the red, green, and blue channels, with 16 bits of integer and 8 bits of fraction.

In other words, the red channel encodes the "256s" place, the green channel the "1s" place, and the blue channel the fractional component, which is 0 - 0.99609375 (255/256) in increments of 0.00390625 (1 / 256).

To decode:

  `(red * 256 + green + blue / 256) - 32768`

To encode, asuming a starting value of `v`:

```
v += 32768
r = floor(v/256)
g = floor(v % 256)
b = floor((v - floor(v)) * 256)
```

For example, with a starting value of 2523.266:

```
v += 32768
> 35291.266
r = floor(v/256)
> 137
g = floor(v % 256)
> 219
b = floor((v - floor(v)) * 256)
> 68

> rgb(137, 219, 68)
```

Decoded, this gives us:

```
(r * 256 + g + b / 256) - 32768
> 2523.265625
```

The range of the elevation data (-11000 - 8900 meters) spans `rgb(85, 8, 0)` - `rgb(162, 198, 0)`, or `[0.33203125, 0.03125, 0] - [0.6328125, 0.7734375, 0]`.

## Normal

**Normal** format _PNG_ tiles are processed elevation data with the the red, green, and blue values corresponding to the direction the pixel “surface” is facing (its XYZ vector), in Web Mercator projection (EPSG:3857). The alpha channel contains **quantized elevation data** with values suitable for common hypsometric tint ranges.

* `red` = x vector
* `green` = y vector
* `blue` = z vector
* `alpha` = quantized elevation data

High alpha channel values indicate lower elevation values (below sea level), making them more opaque. Specifically, **normal** format alpha values are counted in (floored) elevation increments. Below sea level they start at -11,000 meters (Mariana Trench) and range to -1,000 meters in 1,000 meter increments, with more detail on the coastal shelf at -100, -50, -20, -10 and -1 meters and finally 0 (intertidal zone). Values above sea level are reported in 20 meter increments to 3,000 meters, then 50 meter increments until 6,000 meters, and then 100 meter increments until 8,900 meters (Mount Everest).

Encoding quantized height ranges ([src](https://github.com/tilezen/joerd/blob/master/joerd/output/normal.py#L26-L41)):

```
for i in range(0, 11):
    table.append(-11000 + i * 1000)
table.append(-100)
table.append( -50)
table.append( -20)
table.append( -10)
table.append(  -1)
for i in range(0, 150):
    table.append(20 * i)
for i in range(0, 60):
    table.append(3000 + 50 * i)
for i in range(0, 29):
    table.append(6000 + 100 * i)
```

To decode quantized height value:

  `255 - bisect.bisect_left(HEIGHT_TABLE, h)`

### References

#### Terrain
* https://houseprices.io/lab/lidar/map – Easily the best way to  view Lidar.  Only works on Chrome tho.  Based on the 1m DSM data.  Actually better than anything I got from this!
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

[[Web-Console]]