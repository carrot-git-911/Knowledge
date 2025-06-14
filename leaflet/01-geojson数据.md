> [!abstract] GeoJSON 是一种用于表示地理空间数据的开放标准格式，基于 JSON（JavaScript Object Notation）。它支持点、线、面等几何类型，并且可以包含属性数据。

GeoJSON 基本结构

type 表示GeoJSON 对象的类型，常见的有 `FeatureCollection`、`Feature`、`Point`、`LineString`、`Polygon` 等。

geometry 表示地理空间数据的几何形状

properties: 包含与几何形状相关的属性数据

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [102.0, 0.5]
      },
      "properties": {
        "name": "Example Point"
      }
    }
  ]
}
```

GeoJSON 几何类型

Point 点
```json
{
  "type": Point,
  "coordinates": [100.0, 0.0]
}
```

LineString 线
```json
{
  "type": "LineString",
  "coordinates": [
    [100.0, 0.0],
    [101.0, 1.0]
  ]
}
```

Polygon 多边形

```json
{
  "type": "Polygon",
  "coordinats": [
    [
      [100.0, 0.0],
      [101.0, 0.0],
      [101.0, 1.0],
      [100.0, 1.0],
      [100.0, 0.0]
    ]
  ]
}
```

MultiPoint 多个点
```json
{
  "type": "MultiPoint",
  "coordinates": [
    [100.0, 0.0],
    [101.0, 1.0]
  ]
}
```

MultiLineString 多条线
```json
{
  "type": "MultiLineString",
  "coordinates": [
    [
      [100.0, 0.0],
      [101.0, 1.0]
    ],
    [
      [102.0, 2.0],
      [103.0, 3.0]
    ]
  ]
}
```

**MultiPolygon**: 表示多个多边形。

```json
{
  "type": "MultiPolygon",
  "coordinates": [
    [
      [
        [102.0, 2.0],
        [103.0, 2.0],
        [103.0, 3.0],
        [102.0, 3.0],
        [102.0, 2.0]
      ]
    ],
    [
      [
        [100.0, 0.0],
        [101.0, 0.0],
        [101.0, 1.0],
        [100.0, 1.0],
        [100.0, 0.0]
      ]
    ]
  ]
}
```

使用 GeoJSON
在 leaflet 中使用 GeoJSON
详见 [[02-leaflet知识点]]
在 Python 中使用 GeoJSON

