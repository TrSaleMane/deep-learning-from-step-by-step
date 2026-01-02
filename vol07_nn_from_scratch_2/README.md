# Vol.7：ニューラルネットを“ゼロから”実装する（後編）

この回では、前編で作った **forward（順伝播）** に続き、  
いよいよ **学習** を実装します。

ディープラーニングの学習は、次の3ステップで進みます。

1. 損失を計算する  
2. 勾配（gradient）を計算する  
3. パラメータを更新する  

この3つを理解すれば、ディープラーニングの **「学習のポイント」** が理解できると思います。

---

## Google Colabとのリンク（Vol.7）

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol07_nn_from_scratch_2/vol07_notebook.ipynb)

[Open in Colab（新しいタブで開くには右クリック）](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol07_nn_from_scratch_2/vol07_notebook.ipynb)

---

## 📌 1. 損失関数の計算（Softmax + Cross Entropy）

MNIST のような分類問題では  
**交差エントロピー損失（Cross Entropy Loss）** を使います。

- **Softmax**：出力（logits）を確率に変換  
- **Cross Entropy**：正解ラベルとのズレを損失として数値化  

これで「どれくらい間違えているか？」を測ることができます。

---

## 📌 2. 勾配の計算（Backpropagation）

ここがディープラーニングの核心です。

本来は複雑な微分計算が必要ですが、  
ここでは「何が起きているか」を理解するために、**手計算で勾配を実装** します。

ポイント：

- Softmax + CrossEntropy の勾配は  
  $$\(\frac{\partial L}{\partial z} = p - y\)$$  
  というシンプルな形になる  
- 隠れ層では ReLU の勾配（負の部分を 0 にする）が効いてくる  

---

## 📌 3. パラメータ更新（確率的勾配降下法：SGD）

勾配が求まったら、重みを  
**損失が小さくなる方向に少しずつ動かす** ことで学習します。

- 学習率（learning rate）`lr` を決める  
- `W ← W - lr * dW` のルールで更新する  

これが **確率的勾配降下法（SGD）** です。

---

## 📌 4. 1エポック学習と loss の推移

MNIST をミニバッチで学習し、  
**1エポック分の学習ループ** を自分で実装します。

- `for x, y in train_loader:` でバッチを取り出す  
- forward → 損失 → 勾配 → 更新  
- `loss` の推移をグラフにして、学習が進んでいるかを確認  

loss が下がっていれば  
**「モデルの精度が上がっている」** ということです。

---

## ▶ 次のステップ

Vol.8 では、  
**「PyTorchでMNISTモデルを作る」** をテーマに、  
いよいよ `nn.Module` を使ってニューラルネットワークを実装していきます。
