# Nexthr

### 概要

##### 背景

小売業、飲食業、レンタサイクルなどの道路旅客運送業は、顧客数が多くなる時期に対応できる量の商品を備えつつも稼働していない在庫を出来るだけ少なく保つことによって、損失を最小限に抑えて売上を最大化することが出来る。したがって顧客数がどのように時間変化するかを精度良く予測し、それに合わせてリソース管理することは重要な課題である。

##### 目的

過去の顧客数、時間、曜日、天候などのデータから、利用者数の時間変化を予測する。

##### 概要

ランダムな50日のデータ（ソースは使用言語・環境の欄のURLを参照）をテストデータとして分析を行った。元データのテーブルと元データに時系列情報を取り込んだテーブルを作成し、それぞれのテーブルに対して50回学習と出力を繰り返した。

##### 想定業界

+ 道路旅客運送業
+ 小売業
+ 飲食業

##### 想定企業

HELLO CYCLING様

##### 想定ポジション

売上・利用者数分析担当、マーケティング担当、現場担当者

##### 使用言語・環境

python, jupyter-lab
[https://signate.jp/competitions/114/data](https://signate.jp/competitions/114/data)


### 成果物（出力結果）

##### 効果

学習させる元データに含まれる特徴量は、季節、月、時間、曜日、祝日否かのフラグ、天候ラベル、気温、湿度、風速、体感温度の10個である。

ターゲットとする日付をランダムに選び、その日付以外のデータで学習したモデルでその日付の24時間分の利用者数を予測することを一つの単位とし、それを50回繰り返した。一単位ごとに予測データと学習データのMAEを計算し、50回の試行から得られたデータの平均と標準偏差を計算した。

元データのみのテーブルで学習した場合には予測値と正解系列のMAEの平均が 23.41±1.00 であったのに対し、直前6時間の利用者数を取り入れて学習した場合の1期先予測では、MAEの平均が 18.34±0.62 となった。

これにより、カレンダー、天候情報、過去の利用者数などから1期先を平均的に高い精度で予測することが可能になったと言える。
この予測に基づいて、リアルタイムで近隣の拠点間にある自転車の台数と利用者数予測をアプリなどに表示して近隣の拠点の利用を促したり、拠点間での在庫の融通などにつなげることが出来る。

##### 工夫・苦労点

学習した内容の再現性を高めつつ、自分で考えたことをどのように取り入れるかという点が難しかった。
また、学習データ/検証用データ分割のランダム性を利用して複数回の学習させ、学習精度の高まりについて簡単に評価指標を与えられたことは工夫した点である。

##### 今後の施策

クラスタリングやウェイトを利用したり、可能であればデータに新たな特徴量を加えたりしてモデルの精度を上げ、24期先予測といった実用に供することのできるレベルに向上させ分析が出来たら面白いと考える。
