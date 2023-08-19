---
marp: true
theme: test
footer: "**2023-B-07-a**"
paginate: true 

---
<!--
class: title
_backgroundColor: orange
-->

# 想定問題集

---
<!--
class: slides
-->

## 問題１

### 位相回転するゲートは？

1. Xゲート
2. Yゲート
3. Zゲート
4. Tゲート
5. Sゲート

<details>
<summary>答えはこちら</summary>
Z軸の周りを回転することを位相回転（Phase flip）という

3. Zゲート
4. Tゲート
5. ゲート
</details>

---

## 問題２

### ビット反転するゲートは？

1. Xゲート
2. Zゲート
3. Tゲート
4. Sゲート

<details>
<summary>答えはこちら</summary>
パウリX行列をつかうと|0>が|1>に|1>が|0>になる。これをビット反転（bit flip）という.

1. Xゲート

</details>

---

## 問題３

### 下記を実行すると、量子状態はどうなりますか1？

![問題画像](./image/question/q3.png)

<details>
<summary>答えはこちら</summary>
アダマールゲートのあとCCXゲートを通している事を確認してください

Bell状態になります

</details>


---

## 問題４

### 下記を実行すると、量子状態はどうなりますか2？

![問題画像](./image/question/q4.png)

<details>
<summary>答えはこちら</summary>

GHZ状態になります

</details>

---

## 問題５

### 下記と等価なゲートは1？

![問題画像](./image/question/q5.png)

<details>
<summary>答えはこちら</summary>
図と同じゲートはZゲートになります

</details>

---

## 問題６

### 下記と等価なゲートは2？

![問題画像](./image/question/q6.png)

<details>
<summary>答えはこちら</summary>
図と同じゲートはXゲートになります

</details>


---

## 問題７

### Sゲートのフェーズの値は？

1. π/2
2. π/4
3. π/8
4. π

<details>
<summary>答えはこちら</summary>
1. π/2

</details>


---

## 問題８

### Tゲートのフェーズの値は？

1. π/2
2. π/4
3. π/8
4. π

<details>
<summary>答えはこちら</summary>
2. π/4

</details>

---

## 問題９

### QuantumCircuit　正しくない記述は？

1. QuantumCircuit(QuantumRegister(4))
2. QuantumCircuit(QuantumRegister(4), ClassicalRegister(3))
3. QuantumCircuit(QuantumRegister(4, 'qr0'), QuantumRegister(2, 'qr1'))
4. QuantumCircuit（4,4)
5. QuantumCircuit（cr,qr)
6. qr = QuantumRegister(2)<br>
  cr = ClassicalRegister(2)<br>
  qc = QuantumCircuit(cr[0:2],qr[0:2])

<details>
<summary>答えはこちら</summary>
すべて正しい記述です。

</details>


---

## 問題10

### Measure　正しくない記述は？

1. circuit = QuantumCircuit(2, 2)<br>
  circuit.measure([0,1], [0,1])
2. circuit = QuantumCircuit(2, 2)<br>
  circuit.measure(0, 0)<br>
  circuit.measure(1, 1)
3. qreg = QuantumRegister(2, "qreg")<br>
  creg = ClassicalRegister(2, "creg")<br>
  circuit = QuantumCircuit(qreg, creg)<br>
  circuit.measure(qreg, creg)
4. circuit = QuantumCircuit(qreg, creg)<br>
  circuit.measure(qreg[0], creg[0])

<details>
<summary>答えはこちら</summary>

回答作成中です

</details>

---

## 問題11

### plot_histogram()のオプションで、ラベルを追加するのは？

1. legend
2. short
3. number_to_keep
4. bar_labels
<details>
<summary>答えはこちら</summary>
ラベルは1.legendオプションで追加します。<br>
ラベルに表記する文字は、リストとして渡す必要があります。

![問題画像](./image/question/q11.png)

</details>

---

## 問題12

### plot_histogram()のオプションで、バーの色を変更するのは？

1. legend
2. color
3. number_to_keep
4. bar_labels
<details>
<summary>答えはこちら</summary>
ラベルは2.colorオプションで変更します。<br>

</details>

---


## 問題13

### 以下のコードで出力されるのはどちらですか？
qc = QuantumCircuit(2)<br>
qc.h(0)<br>
qc.cx(0, 1)<br>
<br>
state = DensityMatrix(qc)<br>
plot_state_city(state)<br>


1. [問題画像](./image/question/q13_1.png)


2. [問題画像](./image/question/q13_2.png)
<details>
<summary>答えはこちら</summary>

1.が正解です。bell状態をplot_state_cityで表示したものです。
2,は<br>
qc.h(0)<br>
qc.x(0)<br>
qc.cx(0, 1)<br>
の状態です

</details>



---
以下テンプレート
改行は\#<br>

---

## 問題??

### 問題文text

1. 
2. 
3. 
4. 
<details>
<summary>答えはこちら</summary>

回答text

</details>

