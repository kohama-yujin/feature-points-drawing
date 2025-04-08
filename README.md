# 特徴点描画ツール

このツールは、指定した画像に特徴点を描画するためのツールです。
特徴点は、色・形状・大きさ(半径)のカスタマイズが可能です。

## 環境
- Ubuntu 22.04.5 LTS
- Python 3.10.12
- OpenCV 4.10.0.84
- NumPy 1.26.4

## 概要
- 特徴点は、円、正方形、ひし形のいずれかで描画できます。
- 描画する特徴点の色、形状、大きさ(半径)はファイルからの読み込みや、実行時のオプションで指定するなど、柔軟に設定可能です。
- 色は名前（例：`red`）や16進数カラーコード（例：`#FF5733`）で指定できます。
- 画像の中心を原点として座標を補正するオプションもあります。

## インストール

このツールを使用するには、Pythonの環境が必要です。

### 必要なライブラリのインストール

1. このリポジトリをクローンします。
    ```bash
    git clone https://github.com/username/feature-point-drawing-tool.git
    ```

2. 必要なライブラリをインストールします。
    ```bash
    cd feature-point-drawing-tool
    pip install -r requirements.txt
    ```

## 使用方法

### 1. 特徴点データの準備
特徴点データは`.dat`ファイルとして準備します。各行には、特徴点の座標や色、形状、半径を記載します。
- 先頭２列に座標（x, y）を記載
- その後ろに色、形状、半径を記載（順不同、省略可）
> ※細かい設定方法は「色の指定方法」「形状の指定方法」の項目を参照してください。
- 何も指定しない場合、デフォルトで`red circle 3px`が指定されます


#### 特徴点データの例
例 `points.dat`
```bash
100 100  
150 100 3px red circle  
100 150 #2bbaaf
150 150 green
200 200 5px
250 200 5px diamond
200 250 square black 5px
250 250 black square 5px
```

### 2. 画像の準備
特徴点を描画する対象となる画像を準備します。

このツールは、OpenCVの`cv2.imread`を使用して画像を読み込むため、さまざまな画像形式に対応しています。**詳細な対応形式についてはここでは記載しません**。対応形式に関しては、[OpenCV公式ドキュメント](https://docs.opencv.org)を参照してください。


### 3. 実行
実行時、以下のようなオプションを指定することができます(順不同)。  

#### オプション一覧
| オプション | 説明 |
| :--- | :--- |
| -i    | 入力画像のパス(必須) |
| -p    | 特徴点データのパス(必須) |
| -o    | 出力画像のパス |
| -c    | 色の指定 |
| -s    | 形状の指定 |
| -r    | 半径の指定 |
| --shift | 画像の中心を原点とする場合 |

#### 実行例
以下のように実行して、特徴点を画像に描画します。
```bash
python3 main.py -i ./image/sample.png -p ./points_data/sample.dat
```
半径5pxの青い円を描画したい場合
```bash
python3 main.py -i ./image/sample.png -p ./points_data/sample.dat -r 5px -c blue -s circle
```
特徴点データの座標が画像の中心を原点としている場合
```bash
python3 main.py -i ./image/sample.png -p ./points_data/sample.dat --shift
```
