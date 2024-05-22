# Digital Twin for Shibuya City Planner
CityPlannerを用いた渋谷デジタルツインデータ整備


## 1. 対象エリア
CityPlannerの仕様上平面投影の正方形が必須条件

* Plan A (標準地域メッシュをベースにしているため、正方形ではない。このエリアに近似した EPSG:3857 での正方形座標はこちら)
<img width="600" alt="PlanA対象エリア" src="https://github.com/furuhashilab/digitaltwin4shibuyaCP/assets/416977/7a2d8635-925e-48c4-846a-6ae0ca2f2452">

### 1-1. 空間参照系
* EPSG:3857 に統一

### 1-2. 地域メッシュ
* UL,UR: 53394504 , 53394507
* LL,LR: 53393574 , 53393577

### 1-3. BBOX
* [GeoJSON 正方形ではない](https://github.com/furuhashilab/digitaltwin4shibuyaCP/blob/main/data/BBOX/StudyAreaInShibuya_PlanA.geojson) 
```
{
  "type": "FeatureCollection",
  "features": [
   
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "coordinates": [
          [
            [
              139.67400258922322,
              35.67576991472468
            ],
            [
              139.67400258922322,
              35.6406857362758
            ],
            [
              139.7261290509494,
              35.6406857362758
            ],
            [
              139.7261290509494,
              35.67576991472468
            ],
            [
              139.67400258922322,
              35.67576991472468
            ]
          ]
        ],
        "type": "Polygon"
      }
    }
  ]
}
```

```
{
"type": "FeatureCollection",
"name": "StudyAreaInShibuya_PlanA_3857",
"crs": { "type": "name", "properties": { "name": "urn:ogc:def:crs:EPSG::3857" } },
"features": [
{ "type": "Feature", "properties": { }, "geometry": { "type": "Polygon", "coordinates": [ [ [ 15548438.845290701836348, 4256099.03733919467777 ], [ 15548438.845290701836348, 4251292.254631052725017 ], [ 15554241.536466917023063, 4251292.254631052725017 ], [ 15554241.536466917023063, 4256099.03733919467777 ], [ 15548438.845290701836348, 4256099.03733919467777 ] ] ] } }
]
}
```

## 2. 整備すべきデータ形式

### 2-1. ラスタデータ
* GeoTIFF(EPSG:3857)

#### 2-1-1. ラスタデータの整備方法
* XYZタイル → QGIS → GeoTIFFエクスポート

### 2-2. ベクタデータ
* GeoJSON(EPSG:3857)
* GeoPackage(EPSG:3857)

#### 2-2-1. ベクタデータの整備方法
* XYZタイル → QGIS → GeoTIFFエクスポート

## 3. 整備データリスト

### 3-1. 主題データ
* 渋谷区オープンデータ
* 

### 3-2. PLATEAU 3Dデータ
* 3D建物

#### 3-2-1. PLATEAUデータの整備方法
* CityGML → [plateau-gis-converter](https://github.com/MIERUNE/plateau-gis-converter) → GeoJSON(EPSG:3857)エクスポート


### 3-3. 標高DEM
* 地理院5m標高

### 3-4. ベースマップ
* OpenStreetMap
* 地理院地図シームレス空中写真


## License
原則オープンデータを用いる


## Appendix
* [plateau-gis-converter](https://github.com/MIERUNE/plateau-gis-converter)
* [QGIS](https://qgis.org/)
* [GeoJSON.io](https://geojson.io/)


