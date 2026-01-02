# Vol.4：実習環境の準備（GitHub & Colab）

これから実際にコードを書いていくための **実習環境** を整えます。  
Google Colab を使えば、パソコンに何もインストールしなくてもディープラーニングを始められます。

※Google アカウントが必要です。

- 講座のコードをすぐ開くことができます
- 自分で作ったソースコードを保存することができます
- ブラウザを使ってどの端末からでも続きができます  

というメリットがあります。

---

## Google Colabとのリンク（Vol.4）

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol04_env_setup/vol04_notebook.ipynb)

[Open in Colab（新しいタブで開くには右クリック）](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol04_env_setup/vol04_notebook.ipynb)

---

## 📌 1. GitHub リポジトリの構成

講座用の GitHub リポジトリは、次のような構成になっています。

```
deep-learning-from-step-by-step/
├── vol01_overview/
├── vol02_mnist_intro/
├── vol03_dl_basics/
├── vol04_env_setup/
├── vol05_mnist_visualize/
├── vol06_nn_from_scratch_1/
├── vol07_nn_from_scratch_2/
├── vol08_pytorch_mnist/
├── vol09_improve_accuracy/
└── vol10_summary/
```

各フォルダには  
- `README.md`（解説）  
- vol01～vol10の`notebook.ipynb`（Colabで動かせる実習）  
が入っています。

---

## 📌 2. Google Colab を使った講座のノートブックの開き方

Google Colab はブラウザだけで使えるノートブック環境です。

開き方：

1. ブラウザで「Google Colab」と検索  
2. Google アカウントでログイン  
3. **ファイル → ノートブックを開く**  
4. **GitHub** タブを選ぶ  
5. リポジトリ URL を貼るとノートブック一覧が表示される  

---

## 📌 3. ノートブック内の「Open in Colab」ボタン

講座のGitHub の notebook に以下のボタンを設定しています。  
ワンクリックで Google Colab を開くことができます。

※下のボタンをクリックするとサンプルとしてvol4のノートブック(vol04_notebook.ipynb)が開きます。

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TrSaleMane/deep-learning-from-step-by-step/blob/main/vol04_env_setup/vol04_notebook.ipynb)

---

## 📌 4. GPU の確認方法

Colab では無料で GPU が使えます。  
MNIST なら CPU でも十分ですが、GPU があると学習が速くなります。

GPU の有無は次のコードで確認できます：

```python
import torch
torch.cuda.is_available()
```

---

## 📌 5. ノートブックの基本操作

● **セルを実行する**  
　セル左の「▶」ボタンを押すだけ。

● **新しいセルを追加**  
　上部メニューの「+ コード」または「+ テキスト」。

● **ランタイムの再起動**  
　エラーが出たら  セルをもう一度実行するか、ランタイムを再起動してください。 「ランタイム → ランタイムを再起動」 

---

## 📌 6. Googleドライブを Colab にマウントする方法

🔧 マウント手順ノートブックのセルに次のコードを実行します：

```
from google.colab import drive
drive.mount('/content/drive')
```

実行すると、「Googleアカウントへのアクセス許可」→「認証コードの入力」という流れが表示されます。

認証が完了すると、次のようなフォルダが使えるようになります

```
/content/drive/MyDrive/
```

ここに画像やモデルを保存しておくと、Colab から自由に読み書きできます。

---

## 📌 7. Colab に画像ファイルをアップロードする方法（Vol.8 で使用）

Vol.8 では、あなたが紙に書いた手書き数字をスマホで撮影し、その画像を Colab にアップロードして MNIST モデルで推論します。

Colabでは、次のコードを実行することでファイルをアップロードできます。

```
from google.colab import files
uploaded = files.upload()
```

すると、画面に「ファイルを選択」ボタンが表示されます。

手書き数字の画像（例：my_digit.png）を選ぶと、Colab にアップロードできます。

アップロードされたファイルは次のようにアクセスできます：

```
from PIL import Image
import matplotlib.pyplot as plt

img = Image.open('my_digit.png')
plt.imshow(img, cmap='gray')
plt.axis('off')
```

---

## 📌 8. Googleドライブに保存している画像ファイルを読み込む

Googleドライブをマウントしている場合は、あらかじめドライブ内に画像を保存しておけば Colab から直接読み込むことができます。

例えば、みなさんのGoogleドライブに、mnistフォルダがあって、その中に、my_digit.pngという画像ファイルがある場合、Colab から直接読み込むことができます。

```
img_path = '/content/drive/MyDrive/mnist/my_digit.png'
img = Image.open(img_path)
plt.imshow(img, cmap='gray')
plt.axis('off')
```

---

## ▶ 次のステップ

Vol.5 では  
**「MNISTを読み込んでみよう：前処理と可視化」**  
をテーマに、実際にデータを触りながら進めていきます。
