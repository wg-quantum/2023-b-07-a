# 受験時の注意点

<<<<<<< Team_C
## アセスメントテストを受験する際

- 3000円で受験が可能
- 問題は60問　時間は90分で本試験と同じ
- 出題パターンは何回受けても同一。同じ問題が出題される。
- 本試験とは違い、試験管による監督はないため、インターネットが利用できればいつでも受けれる。
- 本試験で出題される問題がそのまま出題されるわけではないが、出題傾向が得られるため、受験することがおすすめ。

## 本試験について

### 1. 前提(失敗談)

- 試験の受験ポリシーに下記の記載がある <br>【同一試験番号の受験に際し、1回目のご受験が不合格であった場合、30日の間に2回目のご受験が可能】
- これは、「1回目が不合格でも、2回目の費用を払わずに、30日以内であれば、無料で再試験が受けれる」と受け止める事ができそうだが、大きな間違い！
- 以下が正しい (以下、受験事務局からの説明を引用) <br> 
    再受験は、30日間に2回までとなっております。
    1回目と3回目/ 2回目と4回目...のご受験の間隔を、30日空けて頂く必要がございます。
    例）1回目の受験が2月1日の場合、3回目の受験の最短可能日は3月1日
    7月21日にご受験済みの場合は、2回目はすぐ受験できます。（30日以上あけていただいてもご受験は可能です。）
    ただし、3回目の受験最短可能日は、7月21日から30日後にあたる8月21日となります。
    4回目の受験最短可能日は、2回目の受験日から30日後になります。
    尚、ご予約の際には、上記、再受験ポリシーに関係なく、ご予約毎に試験料金が発生致します。

### 2. 受験にあたって、環境など

- 受験料はIBM社員でなければ、２万円かかる。
- 受験には予約が必要。日曜日は予約できない。
- オンラインで30分前にチェックインが可能になる。環境まわりのトラブルありそう（実際あった）なので早めに入るの推奨。ギリギリのチェックインは危ない。下記事例
    - スマホでのチェックイン作業に10分ぐらいかかる。特に、自撮り写真が必要だが、自撮りに慣れておらず、なかなか写真取れない。
    - 事前に環境テストしていたが、チェックイン後の環境確認で試験官から「（試験管のPCからは）カメラに映像が写ってないのでやり直ししてください（自身の画面上は写っているのに）」といわれ焦る。この時点で、試験開始前の16分前だが、「再起動してください」といわれ、チャットを切られる。最悪、間に合わなくて試験できなくね？と非常に焦る。（時間に間に合わないと、受験料無駄になるよとの注意書きあり）
    - あわててPCの再起動、アプリ起動して再接続し、今度はOKになった。
- 不正防止のため、強めの制御がかかるアプリケーションをインストールする必要があり、会社のNW、PCでやるのは良くない（説明にも書いてあるんだけど） 
- 場所が近ければ、リアル試験会場での受験が確実
- 机の周囲の写真を撮らされるので、事前の掃除などは必要。恥ずかしいものは避ける。
- 腕時計も外せといわれ、ヘッドセットも利用できない。（最初していた場合は、置いた場所を確認させられる）
- 会社でやったため、社員にしゃべりかけられたらＮＧの中、ドキドキしながらになってしまった。

### 3. 試験の内容について

- コーディングのお作法問題が主。
- 計算問題は多くない
- 毎回問題が同じかは謎。多分、数百問の候補中から、６0問が都度抽出し出されている気がする。※サンプルテスト、アセスメントテストで出された問題は、あまり見当たらず・・・（数問近いのはあった気がする）
- 出る順番に一貫性はない
- 時間はあまりまくって、集中力がきれた。1週目40分 2週目フラグ立てたやつ20分 3週目20分
- 経過時間と、何問目かは画面にでているので、時計は必要ない。
- 下記出題パターン
    1. 4つの選択肢で、どのコーディングが正解？（微妙に文法が違う選択肢から、正しいコードを選択）    
    2. このゲート通したときの結果は？（選択肢パターンとして、ブロッホ球、vector、Unity、Multivectorなど様々。)
    3. この条件のゲートってどれ？（X Y Z S T などから、○○の時、BetWeen |+>and |-> unchange）
    4. コーディング並べ変え問題（少ないが、１問ぐらい出題される）
    5. ヒストグラム表示、executeなどのオプション問題（少ないが確実にある）
    6. 英文を理解しないと解けない問題がある・・・（Barrierはどういった機能を有しているか？説明している文章を選べ・・みたいな）
    7. Visualizetionの問題も多い
    8. こんなコードあったっけ？というのもでるので、出題範囲のコードはすべて学習しておく必要がある　<br>
    .compose() <br>
    plot_state_qsphere(state) plot_state_city(state) <br>
    plot_state_hinton(state) <br>
    9. 意外に出る.initialize 
    10. Def ループ文 などもでて、ノーマークでした。
- 虎の巻の実装解説もよんでおくと、広く学習が可能。
    quantum-education-2022/2_basic/2-2_basic_textbook_11-4-1-2/bible_4-1/Dev.pdf at main · wg-quantum/quantum-education-2022 (github.com)
