# Digital Twin for Shibuya City Planner
CityPlannerを用いた渋谷デジタルツインデータ整備


## 1. 対象エリア
CityPlannerの仕様上平面投影の正方形が必須条件

* Plan A
<img width="848" alt="スクリーンショット 2024-05-22 8 38 21" src="https://github.com/furuhashilab/digitaltwin4shibuyaCP/assets/416977/ccccdbc3-3dd0-4760-90d2-204a46613d4a">

```
{
      "type": "Feature",
      "properties": {
        "name": "Shibuya"
      },
      "geometry": {
        "coordinates": [
          [
            [
              139.68098993411616,
              35.67097571228027
            ],
            [
              139.68098993411616,
              35.64126300363202
            ],
            [
              139.72528202455675,
              35.64126300363202
            ],
            [
              139.72528202455675,
              35.67097571228027
            ],
            [
              139.68098993411616,
              35.67097571228027
            ]
          ]
        ],
        "type": "Polygon"
      },
      "id": 25200
    }
```


### 1-1. 空間参照系
* EPSG:3857 に統一

### 1-2. 地域メッシュ


### 1-3. BBOX


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


