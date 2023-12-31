# Quantum Federated Learningとは

## 1. はじめに
量子連合学習 (QFL) は、量子コンピューティング (QC) と連合学習 (FL) の原理を融合し、学習プロセスにおけるプライバシー、セキュリティー、効率性を高めるために量子テクノロジーを活用することを目的とする、新しい学際的な分野です。  
</br>
このレビューでは、QFL の研究領域を初めて総合的に検討した Ren et al (2023)の論文をベースに、 QFL の原理、手法、新たな適用について包括的に理解することを目的としています。 この急速に進化する分野における研究の現状について、これらの技術の統合に関連する課題と機会を特定し、将来の方向性とオープンな研究課題の概要を示します。 そのため、QFL 手法の特性と採用された量子手法によって分類された、QFL 手法の分類法を紹介します。 このレビューは、QFL の分野を理解して発展させることに関心を持つ研究者や実践者のための、包括的なガイドとして役に立てば幸いです。

### 背景
QC の計算上の利点と、FL のプライバシー保護機能を組み合わせることにより、QFL は機械学習 (ML) モデルの開発、トレーニング、およびデプロイの方法を変革する可能性があります。

### QFLのモチベーション
QFL の動機付けは、古典的な FL の限界に対処し、QC の可能性を活用してそれを改善したいという欲求から生じています。 従来の FL 手法よりもいくつかの利点を提供する可能性があります。 QFL 開発の主なモチベーション要因には、以下のものがあります。

- プライバシーとセキュリティの強化  
FL はローカル・デバイスで生データを保持するように設計されていますが、デバイス間でモデルの更新を共有すると、機密情報が漏えいする可能性があります。 QFL は、量子鍵配送 (Quantum Key Distribution; QKD) などの量子保護された手法を使用してプライバシーを強化することができます。QKD は、従来の暗号化方式よりも安全であり、盗聴やハッキングに対してより高いレベルのプライバシーとセキュリティーの保証を提供します。

- 計算効率の改善  
複雑な FL モデルのトレーニングは、特に大規模なデータ・セットおよびモデルを扱う場合、時間がかかり、リソースを集中的に消費する可能性があります。 QFL は、量子並列処理や量子もつれ (Qunatum Entanglement) などの量子コンピューターの独自の機能を活用してトレーニング FL プロセスを高速化することで、計算効率を向上させる可能性があります。これは、迅速な意思決定が重要なシナリオで特に有益です。

- 通信オーバーヘッドの削減  
従来の FL では、デバイス間でモデルの更新を送信するプロセスは帯域幅を大量に消費し、FL プロセスの処理速度を低下させる可能性があります。 QFL は、量子データ・エンコード (quantum data encoding; QDE) などの量子技術を使用してモデルの更新を圧縮することにより、通信のオーバーヘッドを削減することができます。これにより、より効率的なモデルの更新とより迅速な収束が可能になります。

- モデル・パフォーマンスの改善  
古典的な FL 方式では、特にディープ・ラーニング (DL) で一般的な非凸最適化問題に対処する場合に、最適なモデル・パフォーマンスの達成に苦労することがあります。  QFL には、量子並列処理と量子もつれを活用することにより、より効率的な最適化アルゴリズムを提供する可能性があり、連合学習の設定でモデルのパフォーマンス改善や一般化をもたらす可能性があります。

- スケーラビリティの向上  
データとモデルの複雑性の急速な増大により、従来の FL 手法は効率的に拡張することが困難になる可能性があります。 QFL は、量子コンピューターの固有の並列処理を活用して、大量のデータ・セットを処理し、多数のノードにわたって複雑なモデルをトレーニングすることで、よりスケーラブルな FL を実現しようとしています。

- 新たな応用の有効化  
QC により、従来は古典的なコンピューティングでは計算的に実行不可能であると見なされていた新しい ML アルゴリズムおよびアプリケーションの開発が可能になります。 QFL は、これらの新しいアルゴリズムを分散設定に適用して、医療、金融、輸送などのさまざまな分野における新たな可能性を広げることができます。

### 関連研究
QFLに関連した研究の概観としては、Chen et al (2021)、Larasati et al (2022)、Kwak et al (2022）が挙げられます。以下では、QFLの次の三つの重要側面について取り上げます：
- QML (quantum ML)
- QSM (quantum-secured mechanisms)
- QOA (quantum optimization algorithms)

## 2. QC と FL のいくつかの用語と基本的事項
### 2.1. FLの基礎
FL は、複数のパーティーが、データをローカルに保持しそれによってデータ・プライバシーを保持しながら、共同で共有モデルをトレーニングできるようにする分散 ML アプローチです。 以下に、FL の一般的な分類をいくつか示します。

#### データの分布  
データ分布に基づいて、FL は水平的 FL (HFL)、垂直的 FL (VFL)、および連合転移学習 (FTL) に分類できます。HFL は、お客様が同じ特徴量空間を持っているが、異なるサンプル (つまり、IID データ) を持っている場合に使用されます。このシナリオでは、クライアントは、生データを共有せずにモデルをトレーニングするためにコラボレーションします。 HFL は、複数の組織または個人が機密情報を共有することなく共同でモデルをトレーニングする必要がある場合に特に役立ちます。 VFL は、クライアントが異なる特徴量空間を持っているが、同じサンプル集合を共有している場合に使用されます。 クライアントは、生の特徴量データを共有することなく、共同でモデルをトレーニングします。 VFL を使用すると、様々なクライアントからの補完的な特徴量集合を組み合わせて、より正確で頑健なモデルをトレーニングできます。 FTL は、FL と転移学習 (TL) を組み合わせます。FTL では、1 つのドメインで学習された知識は、データ・プライバシーを保持しながら別のドメインに転移されます。 クライアントは、事前トレーニングされたモデルや他の分野の知識を活用して、モデル・トレーニングの効率とパフォーマンスを向上させることができます。

図０: 連合学習のシナリオによるタイプ
<img src="Screenshot 2023-09-28 at 23.11.19.png" alt="図０: 連合学習のシナリオによるタイプ">

#### ネットワーク・アーキテクチャー  
ネットワーク・アーキテクチャーに基づいて、FL は集中的 FL (CFL) と非集中的 FL (DTL) に分類できます。 CFL の場合、クライアントはモデル集約のために中央サーバーと通信します。 クライアントは、データを使用してローカル・モデルをトレーニングし、モデルの更新をサーバーに送信します。 サーバーはこれらの更新を集約し、更新されたグローバル・モデルをクライアントに返します。 DFL の場合、クライアントは、中央サーバーを必要とせずに相互に直接通信します。 クライアントはピアツーピア方式でモデル更新を交換し、モデル集約は分散方式で実行されます。 DFL は、プライバシーを強化し、Single Point of Failure のリスクを軽減することができます。

#### プライバシー・メカニズム  
FL は、プライバシー・メカニズムに基づき、差分プライバシー (DP) ベースの FL (DPFL) と暗号化ベースの FL (EFL) に分類することができます。 DPFL には、集計されたモデル更新から個々のデータ・ポイントを推測できないようにするため、 DP 技法が組み込まれています。 FL のトレーニング・プロセス中にモデルの更新にノイズが追加され、モデルの効用を維持しながら強力なプライバシー保証を提供します。 EFL は、準同型暗号化 (HE) やセキュアなマルチパーティー計算 (SMPC) などの暗号化技術を使用して、FL トレーニング・プロセス中のモデル更新のプライバシーを保護します。 クライアントは、復号されることなく集約できる暗号化されたモデル更新を送信し、グローバル・モデルの品質を損なうことなくデータ・プライバシーを確保します。

#### モデル集約  
広く採用されている FL モデル集計アルゴリズムがいくつかあります。 連合平均 (FedAvg) は、ローカル・モデルの更新の加重平均を計算して、グローバル・モデルを作成します。 各クライアントのローカル・モデル更新は、トレーニング・データのサンプル・サイズによって重み付けされます。これにより、3 つのグローバル・モデルがすべてのクライアントのコントリビューションを反映するようになります。 連合確率的勾配降下 (FedSGD) は、各クライアントからの局所勾配に基づき確率的勾配降下 (SGD) を使用してグローバル・モデルを更新します。 サーバーは、クライアントからの勾配を集約し、更新をグローバル・モデルに適用します。 FedSGD は、特にクライアントの帯域幅が限られている場合やモデルが非常に大きい場合に、FedAvg よりも通信効率が優れています。 その他の高度な集計手法では、幾何平均、トリム平均、または頑健な集計アルゴリズムなど、より高度な集計方法を使用して、グローバル・モデルの品質を向上させ、ノイズや悪意のあるクライアントの影響を軽減することができます。

### 2.2. 量子力学とQCの基礎
QC は、量子重ね合わせ (Quantum Superposition) や量子もつれといった量子力学の現象を利用して、古典的コンピューターを超えた計算能力を提供します。 量子力学の原理に頼ることで、特定の問題領域については、古典的なコンピュータよりも複雑な計算をより効率的に行います。 このセクションでは、量子力学の原理と QC の基本について概説します。

#### 量子力学の原理
量子重ね合わせ  
量子力学の重ね合わせは、量子系が同時に複数の状態で存在することができることを示す、量子力学の基本概念です。 この現象は、電子や光子などの量子的粒子の波動のような性質から導出され、位置、エネルギー、その他の性質の異なる状態を同時に占有することができます。 数学的には、量子系の状態は複素ヒルベルト空間におけるベクトルによって表され、ヒルベルト空間の線型構造は、これらの状態ベクトルの線型結合もシステムの有効な状態であることを意味します。 量子重ね合わせは、量子並列性や量子もつれなど、多くの量子現象の基礎にある重要なリソースです。

量子もつれ  
量子もつれとは、2 つ以上の量子的粒子の状態が相互に絡み合って、1 つの粒子の状態が他の粒子の状態とは独立して記述できないというユニークな現象です。 この性質は重ね合わせの原理により生じ、量子情報技術に対して深い意味を持ちます。 もつれた 量子ビット (qubits) は、アダマール (H) ゲートの後に制御 NOT (CNOT) ゲートが続くような演算によって作ることができ、複数の量子ビットに対して同時に複雑で相関のある演算を実行するのに用いることができます。 量子もつれは、より効率的な計算を可能にするとともに、セキュアな通信と分散コンピューティングのための新しいプロトコルを可能にします。 

量子測定  
量子システムを観察または測定するプロセスを記述する量子力学の重要な概念です。 重ね合わせの原理により、量子系は射影測定 (projective measurement) が行われるまで同時に複数の状態に存在することができます。 測定時に、量子系は可能な状態の 1 つに崩壊し、その確率は各測定結果に関連する係数の絶対値の二乗によって決定されます。 この崩壊は本質的に確率的なものであり、結果を確実に予測することはできません。

#### QCの基礎
量子ビット  
QC の基本的なビルディング・ブロックは量子ビット (qubit) であり、古典的ビットとは異なり、0 と 1 だけでなく、両方の状態の重ね合わせを表すことができます。 数学的には、量子ビットはその基底状態 $|0\rangle$ と $|1\rangle$ の線型結合として記述することができます：  
$$|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$$  
ここで、$\alpha$ と $\beta$ は $|\alpha|^2 + |\beta|^2 = 1$ を満たす複素数である。 このユニークな特性により、量子コンピューターは、単一の量子ビットで複数の可能性をエンコードすることにより、膨大な量の情報を同時に処理することが可能となっています。 複数の量子ビットを持つと、アクセス可能なヒルベルト空間の次元は指数的に大きくなり、古典的なコンピュータでは扱いにくい問題を解くことができるようになります。

量子ゲートと量子回路  
量子ゲートは、制御された方法で量子ビットの状態を操作するために用いられる基本的な演算です。 量子演算 (ユニタリ変換) はゲートの列によって任意の精度で実装することができます。 一般的な量子ゲートには、Pauli-X、Y、Z、Hadamard、Phase S、CNOT ゲートがあります。 これらのゲートは Clifford 群と呼ばれます。 しかし、Clifford 群のみで構成された量子回路は、古典的なコンピュータ上で効率的にシミュレートすることができます。 そのため、量子的スピードアップを示すためには、Toffoli (CCNOT) ゲートのような non-Clifford ゲートを含めることが不可欠です。 特に、量子ゲートは可逆であり、量子状態を元の状態に戻すことができ、量子ゲートの逆演算も容易に計算することができます。

### 2.3. 量子アルゴリズムと複雑性
量子アルゴリズムは、量子重ね合わせや量子もつれなどの量子現象のユニークな特性を利用して、複雑な問題に対して古典的なアルゴリズムを大幅に高速化します。 いくつかのよく知られた量子アルゴリズムには、素因数分解のための Shor のアルゴリズム (暗号理論に重要な意味を持つ) や、古典的な探索アルゴリズムに対して 二次高速化 (quadratic speedup) を提供する非構造化探索のための Grover のアルゴリズムがあります。 連立一次方程式を解くための Harrow-Hasssidim-Lloyd (HHL) アルゴリズムのような他の量子アルゴリズムは、ML や最適化に向けて提案されている。

量子複雑性理論は、量子アルゴリズムが必要とする計算資源を研究し、しばしば量子ビットの数と量子ゲート演算の数で表現されます。 BQP (bounded-error 量子多項式時間) のような複雑性クラスは、量子コンピューターによって効率的に求解できる問題を表します。 BQP は古典的な複雑性のクラスよりも大きいと考えられており、一部の問題は古典的なコンピュータよりも量子コンピュータを使ってより効率的に解決できることが示唆されている。
このセクションでは、QML、QSM、QOA などの 3 つの観点から、量子アルゴリズムと複雑性について説明します。

#### QML
変分量子分類器 (VQC)  
VQC は QC の原理を使ってデータに対して分類タスクを行います。 VQC は、古典的な最適化技術を使用して最適化されたパラメータ化された量子回路である変分回路の概念に基づいて構築されています。 VQC の目的は、コスト関数を最小化する最適なパラメーターを見つけることです。 VQC は、データ・エンコーディング（量子ビットとして符号化するプロセス）、変分回路、測定、最適化、評価などの 5 つのステップに分けることができます。図１が示す VQC の基本構造にあるように、 CNOT ゲートと回転ゲート (Rotation Operator Gate) の２種類の量子ゲートから構成されています。回転ゲート $R_x(\theta)$、$R_y(\theta)$、$R_z(\theta)$ は、三つのデカルト座標軸周りの回転行列であり、$\theta$ は、座標軸に対する回転角度です。

図１: VQC の基本構造 (Ren et al 2023)
<img src="Fig-1.png" alt="図１: VQC の基本構造">

##### 量子畳み込みニューラルネットワーク (QCNN) 
QCNN は、ニューラルネットワーク (NN) のトレーニングと推論を加速するために QC の可能性を探索する研究領域です。 参照 [9] は、古典的な ML で広く使われている建築物である畳み込み NN (CNN) の量子バージョンを提案している。 QCNN は、特定の画像認識タスクで従来の CNN よりも優れたパフォーマンスを実現できます。

##### 量子 LSTM (QLSTM)
LSTM セルの古典的な NN を VQC に置き換えることにより、古典的 LSTM を量子領域に拡張します。ここでVQCは、特徴抽出とデータ圧縮の両方の役割を果たすことになります。

##### 量子生成的敵対ネットワーク (QGAN)
QGAN は、QC の原理を生成モデル領域に適用することを目指す新しい研究領域です。 例えば、データが量子状態または古典的なデータで構成され、生成器と識別器に量子情報プロセッサーが装備した研究があります 。

##### 量子転移学習
現代の ML アルゴリズムで広く適用されている転移学習 (TL) の概念を、古典的な要素と量子的な量素からなるハイブリッド NN に拡張しようとした研究があります。

##### ハイブリッド古典-量子 NN
古典 NN の量子版は多くあるが、NISQ は、近い将来使うことのできる唯一の量子デバイスとなるでしょう。そこでは、誤り修正が無い限定的な数の量子ビットだけが使われます。複数の QNN 層からなる量子深層学習 (QDNN) など。

#### QSM
QSM アプローチは、データ伝送のセキュリティーを強化するために量子通信に依存しています。 図 2 は、量子通信における主要な情報キャリアである光子の文脈における量子通信の原理を簡潔に説明しています。 量子セキュリティーは、測定の不可逆性にかかっています。 従来、古典的なビットは二極化の方向によって表現されます。 図 2 に示すように、盗聴者 Eve が使用する X 基底は、二極化の元の方向を 50% の確率で 2 つの方向に変化させます。 したがって、盗聴者によって測定されると、量子ビット・エラー率 (QBER) が高くなります。 QKD と量子セキュア直接通信 (quantum secure direct communication; QSDC) はどちらも、盗聴に対するセキュリティを提供するために上記の量子通信の原理を活用するセキュアな通信プロトコルです。 QKD は暗号鍵の交換に重点を置いていますが、QSDC は秘密メッセージの直接伝送を可能にします。


図２：量子通信の原理 (Ren et al 2023)
<img src="Fig-2.png" alt="図２：量子通信の原理">


本稿では、これ以上の解説は割愛します。

#### QOA
QOA は量子的手法 (量子重ね合わせ、干渉、もつれなどの、複数光子の量子的性質) を用いて、数十年にわたって効率的な解決策に抵抗してきた難しい問題に匹敵する複雑さ (NP-困難) を持つ挑戦的な最適化問題に取り組むことを目的としています。

##### 量子回路分割 (quantum circuit cutting; QCC)
現代の量子コンピューターは NISQ デバイスであり、低い量子ビット数とノイズのある演算によって制約されており、スケーラビリティーという点でエンジニアリング上の大きな障害にも直面しています。 これらの課題を解決するために、QCC を活用して小型量子コンピュータの能力を強化する試みがなされています。 QCC は、特定の計算を実行するために必要なゲートと演算の数を減らすことを目的として、量子回路をより小さな下位回路に分解することによって実装を合理化し、全体的なランタイムとリソースの要求を低減することを目的としています。 QCC では、大規模な回路を識別し、独立して実行できる小さな下位回路に分割し、古典的計算資源で検出された結果を後処理する必要があります。 分割プロセスでは、ゲート間の依存関係を分析し、それらを並列に実行できるグループに分離する方法を見つけます。 図 3 は 1 量子ビット の場合の Pauli QCC 法を示していますが、そこでは QCC は Pauli 分解規則を適用して Pauli ゲート列に回路を分解しています。 これらの規則は、任意の単一量子ビットのユニタリ演算は、単一量子ビットの Pauli ゲートを使って実装できる、X, Y, Z 軸に関する回転の列へと分解できることを述べています。

図３：QCC の基本構造（1 量子ビットの場合のPauli 回路分割法の例） (Ren et al 2023)
<img src="Fig-3.png" alt="図３：QCC の基本構造（1 量子ビットの場合のPauli 回路分割法の例">

##### Grover のアルゴリズム
Grover のアルゴリズムは、N 個の要素からなるソートされていないデータベースを検索することを目的としています。 Grover のアルゴリズムは、古典的な探索アルゴリズムに優る二次高速化を提供し、QC の潜在的な能力を示す基礎となる量子アルゴリズムの 1 つとなっています。 従来の探索アルゴリズムでは、ターゲット要素を見つけるのに平均して $O (n)$ 回の反復が必要になりますが、 Grover のアルゴリズムでは、$O (\sqrt{n})$ 回だけの反復で高確率でターゲット要素を見つけることができます。

##### HHL アルゴリズム
HHL アルゴリズムは、連立一次方程式を効率的に求解します。 HHL アルゴリズムは、 ML やデータ処理などの連立一次方程式の求解が中核的要素になている様々な問題に適用できます。 連立一次方程式を求解する従来の古典的アルゴリズムは、問題のサイズに応じて指数関数的なランタイムを持っているため、大規模な問題では実用的でなくなります。

##### 変分量子固有値ソルバー (Variational Quantum Eigensolver; VQE)
図 4 は、VQE の考え方を示しています。 VQE アルゴリズムの基本的な考え方は、パラメータ化された量子ゲートのセットを使って量子コンピュータ上で試行波動関数 (trial wave function)を準備することです。 これらのゲートは、 Pauli ゲートを使用して実装できる X 軸、Y 軸、Z 軸の回転など、単純で効率的なものとして選択されています。 これらのゲートのパラメーターは、エネルギー期待値を最小化するために、古典的なやり方で最適化されます。 VQE アルゴリズムは分子特性を研究するための強力なツールであり、古典的なコンピュータを使ってシミュレートするには大きすぎる分子の基底状態エネルギーを見つけることができる。 VQE は、問題のコスト関数を表すハミルトニアンを構築することにより、最適化問題を解くのに適用できます。 このハミルトニアンの基底状態エネルギーを見つけることで、VQE は本質的に最適化問題に対する最適解を見つけます。 VQE は、分子の基底状態エネルギーを見つけるという問題を量子回路へとまずエンコーディングすることによって機能します。 この回路は量子コンピュータ上で実行され、分子の基底状態を近似する出力状態を生成します。 その後、出力状態が測定され、測定された結果を使って分子のエネルギーの推定値が計算されます。 このエネルギー推定値は量子回路にフィードバックされ、回路が更新されると、真の基底状態エネルギーにより近い新しい出力状態を生成します。

図４：VQE の基本構造 (Ren et al 2023)
<img src="Fig-4.png" alt="図４：VQE の基本構造">

##### 量子近似最適化アルゴリズム (QAOA)
QAOA は、組み合わせ最適化問題を量子系のエネルギーの数学的表現であるハミルトニアンに位置付けることによって解決するように設計されています。 ハミルトニアンは、問題を記述する目的関数と制約関数のセットを使用して構成されます。 次に、このアルゴリズムは量子ゲート列を系の量子状態に適用し、それにより系はハミルトニアンの基底状態に向かって展開します。 ハミルトニアンの基底状態は、元の組合せ最適化問題の最適解に対応します。 QAOA は、古典的な計算と量子計算を組み合わせており、QAOA の古典的な部分は、システムのエネルギーを最小化するために量子ゲートのパラメータを最適化することを含みます。

## 3. QFLの分類
Chen et al (2023) は、現在及び潜在的な QFL のアプローチ体系的かつ包括的なレビューにおいて、図 5 に示すように、QFL を次の 2 つのカテゴリーに分類する分類法を提案ています：
- 効率的な QFL (EffQFL)
- セキュアな QFL (SecQFL)

図５：QFL の分類  (Ren et al 2023)
<img src="Fig-5.png" alt="図５：QFL の分類 (Ren et al 2023)">

この分類は、各カテゴリーに関連する特性と量子アルゴリズムに基づいています。 EffecQFL と SecQFL の目的は、それぞれ FL タスクで QC の適用を成功させるために重要な QFL の 2 つの重要な側面に対処することです。 これらの 2 つの側面は、異なっていますが補完的な目標に重点があります。 以下に、EffQFL と SecQFL のアプローチの概要を示します。

### 3.1. EffQFL
EffQFL は、古典的な FL 手法よりも効率的かつ効果的にデータから特徴量を学習するために、 QC の可能性を最大化します。 目標は、QOA と QML を活用して、FL のトレーニングの迅速化、スケーラビリティーの向上、およびパフォーマンスの向上を実現することです。 EffQFL は主に、以下の問題に対処しています:

- スケーラビリティ  
大規模なデータ・セットや高次元データを扱う際に、古典的な FL 方式はスケーラビリティーに苦労する可能性があります。 EffQFL は、大規模な問題を効率的に処理し、計算の複雑さを改善できる QOA と QML を開発することを目的としています。

- スピード  
複雑な FL モデルのトレーニングは、時間がかかります。 EffQFL は、学習プロセスをスピードアップするために、重ね合わせ、もつれ、量子干渉などの量子特性を活用することに重点を置いています。

- 表現力  
適切な特徴表現を見つけることは、FL のパフォーマンスにとって不可欠です。 EffQFL は、量子特徴量マップ (QFM) と量子回路を調べることにより、複雑で高次元の特徴表現が生成され、モデルのパフォーマンスを改善します。

- リソース効率の向上  
QC のリソースは現在制限されており、効率的な QOA および QML の設計が不可欠です。 EffQFL は、既存の量子ハードウェアに実務的に実装できるリソース効率の良いメソッドを開発します。

このカテゴリーの EffQFL は、データ処理ベース、モデル最適化ベース、およびクライアント選択ベースのアプローチに分類されます：
- データ処理ベースの EffQFL は、特徴量エンジニアリングの量子バージョンの調査に重点を置いています。 
- モデル最適化ベースの EffQFL は、グローバル部分 (目的関数ベースおよびモデル集約ベースのアプローチを含む) とローカル部分 (パラメーター化された QML ベースおよび勾配ベースのアプローチを含む) で構成されます。
  -  グローバル・モデル最適化ベースの EffQFL は、最適化のための QOA の開発に重点を置き、QAOA や VQE のような特定のタスクでパフォーマンス改善を達成できる量子にインスパイアされたアルゴリズムを開発します。
  - 他方、ローカルモデル最適化ベースの EffQFL は、手元の特定の問題に適応できるパラメータ化された QML の開発や、ノイズや接続性の制約など、現在の QC デバイスの限界を考慮したハードウェア考慮のある回路設計の開発に重点を置いています。
- クライアント選択ベースの EffQFL は、リソース効率の高い QOA に焦点を当て、QC リソースの実用的な使用を可能にします。 

EffQFL の応用例としては、高次元のデータ分析と次元削減、画像・信号処理、自然言語処理 (NLP)、創薬、材料科学などが挙げられます。

要約すると、EffQFL は、QC を使用した特徴量エンジニアリングの効率と有効性を向上させることができます。 さらに、量子特性を活用して、複雑な特徴量表現を作成し、学習プロセスを迅速化することができます。 さらに、リソース効率の良い量子回路と最適化アルゴリズムを開発し、古典的な FL から QFL への移行を促進します。

### 3.2. SecQFL
SecQFL は、敵対的攻撃、量子攻撃、無許可アクセスなどに対してセキュアで頑健な QFL メソッドの開発に重点を置いています。 主な目的は、FL プロセスに QSM および QML を使用する際に、データ・プライバシーとモデル・セキュリティーを確保することです。 SecQFL は主に、以下の問題に対処します。

- データ・プライバシー  
データ・プライバシーの確保は不可欠であり、特に医療や金融のような機密性の高いアプリケーションでは、データ・プライバシーの確保が不可欠です。

- モデル・セキュリティー  
FL モデルを無許可アクセスから保護することは、通信中に非常に重要です。

- 頑健性  
FL アプローチは、ノイズ、ハードウェア・エラー、攻撃に対して回復機能がなければなりません。SecQFL には、QEC などの手法が含まれており、そのような不完全性があっても信頼性の高いパフォーマンスを維持します。

このカテゴリーの SecQFL は、データ・プライバシー・ベース、モデル・セキュリティー・ベース、および頑強性ベースのアプローチに分類されます：
- データ・プライバシー・ベースの SecQFL は、量子 HE (QHE)、量子 DP (QDP)、量子 SMPC (QSMPC) などのデータ・プライバシーを保護しながら、機密情報を漏洩することなくデータから特徴を学習できるようにする量子プライバシー保護技術の開発に重点を置いています。
- モデル・セキュリティー・ベースの SecQFL は、量子暗号化技法に基づいており、伝送中および保管中のデータを保護するために QKD や QSDC などのセキュアな通信プロトコルを開発するために量子特性を活用します。
- 頑健性ベースの SecQFL は、QEC、ポスト量子暗号、格子ベースの暗号化などの QSM および耐量子 ML アルゴリズムを開発することにより、量子攻撃、敵対的攻撃、ハードウェアの欠陥、ノイズに対して耐性を持つことを目的としており、 QC リソースを利用できる攻撃者からの攻撃にモデルが耐えることができます。 SecQFL の潜在的な適用には、セキュアな金融取引と不正検出、プライバシーを保護する医療データ分析、サイバー・セキュリティーと侵入検知などが含まれます。

要約すると、SecQFL は、潜在的な脅威に対する QFL メソッドのセキュリティー、プライバシー、および頑健性を確保できます。 さらに、データ・プライバシーとモデル・セキュリティーが重要な機密アプリケーションでの量子学習の採用を可能にします。 さらに、QC リソースが利用可能な攻撃者からデータとモデルを保護し、コラボレーション型および分散型の学習シナリオのためのプライバシー保持手法を開発します。

## 4. EFFQFL
このセクションでは、EffQFL の手法について説明します。 これらの技法の基本的なセットアップと構成を図 6 に示します。

図６：EffQFL アプローチの図解 (Ren et al 2023)
<img src="Fig-6.png" alt="図６：EffQFL アプローチの図解 (Ren et al 2023): a) データ処理ベースの EffQFL ； b) モデル最適化ベースの EffQFL ; c) クライアント選択ベースの EffQFL">
a) データ処理ベース EffQFL、 b) モデル最適化ベース EffQFL、 c) クライアント選択ベース EffQFL

### 4.1. データ処理ベースの EffQFL
データ処理ベースの EffQFL 手法は、古典的な特徴量工学技術に対する量子エンコード (図 7 に示す) の開発を強調しています。 これらの手法は、QC プロパティーを活用することにより、量子特徴量エンジニアリング手法の効率とパフォーマンスを向上させ、オーバーフィッティングを軽減し、データの可視化と理解を促進することを目的としています。 データ処理ベースの EffQFL 内の主なフォーカス領域には、以下が含まれます。

図７：量子エンコーディング (Ren et al 2023)
<img src="Fig-7.png" alt="図７：量子エンコーディング (Ren et al 2023)">
(QuAM: Quantum Associative Memory; QRAM: Quantum Random Access Memory)

1. QDE  
このアプローチは、異なるコード化スキームを調査することにより、古典的データを量子状態に効率的に変換することに重点を置いています。 目標は、量子系でのデータのエンコードと処理に必要なリソースを最小限にすることです。 研究者は、さまざまなタイプのデータ (連続型、離散型、またはカテゴリー型) を量子状態に効率的にエンコードする方法を研究し、その本質的な関係と特性を保持しながら、エンコードに必要な量子回路の複雑さとデータ表現の精度の間のトレードオフを検討します。 この領域は、特徴量エンジニアリングにおける従来の特徴量抽出および前処理の方法に類似しています。
<!-- 
参照 [67] は、ユーザー・データ・プライバシーを維持し、計算負荷を分散させながら、無線ネットワークにおける非直交多重アクセス (NOMA) 電力配分を最適化するための統計 QFL (SQFL) アプローチを提案します。 SQFL は、NN 推論を実行するために他のエッジを必要とせずに、QDE によって統計情報をクラウドに送信できます。 [68] の作業では、QDE メソッドを使用して、VQC による非集中データに関する量子データを生成します。 [69] では、入力音声は非集中 Mel-spectrogram 機能抽出のために QC サーバーにアップストリームされ、対応する畳み込み機能は VQC を使用してエンコードされます。 [70] の資料では、NLP 領域での量子エンコードに VQC を使用しています。 参照 [71] は、大規模な分散量子ネットワークの量子クラスター状態の引用で構成される、階層データ・フォーマットを持つ最初の量子統合データ・セットを生成します。 [21] のレビューでは、QDE の VQC も使用されます。
-->

1. QFM  
QFM は、量子特性を活用することにより、古典的なデータの高次元非線形表現を作成します。 これらの特徴量マップは、カーネル法などの古典的な特徴量変換技法の量子バージョンを提供します。 この分野の研究者は、QML モデルの性能を向上させる表現的かつ効率的な QFM を設計することを目的としています。
<!-- 
例えば、表現的かつ複雑な特徴表現を生成する非線形 QFM の探索、データの基礎構造を取り込むための量子モデルのリソース効率機能の向上、特定のタスクに最適な QFM の選択または構築、特徴マップの表現力のバランス化などが考えられます。 ハードウェアの欠陥が存在する場合の安定性と回復力を向上させるために、ノイズおよび潜在的なハードウェアの不完全な対策に対する QFM の頑強性を調査します。

量子分割学習 (QSL) 方式は QCNN を FL [72] に統合し、クロスチャネル・プーリングを利用して、QCNN による量子状態トモグラフィーのユニークな性質をフルに活用します。 QSL は、基本的な QFL よりも高い精度を実現することができ、収束の迅速化、通信コスト、さらにはプライバシーにおいても多くの利点を発揮します。
-->

3. 量子特徴量選択 (QFS) と量子次元削減 (QDR)  
QFS は、データ処理ベース EffQFL の重要な側面であり、重要な特徴量のサブセットを戦略的に選択することにより、所与のタスクに最も関連性が高く情報量のある特徴量を特定することに重点を置いています。 QDR は、QC 環境でデータ・セットの基本特性を保持しながら、データ・セットの次元数を削減するプロセスです。
<!-- 
QML を使用する QFS は、これらのモデルから特徴量重要度情報を抽出するように QML モデルをトレーニングすることを目的としています。 例えば、トレーニングされた QNN の重みまたはパラメーターを分析することにより、モデルの予測に寄与する特徴量を判別し、それらを適宜選択できます。 QOA を使用する QFS (量子変量特性選択 (QVFS) など) は、特定の評価基準 (分類精度、情報ゲインなど) を最大化する機能の最適なサブセットを検索するために使用できます。 疎性誘発ペナルティー項を組み込むことにより、QVFS は、高い予測パフォーマンスを維持しながら、より小さな機能のサブセットを選択することを推奨します。 量子主成分分析 (QPCA) では、データ共分散行列の最大固有値に対応する主成分 (固有ベクトル) を見つける必要があります。 これらの固有ベクトルと固有値を計算するために HHL アルゴリズムを使用することができ、従来の方法と比較してプロセスを高速化する可能性があります。 量子等角埋め込み (QISO) は、VQE を活用してデータを低次元量子状態空間に埋め込むことで、低次元空間におけるデータ点間の距離を保持することを目的としています。 このアルゴリズムは、データ・ポイント間のペアごとの距離の保存を測定するコスト関数を最適化します。 量子局所線形埋め込み (QLLE) は、データ・セットの局所幾何学を保持しながら、データの低次元表現を見つけることを目的としています。 データ・ポイント間のローカル関係は、各データ・ポイントを下位ディメンション・スペース内の隣接データ・ポイントの線形結合として再構成することによって保持されます。
-->

### 4.2. モデル最適化ベースの EffQFL
モデル最適化ベースの EffQFL は、QOA を通じてモデルのトレーニングと集計の効率と有効性を向上させることに重点を置いています。 このカテゴリーは、グローバル・モデル最適化アプローチとローカル・モデル最適化アプローチに分類されます。

#### グローバル・モデル最適化ベースの EffQFL
グローバル・モデル最適化ベースの EffQFL は、QOA と量子に基づく技術を開発することで、学習プロセス全体を最適化することを目標としています。 これらのアプローチにより、特定のタスクのパフォーマンスを向上させることができます。 主なサブカテゴリーには、次の 2 つがあります。

1. 目的関数ベースの EffQFL  
これらのアプローチは、FL プロセスを導く QOA を使用してグローバル・モデルの目的関数を直接最適化することを目的としています。 研究者は、モデルのパフォーマンスを向上させるために QOA を使用して最適化できる新しいコスト関数、損失関数、または目的関数を開発します。 技法には、QAOA、VQE、および量子メトロポリス・サンプリングが含まれます。これにより、コンバージェンスを加速し、モデルのパフォーマンスを向上させることができます。 QAOA は、複数のクライアントにわたる損失機能を最小化することにより、グローバル・モデルの目的関数を最適化するように適応させることができます。 研究者は、FL 損失関数を適切なハミルトニアンにマップし、VQE を適用して、最適なモデルパラメータに対応する最小エネルギー状態を見つけることができます。 量子メトロポリスサンプリングは、古典的なマルコフ連鎖モンテカルロ法であるメトロポリス・ヘイスティングス法に基づいている。 量子バージョンにより、FL 設定で損失関数のランドスケープをより効率的にサンプリングできるため、最適化プロセスが加速されます。 ベイズ推論の FL シナリオでは、量子メトロポリス・サンプリングを使用して、モデル・パラメーターの事後分布を効率的に探索することができます。これにより、収束が速くなり、モデル・パフォーマンスが向上します。
<!-- 
さまざまなチャネル条件に対応するために、[73] の ESQFL は、複数の深さにわたって重ね合わせ符号化を適用し、収束境界を導出して最小化することにより、重ね合わせ符号化の割り当てを最適化します。 この作業では、非常に不十分なチャネルの下での障害、成功した受信の重要性、NISQ の制限、およびいくつかの重要なメトリックが考慮されました。
-->

2. モデル集約ベースの EffQFL  
このサブカテゴリーは、量子 FedAvg や量子 FedSGD などの効率的なモデル集約のための集約手法の量子バージョンを使用することに焦点を当てています。量子並列処理を活用して、FL でのモデル集約に必要な集計時間と計算リソースを削減する量子にインスパイアされたモデル集計手法です。 このようなアプローチを使用して、並列モデル平均化を実行し、集約プロセスを大幅に加速することができます。 例えば、大規模データを持つ複数のクライアントが関与する FL 設定では、量子にインスパイアされたモデル集約を使用して、すべてのクライアントからのローカル・モデル更新の加重平均を同時に計算することができます。これにより、全体的な集計時間が短縮されます。
<!--
参照 [74] は、QFL における非 IID の問題を検討し、ローカル密度推定量を利用して各クライアントによって訓練されたローカル・チャネルにグローバル量子チャネルを分解するための量子フェデレーテッド推論 (QFedInf) 方式を提案します。 この方法により、IID 以外のデータで QFL の 1 回限りの通信の複雑さを実現できます。 参照 [75] は、各ノードによってアップロードされる更新の統一性に基づいて、グローバル更新のための QuanFedPS アルゴリズムを提案します。 この研究では、Lemma が更新の統一を適用する順序はほとんど問題にならないことを検証し、更新の統一はほぼ確実に相乗的同一性プロパティーを示すことになる。
-->

#### ローカル・モデル最適化ベースの EffQFL
ローカル・モデル最適化ベースの EffQFL は、クライアント・レベルで QFL プロセスの特定の側面の最適化に集中します。 カテゴリーは、主に次の 2 つのサブカテゴリーに分けられます。

1. パラメータ化された QML ベースの EffQFL  
これらの手法には、特定の問題に適応するための量子 NN や量子サポート・ベクトル・マシン (SVM) などのパラメータ化された QML モデルの設計とトレーニングが含まれます。 研究者は、これらのモデルを効率的にトレーニングするために QML を検討し、ローカル・モデルのパフォーマンスを向上させるためにデータ処理ベースのアプローチを取り込むための手法を開発しています。

<!--
[76] の論文は、アクセス・ポイントとクラウドで QNN 操作を使用することによりワイヤレス用の 2 層 QFL アーキテクチャーを提案しており、将来のワイヤレス通信のための効率的なソリューションとなっています。 [68] の作業は VQTN を使用し、パラメーター・ランドスケープ内で近似最適性を検出します。 [69] では、VFL の分散アーキテクチャーにより、QCNN を使用した自動音声認識への新しいアプローチが提案されています。 [70] の論文は、事前に訓練された BERT モデルと量子の利点を組み合わせたテキスト分類のためのハイブリッド古典量子 NN モデルを提案している。 提案されたモデルには、BERT ベースのデコーダーのいくつかの層を置き換えるランダム量子時間的畳み込み (QTC) 学習フレームワークが含まれています。これにより、インテント分類タスクで競合するパフォーマンスが得られます。 参照 [77] は、スリムブル QFL (Slimmable QFL) と呼ばれる FL フレームワークに量子スパイク・ニューラル・ネットワーク (QSNN) を使用しています。 このようにして、ローカル QSNN モデルの極と角度のパラメーターを個別にトレーニングし、動的に伝達することができます。 したがって、SlimQFL は、通信チャネルの条件が悪い場合は、他の QFL メソッドよりもパフォーマンスが優れています。 [73] の論文は、entangled slimmable 量子ニューラル・ネットワーク (ESQNN) の深さ調整可能なアーキテクチャーを使用して、entangled slimmable QFL (ESQFL) を提案しています。 [21] のレビューでは、ハイブリッド・クォンタム・クラシカル TL に関する統合トレーニングのフレームワークとプロセスが提供されています。
-->

2. 勾配ベースの EffQFL  
このサブカテゴリーは、FL における勾配計算と最適化のためのハードウェアを意識した量子回路の設計に焦点を当てています。 QCC は大きな量子回路を小さな管理可能な断片に分解し、限定された量子ビットとノイズ操作で近い量子デバイス上で実行することができます。 例えば、deep QNN をトレーニングするための FL シナリオでは、クライアントは QCC を適用して複雑な勾配計算回路を分解し、NISQ デバイスで実行できるようにすることができます。 その他のアプローチとしては、量子勾配降下 (QGD) と量子自然勾配 (QND) があり、これらは QC 機能を利用して古典的な手法よりも効率的に勾配を計算し、局所モデルを最適化する。 QGD は古典的な勾配降下アルゴリズムの量子アナログであり、量子演算を使ってモデルパラメータをより効率的に計算・更新する。 この方法は、FL タスクのローカル・モデル最適化に適用でき、収束を加速する可能性があります。 線形回帰の FL 設定では、クライアントは QGD を使用してローカル・モデルのパラメーターを効率的に更新し、古典的な勾配降下法と比較して高速な収束を実現できます。 QNG は、量子パラメータ空間の幾何学を考慮した QGD の拡張であり、より効率的で堅固な最適化につながる。 量子パラメータ空間の非ユークリッド構造を考慮することにより、QNG は FL の局所モデル最適化においてより高速な収束とより良い性能を提供することができる。 例えば、VQC をトレーニングするための FL シナリオでは、クライアントは QNG を使用して、量子パラメーター空間の固有の形状を考慮することでローカル・モデルを最適化し、最適化と汎化を向上させることができます。

<!--
[68] の作業では、ローカル・モデルに量子 SGD (QSGD) を使用して、分析グラジエントのコストが高くなりすぎないようにします。 [78], [79] のプリプリントでは、QFL のためのフェデレーテッド量子自然勾配降下 (QNGD) が導入されています。 FQNGD アルゴリズムは、VQC ベースの QNN で構成される QFL フレームワークに適用されます。 これらの論文は、統合された QNGD がローカル量子デバイス間の通信コストを大幅に削減できることを示している。 手書きの数字の分類に関する実証的な研究は、理論上は他の SGD 方式よりも FQNGD のパフォーマンス上の利点を示しています。 [80] の作業では、プライベート単一パーティーのグラジエント推定のために QGD がデプロイされます。これにより、QFL アーキテクチャーのお客様は、各反復で古典的なグラジエントを取得することができます。 このようにして、時間の複雑さを軽減し、データ・セット・スケールの指数加速と、従来の対応するデータ・ディメンションの 2 次高速化を実現することができます。 最も一般的な量子勾配計算器の 1 つであるパラメーター・シフト・ルールは、モデルのトレーニングに適用されます。 次に、[73] の ESQNN は、QGD を使用して適宜トレーニングされます。 QuantFed は、[75] で提案されています。これにより、ノード選択戦略 (QuanFedNode アルゴリズム) を持つ複数の量子ノードが、ローカル量子データを使用してコラボレーションし、グローバル QNN モデルをトレーニングすることができます。 このフレームワークは、QC の能力を活用して、従来の ML における計算能力の制限を克服します。
-->

### 4.3. クライアント選択ベースの EffQFL
これらのメソッドは、リソース効率の高い QOA の設計に重点を置き、QC リソースを実際に使用できるようにします。 目標は、FL タスクに最も関連性の高いクライアントを選択し、モデルのパフォーマンスを維持しながら、必要な通信リソースと計算リソースを最小限に抑えることです。 このような方法により、クライアントの選択の効率性、公平性、および適応性を向上させ、クライアントのデータ分布、モデル品質、およびリソース可用性における動的な変更を考慮することができます。

1. 量子クラスタリング・ベースの EffQFL  
これらのメソッドは、データ分布またはモデル・パラメーターに基づいてクライアントをグループ化し、FL タスクに参加する各クラスターから代表的なクライアントを選択することで、通信オーバーヘッドを削減します。

<!--
[68] の研究では、QCC を使って量子最適化を近似し、FL の Ising モデルに対応することを目指している。 このトレーニング・プロセス中に、QFL は複数のクライアントとコラボレーションして、MaxCut の問題を効果的に解決することができます。
-->

2. 量子公平性とアダプティブ・ベースの EffQFL  
このような手法は、 Grover の探索などの量子アルゴリズムを採用して、データ多様性やモデル性能などの特定の基準に基づいてお客様を効率的にサンプリングし、選択したクライアントがグローバル・モデルに価値ある情報を提供できるようにすることで、クライアント選択時の公平性と適応性を確保します。 多様なデータ・コントリビューションとモデル品質を持つクライアントとの FL 設定では、公平性を意識したクライアント選択方式により、クライアントの参加のバランスを取ることができます。これにより、少数のクライアントの優位性を防ぎ、十分に代表されていないクライアントを含めることが促進されます。 時間の経過とともにデータ・コントリビューションおよびリソース制約が変化する FL システムの状況の変化に基づいて、アダプティブ・クライアント選択方式は、現在の状態に最も適したクライアントを選択することにより、システムの全体的なパフォーマンスおよびコンバージェンスを維持するのに役立ちます。

## 5. SecQFL
このセクションでは、SecQFL のアプローチについて説明します。 これらの技法の基本的なセットアップと構成を図 8 に示します。 提案された分類法に基づいて、SecQFL のアプローチは、以下に詳述するように、データ・プライバシー・ベース、モデル・セキュリティー・ベース、頑健性ベースのアプローチに分割されます。 各カテゴリーは、量子力学の原則、QSM および QML 機能を活用することにより、QFL のプライバシーとセキュリティーを向上させることを目的としています。

図８：SecQFL アプローチの図解 (Ren et al 2023)
<img src="Fig-8.png" alt="図８：SecQFL アプローチの図解 (Ren et al 2023)">
(a) データ・プライバシー・ベース SecQFL; b) モデル・セキュリティー・ベース SecQFL; c) 頑健性ベース SecQFL)

### 5.1. データ・プライバシー・ベースの SecQFL
これらのアプローチは、QHE、QDP、QSMPC などのデータ・プライバシーを保護する量子プライバシー保持手法の開発に重点を置いています。これらの手法により、機密情報を漏えいすることなくデータから学習機能を取得できます。

QHE を使用すると、暗号化解除を必要とせずに、暗号化されたデータに対して計算を実行できます。 FL では、QHE を使用して機密データのプライバシーを確保しながら、クライアントとサーバーが共同でグローバル・モデルをトレーニングできるようにすることができます。 量子完全 HE (QFHE) は、暗号化されたデータに対する任意の計算をサポートする QHE の拡張形式です。 FL 設定では、クライアントは QFHE を使用して機密データを暗号化してからサーバーに送信することができます。 その後、サーバーは、生データにアクセスすることなく、暗号化されたデータに対して直接、モデル更新などの量子計算を実行できます。 このプロセスでは、効果的なモデル・トレーニングを引き続き可能にしながら、クライアント・データのプライバシーを保持します。 QDP は、制御された量子ノイズを量子データまたは量子計算に追加して、個々のデータ・ポイントのプライバシーを確保すると同時に、データ・セットからの正確な学習を可能にするプライバシー・フレームワークです。 量子ローカル DP (QLDP) は、データまたはモデルの更新をサーバーに送信する前に、各クライアントによってノイズがローカルに追加される QDP のバリアントです。 この方法では、サーバーが元のデータまたはモデルの更新にアクセスできないため、プライバシーがさらに強化されます。 QSMPC を使用すると、複数のパーティーが入力を非公開にしながら、入力に対して関数を共同で計算することができます。 FL では、QSMPC を使用して機密データを保護しながら、クライアント間のセキュアなコラボレーションを実現できます。 量子認識転送 (QOT) は、QSMPC における基本的なプリミティブであり、送信側は、どの部分が選択されたかを知らずに、いくつかの情報の 1 つを受信側に送信することができます。 FL では、FL プロセス中にクライアント・データのプライバシーを保護する、より複雑な QSMPC のビルディング・ブロックとして QOT を使用できます。
<!--
[68] の作業では、量子力学の特性を利用した QSMPC を展開し、フェデレートされた勾配を安全に計算するという課題に対処します。
-->

### 5.2. モデル・セキュリティー・ベースの SecQFL
これらのアプローチは、量子暗号技術に基づいており、QKD や QSDC などのセキュアな通信プロトコルを開発するために量子プロパティーを使用して、伝送および保管中のモデルの更新を保護します。 BB84 や E91 などの QKD プロトコルを使用して、クライアントと FL システムのサーバーとの間で暗号鍵を安全に配布できます。 QKD は、量子情報の固有の特性を活用することで、盗聴の試みを検出して防止し、学習プロセス中にモデルの更新のセキュリティーを確保することができます。 QSDC プロトコルを使用すると、暗号鍵を必要とせずに、モデルの更新やその他の機密情報を安全に送信できます。 QSDC プロトコルは、量子状態や量子プロパティーを使用することにより、モデルの更新やその他の機密情報を安全に伝送することができ、FL システムに追加のセキュリティー層を提供します。 ブラインド・クォンタム・コンピューティング (BQC) は、クライアントが入力、出力、または計算自体を明らかにすることなく、リモート・クォンタム・サーバー上で計算を実行できるようにする技法です。 FL システムでは、BQC を使用して、モデル更新のプライバシーとセキュリティーを確保し、無許可アクセスや操作を防止することができます。
<!--
[68] サーバーでの作業では、サーバー集約時に BQC 方式が使用されます。これにより、サーバーのサード・パーティーによる盗難が回避され、データ・プライバシーが確保されます。 参照 [81] は、BQC を使用して FL の量子プロトコルを提示します。これは、VQC によるプライベート・シングル・パーティーの代行トレーニングのプロトコルを導入し、それを DP によるマルチパーティー分散学習に拡張します。 参照 [82] は、ローカル・モデル・パラメーターの高度にセキュアかつ効率的な集約を保証する、FL の量子シークレット共有プロトコルに基づく新しい量子セキュア集約スキームを提案します。 このスキームでは、qubit を使用してモデル・パラメーターを表します。これにより、半正直な攻撃者に開示されないようにプライベート・モデル・パラメーターが保護されます。 参照 [83] は、分散 QML に QSDC プロトコルを適用します。このプロトコルは、リモートの小規模光子量子計算プロセッサーを使用して、2 次元ベクトルを異なるクラスターに分類できます。 このようなプロトコルは安全であり、学習プロセスを傍受して妨害しようとする盗聴者を検出することができます。 [84] の研究では、リソース割り当てとルーティングポリシーを最適化するために FL システム内の QKD の階層アーキテクチャーを提案し、[85] の研究では、盗聴攻撃に対する公開鍵とモデルの暗号化を容易にするために QKD に基づく理想的なセキュリティーを備えた、量子セキュアなフェデレーテッド・エッジ・ラーニング (FEL) システムの階層アーキテクチャーを提案しています。 著者は、FEL の鍵とモデルを効率的に暗号化するために、確率的なリソース割り振りモデルを提案しています。 著者は、秘密鍵レートの要件と気象条件の不確実性の下でリソース割り振りのための最適なソリューションを実現するために、確率的なプログラミング・モデルを作成して解決します。 参照 [86] は、都市コンピューティングのための既存の ML アプローチが直面する課題について論じ、これらの課題に対処するためのハイブリッド FL アーキテクチャーを提案します。このアーキテクチャーは、FL を使用して、QKD によって個々のユーザーのデータのプライバシーとセキュリティーを確保しながら、エッジ・デバイスから生成された大量のデータを処理します。
-->

### 5.3. 頑強性ベースの SecQFL
これらのアプローチは、QSM、量子耐性 ML アルゴリズム、および量子耐性暗号技術を開発することにより、QFL モデルが量子攻撃、敵対攻撃、ハードウェアの欠陥、およびノイズに対して耐性を持つようにすることを目的としています。 これらのアプローチは、QSM、量子耐性 ML アルゴリズム、およびそのような課題に耐えることができる量子耐性暗号技術の開発に重点を置いています。

QEC は、QC デバイスのノイズ、ハードウェア・エラー、およびその他の欠陥の影響から量子モデルを保護します。 フォールト・トレラント QC や堅固なトレーニング方式などの量子耐性 ML アルゴリズムにより、敵対的攻撃やサイバー攻撃に対する量子モデルの耐性を高めることができます。 FL 設定では、QEC アルゴリズムと量子耐性 ML アルゴリズムを使用して、量子モデルの更新が正確かつ信頼性の高いものになるようにすることができます。 量子耐性暗号技術は、量子攻撃に耐えることができ、QC 機能を持つ敵に対してモデルを保護するために、ポスト・クォンタム暗号化と格子ベースの暗号化を取り込んでいます。 これらのアルゴリズムは、急速に進化する QC テクノロジーに直面する FL モデルの長期的な安全性を確保することを目的としています。
<!--
[69] および [70] では、ランダム量子回路 (RQC) が適用され、QCNN モデルおよびパラメーター保護の QTC モデルごとに回路設計がランダムに生成されます。 [73] で提案された方法は、もつれのレベルを制御し、深度間の干渉を軽減し、提案された精度に触発された正規化によって様々なチャンネル条件を処理します。 参照 [87] は、モバイル・エッジ・コンピューティング用の Lattice ベースの暗号化に基づくブロックチェーン・ベースの FL フレームワークを提案します。これは、ポスト・クォンタム暗号化 (PQC) を使用して、両者の身元が検証され、量子セキュリティーが確保されるようにすることを目的としています。 格子ベースの暗号化は、量子コンピューターの場合でさえ、妥当な時間内に十分な力で壊すことができないため、安全です。 [88] の論文では、QFL におけるビザンチン攻撃の課題について論じ、それらから保護するための解決策を提案しています。 著者は、古典的な分散学習と QFL の違いを比較し、クアントゥンフェFRB法 [75] のビザンチン問題を拡張し、理論的にこの問題を定義します。 以前に提案された 4 種類のビザンチントレラントアルゴリズムを量子バージョンに変更し、量子バージョンと同様の性能を示すためにシミュレーション実験を行う。 [89] の論文は、敵対的な攻撃に対して輸送システム分野のセキュリティーを強化するために、最適化された QFL (OQFL) フレームワークを提案しています。 著者は、量子動作の粒子群最適化手法を使用して、学習率、局所的エポック、グローバルエポックなど、FL のハイパーパラメーターを更新します。 提案された手法は、敵対的攻撃から防御するために、サイバー防御フレームワーク内で使用されます。
-->

## 6. 実装に関して
ベンチマークを効果的に実行するには、標準化されたデータ・セット、モデル・アーキテクチャー、評価メトリックを使用して、 QFL 研究領域の公平な比較を実現することが不可欠です。
<!--
実際には、パフォーマンス・ベンチマーキングは、可能性のあるプラットフォーム、さまざまなアプリケーション・ドメイン、データ・セット・タイプ、および評価メトリックを表す、実世界データ・セットと合成データ・セットの両方を使用して実行されることがよくあります。 

このセクションでは、既存の QFL 文献でこれらの側面を検討し、検討します。 これらのベンチマーキングの結果は、研究者や実務者が特定のユース・ケースに最も適した QFL 方式を特定し、さらなる調査を推進し、フィールドの全体的な状態を改善するのに役立ちます。
-->

### 6.1. QFLのためのプラットフォームとライブラリ
QFL プラットフォームは、QC 技法を FL システムに統合したり、QFL ソリューションを構築するためのツールを提供したりするために特別に設計されています。 これらのプラットフォームを使用することで、研究者と実務者は QFL の潜在的なメリットと課題を検討し、QFL 環境におけるより安全で効率的で正確な学習プロセスの開発を可能にします。

- [**Qiskit**](https://qiskit.org/) は、IBM が開発したオープン・ソースの QC ソフトウェア開発キット (SDK) です。 量子ハードウェアまたはシミュレーター上で量子回路を設計、シミュレート、および実行するための高次インターフェースを提供します。 Qiskit は、回路設計と最適化のための Terra、量子回路シミュレーションのための Aer、ノイズ・モデリングと誤り緩和のための Igner、量子アルゴリズムとアプリケーションのための Aqua など、複数のコンポーネントで構成されています。 Qiskit は、QFL アルゴリズムの開発に適しています。

- [**QuTiP**](http://qutip.org/) (Quantum Toolbox in Python の略) は、量子系をシミュレートするためのオープンソース Python ライブラリである。 閉鎖及び開放量子系のダイナミクスをシミュレートするために設計されており、量子力学、量子情報理論、量子光学を研究するための幅広いツールを提供しています。 QuTiP は、シュレーディンガー方程式、マスター方程式、その他の量子系ダイナミクスを解くための様々な数値ソルバーや、結果を視覚化・分析するためのツールを提供しています。

- [**Pennylane**](https://pennylane.ai/) は、 Xanadu が開発したオープンソースライブラリで、QC ハードウェアを使って QML、QOA、化学を可能にする。 IBM、Google、Rigetti、Xanadu 独自の光 QC デバイスなど、さまざまなプロバイダーの QC デバイスのための統一されたインターフェースを提供します。 Pennylane は、QML モデルを FL システムに統合するために使用でき、開発者が他の QC フレームワーク用のカスタム・プラグインを作成するのを可能にするプラグイン・システムをサポートしています。

- [**TensorFlow Quantum**](https://www.tensorflow.org/quantum) (TFQ) は、Google によって開発されたオープン・ソース・ライブラリーです。 QC 技法を TensorFlow と統合しています。 TFQ は、量子-古典ハイブリッド・モデルの開発を可能にし、QFL アルゴリズムの開発に使用することができます。 これは TensorFlow と Cirq の間のシームレスなインターフェースを提供し、ユーザーが TensorFlow の ML エコシステム内で Cirq の量子回路機能を利用できるようにします。

### 6.2. アプリケーション
QFL は、無線通信、NLP、都市コンピューティング、スマートシティ、交通、ヘルスケアなど、様々なアプリケーションや領域で有望な結果を示しています。 また、対応する QFL アプリケーション用のベンチマーク・データ・セットもいくつかあります。

- 無線通信エリアにおいて、QFL は、無線ネットワークにおけるデータ処理とモデルの最適化を向上させるとともに、ユーザーのデータ・プライバシーに関する懸念に対処し、計算負荷を分散させるために使用されます。

- FL 設定がでの NLP については、QFL は、NLP 領域で最初に言及された QFL 研究であるテキスト分類 [70] の量子優位性と事前学習済み BERT モデルを組み合わせることにより、NLP モデルのパフォーマンスと機能を向上させることができます。 また、QFL は、QCNN による自動音声認識のための分散アーキテクチャーに適用され、プライバシーに関する懸念に対処しています。

- 医療分野では、QFL は、医療分野における最初の QFL 研究として、同一独立分布でない (non-identical and independently distributed)  臨床データに使用されています。 このアプローチにより、データ交換の必要性が無くなり、機密性の高い医療データのプライバシーが維持されます。

- 輸送システムにおいて、QFL は、輸送システム分野における最初の QFL 作業である OQFL フレームワークを通じて、敵対的攻撃に対する輸送システムの安全性を向上させることができます。

- 都市コンピューティングとスマートシティにおいては、QFL はスマートシティ・アプリケーションのためにデジタルツインと統合されている。 「量子デジタルツイン」という概念が、QFL を用いた複雑な系をモデル化し、その精度と効率性を向上させるために導入されています。 さらに、QFL を使用して、プライバシーとセキュリティーを確保しながらエッジ・デバイスから生成された大量のデータを処理するハイブリッド FL アーキテクチャーが提案されています。

- これらのアプリケーションは、セキュリティーとプライバシーの強化から効率性とパフォーマンスの向上に至るまで、さまざまな課題に対処し、複数のドメインで改善を提供する QFL の可能性を実証します。 QC 技術の進歩に伴い、幅広い業界における QFL の飛躍的な進歩と応用が期待できます。

### 6.3. 評価指標
QFL 調査の評価メトリックを、表 IV に示すように、1) モデル・パフォーマンス関連、2) システム・パフォーマンス関連、3) 信頼できる AI 関連の 3 つのカテゴリーに分類します。

- モデル・パフォーマンス関連の評価指標  
QFL 研究におけるモデル・パフォーマンス関連の評価指標は、モデルの正確性と収束性の評価に重点を置いています。 これらの評価指標は、学習プロセスの有効性と、未見データでも一般化する能力が十分かを評価するのに役立ちます。 QFL の 正確性 (Accuracy) 評価指標は、トレーニングでの平均、検証 (validation) 、テスト・データにおける正確性、およびグローバル・モデルとローカル・モデルの正確性で構成されます。 収束性の評価指標は、モデルがどの程度良く学習し、最適解に到達しているかを測定しますが、モデルのトレーニング・プロセスを安定させ、優れたソリューションに収束させることが不可欠です。パラメトリック・ランドスケープ、損失、コスト関数値、目的関数値、テイラー損失、収束時間などがあります。

- システム・パフォーマンス関連の評価指標  
QFL におけるシステム・パフォーマンス関連の評価指標は、通信および計算効率、システム・スケーラビリティー、リソース使用率などの側面の評価に重点を置いています。 これらの評価指標は、リソースの使用と信頼性に関して QFL システムの全体的なパフォーマンスを評価するのに役立ちます。 効率性評価指標は、スループット、エポック数、CPU 実行時間、遅延を含む通信効率 (クライアントとサーバー間の通信プロセスの有効性を評価する) と計算効率 (計算時間を測定する) で構成されます。 システムのスケーラビリティーは、適応性のある動的なクライアントに対応し、パフォーマンスを維持するための QFL システムの能力を評価します。 リソース使用状況の評価指標は、学習プロセス中の計算、通信、メモリー、エネルギーなどのリソースの消費量の評価に重点を置いています。これには、パラメーター・メモリーおよびメモリー使用量、波長使用率、通信コスト、デプロイメント・コストが含まれます。

- 信頼できる AI 関連の評価指標  
信頼できる AI の評価指標は、QFL アプローチを評価するために広く実装されてはいません。 しかし、これらの評価指標を考慮する研究がいくつか現れてきています。
<!--
1 つの研究 [69] では、提案された手法の解釈可能性を評価するために、解釈可能なニューラル・サリエンシーが採用されています。 [73]、[75]、[81]、[82]、[88]、[89] の精度指標は、頑強性のパフォーマンスに適用されます。 [87] の作業では、攻撃検出率と累積報酬を使用して、潜在的な脅威に対する頑強性を測定します。
-->

## 7. 課題、オープンな機会、有望な将来の研究の方向性
QFL の分野はまだ未成熟であり、多くの課題に対処する必要があります。 これらには、量子ハードウェアの制限、ノイズと誤りの軽減、モデルとデータの不均質性、量子 FL と古典 FL の相互運用性、標準化とベンチマーキング、倫理と法的考慮事項が含まれます。 しかし、QC 技術の進展に伴い、この分野が急速に進化し、成熟することが期待できます。 今後数年で、QFL は、ますます相互接続が進む世界において複雑な問題に対処し、データ・プライバシーを保護するための重要なツールになる可能性があります。 研究者や実務者が QFL の可能性を探求し続ける中で、QC と FL の両方における新たな進展や飛躍的な進歩を注視し、この有望な分野の潜在能力を十分に実現することが重要になります。

### 量子ハードウェアの制限とリソース制約
量子ハードウェアはまだ開発の初期段階にあり、限定的な量子ビット、高水準のノイズ、比較的短いコヒーレンス時間などの課題があります。 これらの制限は、複雑な QFL アルゴリズムを実装するための課題となるため、量子ハードウェアの能力を向上させ、QFL をより実用的なものにするために継続的な研究開発を必要とします。 

- 限定的な量子ビット  
現在の量子コンピューターには、量子ビット数が限定的であるため、実行可能な量子回路のサイズと複雑さが制約されています。 QFL アルゴリズムをスケールアップするには、耐障害性の量子コンピューターの開発が不可欠です。 
- コヒーレンス・タイム  
量子コンピューターの量子状態は脆弱であり、コヒーレンス・タイムとして知られる短期間しか維持できません。 情報を大幅に失うことなく、より複雑な QFL アルゴリズムを実行するには、コヒーレンス・タイムを増やす必要があります。 
- 接続性  
現在の量子ハードウェアにおける限定的な量子ビット接続性は、量子アルゴリズムの効率に影響を与える可能性があります。 量子ビット接続性のようなハードウェアの制約を考慮した QFL アルゴリズムを設計すると、パフォーマンスを向上させることができます。

### 7.1. ノイズおよび誤りの軽減
量子システムは、本質的に、繊細な性質のためにノイズおよびエラーの影響を受けやすくなっています。 QFL アルゴリズムの精度と信頼性を向上させるには、効果的な誤り軽減手法が不可欠です。 より頑健な量子アルゴリズムの開発に加え、新しい誤りの訂正と緩和の方法を研究することで、これらの課題に対処することができます。 

- 誤り修正  
QFL アルゴリズムの信頼性を向上させるためには、低オーバーヘッドを維持しながらエラーを修正できる効率的で耐障害性のある QEC コードを開発することが重要です。 
- 誤り緩和手法  
ノイズ外挿法やエラー考慮トレーニングのような新しいエラー軽減手法は、 ノイズが存在する場合に QFL アルゴリズムのパフォーマンスを向上させることができます。

### 7.2. モデルおよびデータの不均質性
FL には、参加するデバイス間の不均一なモデルおよびデータ分布が含まれます。これは、QFL アルゴリズムのパフォーマンスに影響を与える可能性があります。 モデルとデータの不均質性に対処するには、そのような多様性を効果的に処理できる適応性と拡張性の高い量子アルゴリズムを開発する必要があります。 
- 適応的アルゴリズム  
さまざまなモデル・アーキテクチャーとデータ分布に適応できる QFL の開発は、FL 環境における不均質の問題に対処するために不可欠です。 
- 分散型最適化  
QFL の分散型最適化アルゴリズムの調査は、不均一な設定におけるアルゴリズムの収束の改善に役立つ可能性がある。

### 7.3. QFL と 古典的 FL の間の相互運用性
量子拡張した FL の古典的な FL 手法とのシームレスな統合は、広く採用される上で不可欠です。 
- ハイブリッド・アルゴリズム  
既存の FL システムに容易に統合できるハイブリッド量子古典的アルゴリズムへの研究は、量子拡張 FL へのスムーズな移行を促進することができます。 
- ミドルウェア・ソリューション  
古典システムと量子システムの間でシームレスな通信とデータ交換を可能にするミドルウェア・ソリューションを開発することで、2 つのパラダイムの間のギャップを埋めることができます。

### 7.4. 標準化とベンチマーキング
異なる QFL アルゴリズムの比較と評価を容易にするためには、標準化とベンチマークが不可欠です。 共用データセット、性能評価指標、およびベンチマーク・プロトコルを確立することは、研究者や実務者がさまざまな QFL 技法の有効性を評価し、それらの採用を促進するのに役立ちます。 
- ベンチマーク・データセット  
QFL の標準化データ・セットを確立することで、さまざまなアルゴリズムを公平に比較し、パフォーマンスの理解を深めることができます。 
- パフォーマンス・メトリック  
通信コスト、収束率、モデルの正確性など、QFL に適した性能評価指標を定義することは、QFL の有効性を評価するのに役立ちます。 
- ベンチマーク・プロトコル  
ハードウェア仕様やアルゴリズム構成を含む堅固なベンチマーク・プロトコルを開発することで、QFL アルゴリズムの信頼性と一貫性のある評価を確保できます。

### 7.5. 倫理と法的考慮
QFL システムを開発および導入する際には、全ての技術と同様、信頼性 (trustworthiness) を考慮する必要があります。 これらのテクノロジーを責任を持って使用するには、データ・プライバシー、セキュリティー、および規制要件への準拠を確保することが不可欠です。 さらに、研究者と実務者は、ML モデルにおける公平性、説明責任、透明性、および利害関係者の関与に QFL が与える潜在的な影響を考慮する必要があります。 
- データ・プライバシー  
QFL アルゴリズムがデータ・プライバシーを保護し、関連するデータ保護規則を順守するのを確保することは、責任あるテクノロジーの展開にとって不可欠です。 
- 公平性  
FL システムにおける公平性を評価するために量子手法を活用することにより、学習プロセスがネットワークに参加する様々なクライアントについてより公平で代表的なものであることを確保し、潜在的なバイアスを同定し軽減するのに役立ちます。 QFL アルゴリズムにおける公平性を向上させる方法 (リサンプリング手法、敵対的トレーニング、公平な最適化など) を開発することで、差別的な結果を防ぐことができます。 
- 説明責任と透明性  
QFL システムの責任ある開発、導入、および監視に関するガイドラインとベスト・プラクティスを確立することで、この分野の説明責任と透明性を確保することができます。 QFL アルゴリズムの解釈可能性 (XAI) 技法の研究は、意思決定プロセスの理解を深め、これらのシステムに対する信頼を促進することに貢献できます。 
- 利害関係者の関与  
政策立案者、業界パートナー、およびエンド・ユーザーを含む利害関係者との連携により、QFL の倫理的および法的影響についての認識を高め、責任あるガイドライン・規制の発展を促進することができます。

### 7.6. QFL の有望な将来研究の方向性
QFL の分野が進化し続ける中、これらのオープンな機会と今後の方向性は、より大きな AI パラダイムのために QC と FL の力を活用する斬新なソリューション、革新的なアプローチ、画期的なアプリケーションの追求において、研究者や実務者をガイドし、QFL の将来の方向性を期待します。

- パーソナライズされた QFL とは、ユーザーごとにパーソナライズされた方法 (スマートフォンや IoT デバイスなど) で QC 技法を FL に適用することを指します。 これにより、各ローカル・モデルはそのデバイスの特定のデータに合わせて調整でき、すべてのデバイスの集約された学習の恩恵を受けることができるため、パーソナライゼーションが可能になります。 量子設定では、このプロセスは、QML や QOA などの QC 固有の機能によって拡張される可能性があります。これにより、特にデータ・プライバシーと効率性が最優先の分野である医療や金融などの分野で、より効果的な学習結果やユーザー・エクスペリエンスの向上につながる可能性があります。 
- 量子フェデレーテッド・グラフ・ニューラル・ネットワーク (QFGNN) 分割は、 QFL のグラフ・ニューラル・ネットワーク (GNN) への応用です。 最大カット問題は、コンピューター・サイエンスおよび組み合わせ最適化においてよく知られる問題で、その目標は、グラフのノードを 2 つのグループに分割して、グループ間を交差するエッジの重みの合計を最大化することです。 QFGNN の文脈では、これには、FL システムにおけるノード選択、QFGNN の接続性の判定、グラフ構造の接続を維持しつつ冗長エッジの削減などの実用的な応用の可能性があります。 
- 量子に基づく圧縮および量子化 (quantization) の手法は、FL システムにおけるモデル更新のサイズと全体的な通信オーバーヘッドの削減に役立ちます。 QFL は、QDE を活用してモデル更新を圧縮し、古典 FL 方式よりもコンパクトに情報を送信することができます。 これにより、モデル更新の効率化と収束の高速化が可能になります。 さらに、QFL は、量子にインスパイアされた手法を使って、モデル更新のサイズを削減するためにモデル・パラメーターの計算精度を低下させて、モデルの量子化を効率的に行うことができます。これにより、モデル性能を犠牲にすることなく、通信オーバーヘッドを削減し、FL システムの効率を向上させることができます。
- GPT-3 や GPT-4 などの大規模言語モデルは、広範な一般知識を活用できる強力な道具立てを備えています。 したがって、これらのモデルは、コンテキストに関連した応答を生成するためのコンテキスト性を識別するのに優れています。 それにもかかわらず、これらの先駆的モデルは、細心の注意とさらなる探索を必要とする特定の課題を提示しています。 追加研究のための重要な領域の熟成は、言語モデルのスケール拡張性と効率性を強化する際の QFL の潜在的な役割に関するもので、特に量子 NLP の領域においてそうである。 これには、QC と、ブロックチェーンやエッジ・コンピューティングなどの他の急展開するテクノロジーとの間の複雑な相互作用の調査と並んで、言語モデリング用に調整された革新的な QFL アルゴリズムの考案が含まれます。 これらの技術を融合させることで、大規模言語モデルの分野で前例のない進歩が実現され、コンピュータ言語学の新しい時代への道が開かれる可能性があります。

## 8. 結び
このレビューは、Ren et al. (2023) の内容を中心に、 QFLの原理、技法、および新興アプリケーションについて包括的な理解を提供し、 QFL に興味を持っている人の手引きとなることを目的にまとめました。

## 9. 参考文献
[1] [Ren et al.(2023) "Towards Quantum Federated Learning", arXiv](https://arxiv.org/abs/2306.09912)

[2] Q. Yang, Y. Liu, T. Chen, and Y. Tong, “Federated machine learning: Concept and applications,” ACM Transactions on Intelligent Systems and Technology (TIST), vol. 10, no. 2, pp. 1–19, 2019.

[3] S. Y.-C. Chen and S. Yoo, “Federated quantum machine learning,” Entropy, vol. 23, no. 4, p. 460, 2021.

[4] H. T. Larasati, M. Firdaus, and H. Kim, “Quantum Federated Learning: Remarks and Challenges,” in 2022 IEEE 9th International Conference on Cyber Security and Cloud Computing (CSCloud)/2022 IEEE 8th International Conference on Edge Computing and Scalable Cloud (EdgeCom), IEEE, 2022, pp. 1–5.

[5] Y. Kwak et al., “Quantum distributed deep learning architectures: Models, discussions, and applications,” ICT Express, 2022.

[6] [Gurung et al. (2023) "Quantum Federated Learning: Analysis, Design and Implementation Challenges", arXiv](https://arxiv.org/abs/2306.15708)

[7] [Zhao (2023) "Non-IID Quantum Federated Learning with One-shot Communication Complexity", arXiv](https://arxiv.org/abs/2209.00768)

[8] [Zhang et al. (2022) "TensorCircuit: a Quantum Software Framework for the NISQ Era", arXiv](https://arxiv.org/abs/2205.10091)

## 10. QFLの実装サンプルコード
H. Zhao, “Non-IID quantum federated learning with one-shot. communication complexity,” Quantum Machine Intelligence, vol. 5, no. 1, p.3, 2023.　の論文の著者たちの実装について、以下のJupyter Notebookで紹介いたします：

- [5a_QFL-Sample#1-1_Centralized_Case.ipynb](https://github.com/wg-quantum/2023-b-07-a/blob/main/src/team_a/5a_QFL-Sample%231-1_Centralized_Case.ipynb)  
  上記論文の数値実験のうち、qFedAvgとの対照実験用のNotebookを実行したもの。

- [5a_QFL-Sample#1-2_qFedAvg.ipynb](https://github.com/wg-quantum/2023-b-07-a/blob/main/src/team_a/5a_QFL-Sample%231-2_qFedAvg.ipynb)  
  上記論文の数値実験のうち、量子連合平均法 (qFedAvg) によるHFL型QFLのNotebookを実行したもの。

<!--
連合学習とは、セキュアなデータ・プライバシーを持つ複数のクライアントからの分散データに基づく機械学習タスクのことです。 最近の研究では、量子アルゴリズムを利用してパフォーマンスを向上させることができることが示されています。 ただし、クライアントのデータが独立同分布でない (non-IID) 場合、従来の連合アルゴリズムのパフォーマンスが低下することが知られています。 この研究では、理論的分析と数値的分析の両方を用いた量子統合学習における非 IID 問題を検討します。 さらに、グローバル量子チャネルは、局所密度推定量の助けを借りて、各クライアントによって訓練されたローカルチャネルに正確に分解できることを証明します。 この観測により、1 回限りの通信の複雑さを伴う非 IID データに関する量子連合学習のための一般的なフレームワークが実現します。 数値シミュレーションは、非 IID の設定で、提案されたアルゴリズムが従来のアルゴリズムよりも大幅に優れていることを示しています。
-->