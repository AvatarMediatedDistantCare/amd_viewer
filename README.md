# directoryの構成
```
amd_kinect_quaternion
├── css
├── img
│   └── img
├── js
│   ├── converter
│   ├── filter
│   ├── formatter
├── lib
└── model
```

### 1. js/ *.js

```
- 概要：ブラウザで描画が必要なコード(動作確認, 定量評価)
```

 - input_predict_correct.js ... kinect, mocap, predictを描画比較するために使用
 - quantitative_evaluation.js ... 定量評価を計算するために使用
 - quantitative_evaluation_methods.js ... quantitative_evaluation_methods.jsの計算メソッドの中身

### 2. js/filter

```
- 概要：以下のためのコード
 - (1) ノイズ付加
 - (2) mocap座標系　→ kinect座標系への変換
 - (3) 移動平均/OneEuroフィルタの適用

```

 - (1) applyNormRand.js ... ノイズ付加に使用
 - (2) mocap_to_kinectCoordinate.js ... mocapからkinectへ変換する際に使用
 - (3) movingAverage_oneEuro.js ... 推定エラー補正後のモーションの移動平均フィルタとoneEuroフィルタを適用するために使用
 
### 3. js/formatter

```
- 概要：生データを整形するためのコード
```

 - kinect_format.js ... kinectの生データを学習データ形式に変換するために使用
 - mocap_local_format.js ... mocapの生データを学習データ形式に変換するために使用


# 使い方

### 1. データの準備

copy visualization/ from amd_keras repository


### 2. データの前処理

normalize and filter predicted motion

```
node js/filter/movingAverage_oneEuro.js data/predict/ki_crossing_arms_back_splitted_predict.csv 20
```
this creates three files _apply_normalize.csv, _apply_one_euro_filter.csv, and \_apply\_moving\_average\_(window size).csv

### 3. 描画
- change filenames to visualize in input_predicted_correct.js
- start server and access to index.html