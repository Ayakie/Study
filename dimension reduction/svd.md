---
marp: true
theme: gaia
paginate: true
footer: 'About Singular Value Decomposition'
---

<!-- _class: lead -->
# 特異値分解とは
# Singular Value Decomposition
---

### とその前に、固有値分解を覚えてますか

正方行列$A$が、対角行列$\varLambda$と固有ベクトルからなる行列$V$でもって
$$
  A = V\varLambda V^{-1}
$$

で表すことを、 **固有値分解**または**行列の対角化**という。

<br>

- 正方行列とは：行と列の数が等しいn×nの行列
- 対角行列とは：対角成分以外全て０な行列

---

### どうやって求めるんだっけ

**$A$の固有値問題**を解く。

例) 行列 $A = \left(
    \begin{array}{cccc}
      5 & -4  \\
      -1 & 2\\
    \end{array}
  \right)$を固有値分解せよ

解) 
$$ \left(
    \begin{array}{cccc}
      5 & -4  \\
      -1 & 2\\
    \end{array} 
  \right)\vec{x} = \lambda \vec{x} \hArr \left(
    \begin{array}{cccc}
      5-\lambda & -4  \\
      -1 & 2-\lambda\\
    \end{array}
  \right)\vec{x}=\vec{0}
$$
をみたす固有値$\lambda$と固有ベクトル$\vec{x}$を求める

---
これを求めるには、固有方程式
$$
|A-\lambda E| =0$$
を解けば良い.

$$\begin{vmatrix}
   5-\lambda & -4 \\
   -1 & 2-\lambda
\end{vmatrix}=0 \hArr \lambda ^2 -7\lambda + 6 = 0
$$
これを解くと、$\lambda=1, 6$となる.
求めた$\lambda$を、前ページの式に代入する.

---
$(ⅰ) \lambda =1 の時$
$$\left(
    \begin{array}{cccc}
      4 & -4  \\
      -1 & 1\\
    \end{array}
  \right)\left(
    \begin{array}{c}
      x_1 \\
      x_2
    \end{array}
  \right)
  = \vec{0}
  \hArr
  \left(
    \begin{array}{cccc}
      1 & -1  \\
      0 & 0\\
    \end{array}
  \right)\left(
    \begin{array}{c}
      x_1 \\
      x_2
    \end{array}
  \right)
  = \vec{0}
$$
より、$\vec{x_1}= c\dbinom 1 1$と求まる. 同様にして$\lambda=6$の時の$\vec{x_2}$も求めると、$\vec{x_2} = c\left(
    \begin{array}{c}
      4 \\
      -1 \\
    \end{array}
  \right)$となる. 
この２つの固有ベクトル$\vec{x}$と、固有値$\lambda$を並べることで、
$$
 A=V\left(
    \begin{array}{cccc}
      1 & 0  \\
      0 & 6\\
    \end{array}
  \right)V^{-1}
$$

---


ただし、$V=\left(
    \begin{array}{cccc}
      1 & 4  \\
      1 & -1\\
    \end{array}
  \right)$である. (逆行列$V^{-1}$は面倒なので省略)
<br>

# 重要なのは$A$が**正方行列**であること
そのおかげで、$V, \varLambda$はどちらもn×nでいい感じに対角化できている

<br>

あと、当たり前だけど$V$が**正則行列**(逆行列$V^{-1}$が存在する)も重要


---
(やっと本題)
<br>
<br>

# じゃあ$A$がm×nの**長方行列**の場合は？
---

(m×n)の行列$A$は、２つの直交行列$U(m×m)$と$V(n×n)$および、対角行列$\Sigma$(m×n)でもって
$$
A = U\Sigma V^{-1}
$$
で表すことができる。これを、**特異値分解**という。
ここで、$U = (\vec{u_1}, \vec{u_2}, \cdots, \vec{u_m})$,          $\Sigma=\left(
    \begin{array}{cccc}
      \sigma_1 &  & \ldots &  \\
       & \sigma_2 &  & \omicron \\
      \omicron &  & \ddots & \\
       &  & \ldots & \sigma_{mn}
    \end{array}
  \right)$
  $V = (\vec{v_1}, \vec{v_2}, \cdots, \vec{v_n})$と表せる

---

- (m×m)と(m×n)の行列をかけると何行何列の行列になるか、思い出してみる
→　外側の数だけ残るよ

- 直交行列$V$とは、$VV^{T}=V^{T}V = E$, すなわち $V^{-1}=V^{T}$を満たすベクトル

- $\vec{u}$および$\vec{v}$は$A$の**特異ベクトル**, $\sigma$は**特異値**という
- $U$を**左特異値**, $V$を**右特異値**ということがある
- $\sigma_1>\sigma_2>...>\sigma_{mn}$であり、$\vec{u}, \vec{v}$は単位ベクトルである

---
### どうやって求める？

$AA^T$の固有値問題を解けば、$U$(特異ベクトル)と$\Sigma$(特異値)が求まる
$$
AA^T=(U \Sigma V^T)(V\Sigma ^T U^T)
=U\Sigma \Sigma U^T
$$
<br>

- 対角行列は転置しても値が等しくなる
- 直交行列の定義$V^T=V^{-1}$より、$V^TV=E$

<br>
なんか見たことあるような式だね

---

逆に、$A^TA$の固有値問題を解けば今度は、$V$と$\Sigma$が求まる.

ただ、この場合、$U$が前ページで求まるので、これを利用するとスマートに解ける

$$
A^TU = V\Sigma
$$
実は$A^TU$を計算して、それを単位ベクトルに直すだけで$V$が求まる...

$\Sigma$は特異値$\fallingdotseq$固有ベクトルであり、単位ベクトルにかける長さを表している, つまり大きさ1の向き(特異ベクトル)のみ表せば$V$が求まることになる
参考: MITの授業 https://youtu.be/cOUTpqlX-Xs

---

## 次元削減

特異値分解により、$A$は次のように表される
$$
A=\vec{u_1}\sigma_1\vec{v_1}^T+\vec{u_2}\sigma_2\vec{v_2}^T+...+\vec{u_k}\sigma_k\vec{v_k}^T+ \vec{u}_{k+1}\sigma_{k+1}\vec{v}_{k+1}^T...+\vec{u_n}\sigma_n\vec{v_n}^T 
$$

- $\sigma_1>\sigma_2>...>\sigma_{n}$だから、$\sigma_1$が最も大きい, すなわち$A$を表すのに最も重要な値であると言える
- ある定数k+1以降は、微細な値であると考え、切り捨てることができる
→ **k番目までの項を採用して、新たな行列$\tilde{A}$を作ることができる**

---
# 補足1
1. 正則行列: regular matrix あるいは **non-singular matrics**(非特異行列) **inversible matrics**(可逆行列)
定義: $AB=BA=E$　を満たすn次正方行列Bが存在する時、BをAの**逆行列**といい、Aは正則であるという.
2. 直交行列： orthogonal matrix
3. 対角行列：diagonal matrix
4. 特異ベクトル：singular vectors
5. 固有ベクトル：eigen vectors
6. 転置行列：transpose

---

# 補足2

#### PCA(Priciple Component Analysis)：主成分分析との違い
分散共分散行列(variamce-covariance matrix)
$$\sigma_{jk} = \frac{1}{n}\sum_{i=0}^{n}(x_j^{(i)}-\mu_j)(x_i^{(i)}-\mu_k)$$
を固有値分解し、k次元までの項目を抽出したもの

※ 分散共分散行列は、相関行列みたいなもの.

---
<!-- _class: lead -->
### 結論としては、ほとんど同じ
[（Qiita) PCAとSVDの関連について](https://qiita.com/horiem/items/71380db4b659fb9307b4)
