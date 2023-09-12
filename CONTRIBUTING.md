## ローカルでの作業

### 必要なライブラリのインストール

以下コマンドを実行して必要なライブラリをインストールする。

```
pip install -r requirement.txt
```


## 動作確認

本リポジトリに Pull Request を送る前に正しく Web ページが表示されるか確認する。

```
jupyter-book build ./src/
```

コマンド実行後、`src/_build`にビルド済みファイルが生成されるためブラウザ等で自身が編集したページが正しく反映されているかを確認する。

ブラウザでの確認方法は、上記の`jupyter-book build`コマンドを実行後、以下のようなメッセージが表示されるので表示されるパスを参考に確認する。

```
===============================================================================

Finished generating HTML for book.
Your book's HTML pages are here:
    src/_build/html/
You can look at your book by opening this file in a browser:
    src/_build/html/index.html
Or paste this line directly into your browser bar:
    <!-- ローカルファイルのパス -->

===============================================================================
```
