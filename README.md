# cesium-hash
Add URL hashes to web pages with Cesium globes and maps,
inspired by [leaflet-hash](https://github.com/mlevans/leaflet-hash).

# Demo

<https://frogcat.github.io/cesium-hash/>

# Usage

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
  <title>cesium-hash</title>
  <link rel="stylesheet" href="https://unpkg.com/cesium@1.32.1/Build/Cesium/Widgets/widgets.css" />
  <script src="https://unpkg.com/cesium@1.32.1/Build/Cesium/Cesium.js"></script>
  <script src="cesium-hash.js"></script>
</head>

<body>
  <div id="container" style="position:absolute;top:0;left:0;bottom:0;right:0;user-select:none;"></div>
  <script>
    var viewer = new Cesium.Viewer("container", {
      timeline: false,
      animation: false,
      homeButton: false,
      geocoder: false,
      sceneModePicker: false,
      baseLayerPicker: false,
      terrainExaggeration: 10.0,
      terrainProvider: new Cesium.CesiumTerrainProvider({
        url: "https://assets.agi.com/stk-terrain/world",
        requestWaterMask: true,
        requestVertexNormals: true
      }),
      imageryProvider: new Cesium.UrlTemplateImageryProvider({
        url: "https://cyberjapandata.gsi.go.jp/xyz/slopemap/{z}/{x}/{y}.png",
        credit: "地理院タイル"
      })
    });

    if (Cesium.Hash.decode(location.hash) === null)
      location.hash = "#28.603885/145.530003/1119707/327/-45";
    Cesium.Hash(viewer);
  </script>
</body>

</html>
```

location.hash has following format.
```
#{latitude}/{longitude}/{height}/{heading}/{pitch}
```



label   | value
-------- | -----------------
latitude  | latitude in degree
longitude | longitude in degree
height | height in meter
heading | heading in degree<br/> north=0/360, east=90, south=180, west=270
pitch | pitch in degree<br/> vertical=-90, horizontal=0
