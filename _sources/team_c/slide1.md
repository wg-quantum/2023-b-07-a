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

---

## 回答1

### Z軸の周りを回転することを位相回転（Phase flip）という

3. Zゲート
4. Tゲート
5. ゲート

---

## 問題２

### ビット反転するゲートは？

1. Xゲート
2. Zゲート
3. Tゲート
4. Sゲート

---
## 回答2

### パウリX行列をつかうと|0>が|1>に|1>が|0>になる。これをビット反転（bit flip）という.

1. Xゲート

---

## 問題３

### 下記を実行すると、量子状態はどうなりますか1？

![100%](./image/3.png)

---

## 回答３

### アダマールゲートのあとCCXゲートを通している事を確認してください

Bell状態になります

---

## 問題４

### 下記を実行すると、量子状態はどうなりますか2？

![100%](./image/4.png)

---

## 回答４

### 
GHZ状態になります

---

## 問題５

### 下記と等価なゲートは1？

![100%](./image/5.png)

---

## 回答５

### 

Zゲートになります

---

## 問題６

### 下記と等価なゲートは2？

![100%](./image/6.png)

---

## 回答６

###

Xゲートになります

---

## 問題７

### Sゲートのフェーズの値は？

1. π/2
2. π/4
3. π/8
4. π

---

## 回答７

### 

1. π/2

---

## 問題８

### Tゲートのフェーズの値は？

- π/2
- π/4
- π/8
- π

---

## 回答8

### 

1. π/4



---

## 問題９

### QuantumCircuit　正しくない記述は？

1. QuantumCircuit(QuantumRegister(4))
2. QuantumCircuit(QuantumRegister(4), ClassicalRegister(3))
3. QuantumCircuit(QuantumRegister(4, 'qr0'), QuantumRegister(2, 'qr1'))
4. QuantumCircuit（4,4)
5. QuantumCircuit（cr,qr)
6. qr = QuantumRegister(2)
  cr = ClassicalRegister(2)
  qc = QuantumCircuit(cr[0:2],qr[0:2])

---

## 回答９

### 

すべて正しい記述です。



---

## 問題10

### Measure　正しくない記述は？

1. circuit = QuantumCircuit(2, 2)
  circuit.measure([0,1], [0,1])
2. circuit = QuantumCircuit(2, 2)
  circuit.measure(0, 0)
  circuit.measure(1, 1)
3. qreg = QuantumRegister(2, "qreg")
  creg = ClassicalRegister(2, "creg")
  circuit = QuantumCircuit(qreg, creg)
  circuit.measure(qreg, creg)
4. circuit = QuantumCircuit(qreg, creg)
  circuit.measure(qreg[0], creg[0])

---
問題10 Measure　正しくない記述は？
