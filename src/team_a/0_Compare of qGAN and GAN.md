### qGANとは
　GAN（Generative Adversarial Network）は真のデータセットの統計を模倣するデータの統計を作成するGeneratorと、真のデータと偽のデータを区別しようとしようとするDiscriminatorの敵対ゲームによって構成される教師なし学習の一つである。
</br>
このGeneratorとDiscriminatorのどちらか一方或いは両方を量子システムに置き換えたものを、qGAN（Quantum Generative Adversarial Networks）と呼ぶ。qGANは、古典部分と量子部分の両方を含むハイブリッド量子古典アルゴリズムである。

### qGANとGANのアルゴリズム面の違い
　qGANの目的は、与えられた古典的なトレーニング データに従って古典的なサンプルを生成することではなく、量子ジェネレーターをトレーニングして、データの基礎となる確率分布を表す量子状態を作成することである。
 </br>
従って、qGANは、GeneratorとDiscriminatorにパラメーター化された2つの量子回路を使用する。量子回路を実行すると、本物の場合は「1」、偽物の場合は「-1」を意味する単一の二値決定変数が出力される。

<img width="404" alt="image" src="https://github.com/wg-quantum/2023-b-07-a/assets/50878026/f1ab9ecd-632a-4165-bc7b-2242bcd5e85a">

（[Pavan  2018](https://pavanjayasinha.medium.com/quantum-generative-adversarial-networks-76243d1c6888)）

### 量子コンピューターの課題
* 実用的な量子の利点を達成したい場合、実世界のデータを量子回路にエンコードする効率的な方法を設計することが重要なのに対し、従来のデータ エンコーディングが非常に非効率であれば、アルゴリズム全体が役に立たなくなる可能性がある
* 量子コンピューターは、亜原子レベルで見られるような相関状態を計算するのが最も得意だが、現実世界の問題は通常、量子コンピューターが優勢な相関状態に一致することはない

### 量子コンピューターの課題に対するqGANのメリット
　現実世界のデータを量子回路にエンコードすることは困難だが、qGANは、非常に高次元のデータセットで作成されたデータを生成する際に、指数関数的に高速化する可能性がある。従って、qGANには、古典的に扱いにくい (古典的にサンプリングすることが指数関数的に困難である) 確率分布のサンプリングと操作を飛躍的に高速化する可能性がある

### qGANの実装
##### 1_pennylane_mnist.ipynb
* pennylaneが開発したQuantum GANsでtutorialのMNISTを実行したもの
    * [ref](https://pennylane.ai/qml/demos/tutorial_quantum_gans)
##### 2_ibm_quiskit_mnist.ipynb
* IBMが開発したQnantum GANsでMNISTを実行したもの
    * pennylaneのdatasetを用いて独自で実装を行った
##### 3_ibm_quisikt_tutorial.ipynb
* IBMが開発したQnantum GANsでtutorialの一次元分布作成を実行したもの
    * [ref](https://qiita.com/ucc_white/items/1fccf6bff9f1f3dc16fa)