# Vol.5：MNISTを読み込んで可視化してみる

この回では、MNIST データを実際に読み込み、画像を表示してみます。  
**「データを確認する」ことは、機械学習を理解するうえでとても重要です。**

MNIST がどんな画像なのか、どんな形状をしているのかを確認しながら進めていきましょう。

---

## Google Colabとのリンク（Vol.5）

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol05_mnist_visualize/vol05_notebook.ipynb)

[Open in Colab（新しいタブで開くには右クリック）](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol05_mnist_visualize/vol05_notebook.ipynb)

---

## 📌 1. データのロード

PyTorch では `torchvision.datasets` を使うことで MNIST を簡単に読み込めます。

ポイント：

- `download=True` → 初回だけ自動でダウンロード  
- `train=True/False` → 学習用とテスト用を分けて取得  
- `ToTensor()` → 画像を PyTorch のテンソルに変換  

---

## 📌 2. 画像の可視化

まずは 1 枚取り出して表示してみましょう。

ここで確認できること：

- MNIST は **28×28 の白黒画像**  
- 手書きなので、太さや傾きがバラバラ  
- 「こういう画像を学習するのか」と直感的に理解できる  

---

## 📌 3. 正規化（Normalize）

ディープラーニングでは、学習を安定させるために **正規化** を行うことが多いです。

MNIST の平均と標準偏差：

- 平均：**0.1307**
- 標準偏差：**0.3081**

---

## 📌 4. flatten（1次元化）

MNIST の画像は 28×28 の 2 次元ですが、  
**全結合ネットワーク（MLP）に入力するには 1 次元に変換する必要があります。**

例：  
28×28 = 784 → **784 次元のベクトル**

---

## 📌 5. shape（データの形）を理解する

機械学習では **shape（データの形）を理解することが重要** です。

- 1 枚の画像：`torch.Size([1, 28, 28])`  
- flatten：`torch.Size([784])`  
- DataLoader（バッチ 64）：`torch.Size([64, 1, 28, 28])`

shape （データの形状）を理解することが、次のステップにつながります。

---

## ▶ 次のステップ

Vol.6 では  
**「ニューラルネットを“ゼロから”実装する（前編）」**  
をテーマに、実際にモデルを定義していきます。
