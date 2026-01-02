# Vol.9：精度を上げるための工夫

この回では、MNIST の精度をさらに高めるためのテクニックを紹介します。  
ディープラーニングでは、モデルを作ったあとに **どう改善するか** がとても重要です。

ここでは、すぐに試せる 5 つの改善ポイントを解説します。

---

## Google Colabとのリンク（Vol.9）

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol09_improve_accuracy/vol09_notebook.ipynb)

[Open in Colab（新しいタブで開くには右クリック）](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol09_improve_accuracy/vol09_notebook.ipynb)

---

## 📌 1. 学習率（Learning Rate）の調整

学習率は「どれくらい重みを更新するか」を決める重要なパラメータです。

- 大きすぎる → 発散して学習が進まない
- 小さすぎる → 学習が遅い、局所解に到達するときがある

MNIST では以下がよく使われます：

```python
optimizer = torch.optim.SGD(model.parameters(), lr=0.1)
```

もし loss が不安定なら：

- 学習率`lr=0.01` に下げてみる
- Adamなどに変えてみる

```python
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)
```

学習率を変えるだけで、精度が **5〜10% 上がる** こともあります。

---

## 📌 2. 層を増やす（モデルを深くする）

層を増やすとより複雑な特徴を学習できます。

例：隠れ層を 2 つにする

```python
class DeepNN(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = nn.Linear(784, 256)
        self.fc2 = nn.Linear(256, 128)
        self.fc3 = nn.Linear(128, 10)

    def forward(self, x):
        x = x.view(-1, 784)
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x
```

層を増やすと精度は上がりますが、  
**過学習しやすくなる** ため、次のテクニックが必要になります。

---

## 📌 3. ドロップアウト（Dropout）

Dropout は、学習中に一部のニューロンをランダムに無効化する手法です。

- 過学習を防ぐ  
- モデルの汎化性能が上がる  
- MNIST でも効果が大きい  

```python
self.dropout = nn.Dropout(0.5)

x = F.relu(self.fc1(x))
x = self.dropout(x)
```

Dropout(0.5) は「そのバッチにおいて出力を 50% の確率で 0 にし、残った出力を 2倍にして流す」仕組みです。

---

## 📌 4. バッチサイズの調整

バッチサイズは「一度に何枚の画像で学習するか」です。

- 小さい → ノイズが多く汎化性能が上がりやすい  
- 大きい → 安定して学習、収束が速い  

```python
train_loader = DataLoader(train_dataset, batch_size=64, shuffle=True)
```

バッチサイズは **正解がない** ので、いろいろ試すのがポイントです。

---

## 📌 5. 過学習とその対策

過学習とは：

学習データに、過剰に適合している状態で、未知の新しいデータで思うような結果が得られない状態です。

対策：

- Dropout を入れる  
- バッチサイズを小さくする  
- 学習率を下げる  
- エポック数を減らす  
- Weight Decay（正則化）を使う  

```python
optimizer = torch.optim.Adam(model.parameters(), lr=0.001, weight_decay=1e-4)
```

Weight Decay は「重みを小さく保つ」ことで過学習を防ぎます。

---

## ▶ 次のステップ

次の記事では、「まとめと次のステップ」 です。

次シリーズの内容も紹介する予定です。
