# Digital Twin for Shibuya City Planner
CityPlannerを用いた渋谷デジタルツインデータ整備

---

## 1. 対象エリア
CityPlannerの仕様上平面投影の正方形が必須条件

### 1-1. 渋谷駅北西エリア(53393596)

<img width="600" alt="スクリーンショット 2024-05-29 10 17 15" src="https://github.com/furuhashilab/digitaltwin4shibuyaCP/assets/416977/31b2e43a-aad2-485b-af50-cf29a58d2175">

#### 53393596
 * X幅: 約 1.4 km (1,392m)
 * Y幅: 約 1.0 km (1,142m)
 * UR: 15552724,4254851
 * UL: 15551332,4254851
 * LR: 15552724,4253709
 * LL: 15551332,4253709
 * CentX: 15552028
 * CentY:  4254280

#### 包有正方形エリア
 * X幅: 1.5 km (1,500m/750m)
 * Y幅: 1.5 km (1,500m/750m)
 * UR: 15552778,4255030
 * UL: 15551278,4255030
 * LR: 15552778,4253530
 * LL: 15551278,4253530
 * CentX: 15552028
 * CentY: 4254280

```
{
"type": "FeatureCollection",
"name": "mesh53393596_epsg3857",
"crs": { "type": "name", "properties": { "name": "urn:ogc:def:crs:EPSG::3857" } },
"features": [
{ "type": "Feature", "properties": { "Name": "53393596", "description": null, "timestamp": null, "begin": null, "end": null, "altitudeMode": null, "tessellate": -1, "extrude": 0, "visibility": 1, "drawOrder": null, "icon": null }, "geometry": { "type": "Polygon", "coordinates": [ [ [ 15552778,4253530, 100.0 ], [ 15552778,4255030, 100.0 ], [ 15551278,4255030, 100.0 ], [ 15551278,4253530, 100.0 ], [ 15552778,4253530, 100.0 ] ] ] } }
]
}
```
座標の記述順番: LR → UR → UL → LL → LR


### 1-2. 渋谷駅周辺4x4エリア

* Plan A (標準地域メッシュをベースにしているため、正方形ではない。)
<img width="600" alt="PlanA対象エリア" src="https://github.com/furuhashilab/digitaltwin4shibuyaCP/assets/416977/7a2d8635-925e-48c4-846a-6ae0ca2f2452">

* Plan A (正方形版)
<img width="600" alt="PlanA対象エリア" src="https://github.com/furuhashilab/digitaltwin4shibuyaCP/assets/416977/5acd7aca-a668-4d06-9bdb-11d9dc8d3d91">


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

* 正方形のエリア定義
## 正方形に修正
 - UL: 15548440, 4256600 [m]
 - UR: 15554240, 4256600 [m]
 - LL: 15548440, 4250800 [m]
 - LR: 15554240, 4250800 [m]

 - X横幅: 5,800 [m] +/- 2900
 - Y縦幅: 5,800 [m] +/- 2900
   
 - 中心座標: 15551340, 4253700 [m]

```
{
"type": "FeatureCollection",
"name": "StudyAreaInShibuya_PlanA_3857",
"crs": { "type": "name", "properties": { "name": "urn:ogc:def:crs:EPSG::3857" } },
"features": [
{ "type": "Feature", "properties": { }, "geometry": { "type": "Polygon", "coordinates": [ [ [ 15548440, 4256600. ], [ 15554240, 4256600 ], [ 15554240, 4250800 ], [ 15548440, 4250800 ], [ 15548440, 4256600 ] ] ] } }
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


