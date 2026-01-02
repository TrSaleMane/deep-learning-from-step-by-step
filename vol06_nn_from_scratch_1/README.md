# Vol.6：ニューラルネットを“ゼロから”実装する（前編）

この回では、ニューラルネットワーク（NN）を **ゼロから実装** していきます。  
PyTorch の `nn.Linear` や `nn.ReLU` を使わず、まずは **仕組みを理解するために自分で書く** ところから始めます。

ここでは **順伝播（forward）、推論（predict）** を中心に理解します。

---

## Google Colabとのリンク（Vol.6）

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol06_nn_from_scratch_1/vol06_notebook.ipynb)

[Open in Colab（新しいタブで開くには右クリック）](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol06_nn_from_scratch_1/vol06_notebook.ipynb)

---

## 📌 1. 重みとバイアスの初期化

ニューラルネットの基本は  
**入力 × 重み + バイアス** の計算です。

MNIST の入力は 28×28 = **784 次元**。  
今回はシンプルに：

- 隠れ層：128  
- 出力：10（数字 0〜9）

という構成にします。

ポイント：

- `randn` は平均0・標準偏差1の乱数  
- 小さな値にするために `* 0.01`  
- バイアスはゼロ初期化でOK  

---

## 📌 2. 行列計算による順伝播

1層目の計算は：

$h = xW_1 + b_1$

PyTorch では `x @ W1` で行列積ができます。

`x` は flatten 済みの `[batch, 784]` のテンソルです。

---

## 📌 3. 活性化関数（ReLU）

隠れ層には **ReLU** を使います。

ReLU の役割：

- 負の値を 0 にする  
- 勾配が消えにくい  
- 計算が速い  
- 現代のNNではほぼ標準  

---

## 📌 4. 出力の計算

隠れ層を通したら、次は出力層へ。

ここで返すのは **logits（生のスコア）**。  
Softmax は後編（Vol.7）で扱います。

---

## 📌 5. forward 関数、predict 関数の実装

「手書きニューラルネットワーク」を作成します。

- 重みとバイアス  
- 行列計算  
- ReLU  
- 入力層、出力層  

PyTorch の `nn.Module` を使うとこの処理は自動化されますが、  
内部で何が起きているかを理解するために、この「手書きニューラルネットワーク」はとても重要です。

---

## ▶ 次のステップ

Vol.7 では、  
**損失関数・勾配計算・パラメータ更新・1エポック学習**  
を実装していきます。

いよいよ「学習」を実装します。
