# Nhóm là gì?

Xét tập hợp $$G$$ gồm các phần tử và phép toán 2 ngôi $$\star$$ trên $$G$$:

$$\begin{align*}G \times & G & \rightarrow \, & G \\ a  \times & b & \rightarrow \, & a \star b\end{align*}$$ (phép toán đóng trên $$G$$).

Một **nhóm** $$(G, \star)$$ phải thỏa mãn:

* Tính đóng (Closure): $$\forall a, b \in G$$, $$a \star b \in G$$​.
* Tồn tại phần tử đơn vị (Identity Law): tồn tại phần tử $$e \in G$$ sao cho, với mọi $$g \in G$$ thì $$g \star e = e \star g = g$$. Ta còn có thể ký hiệu phần tử đơn vị của nhóm $$G$$ là $$e_G$$.
* Tồn tại phần tử nghịch đảo (Inverse Law): với mọi $$g \in G$$, tồn tại $$g' \in G$$ sao cho $$g \star g' = g' \star g = e$$. Ta còn có thể ký hiệu nghịch đảo của phần tử $$g$$ là $$g^{-1}$$.
* Tính kết hợp (Associative Law): với mọi $$a, b, c \in G$$​ thì $$(a \star b) \star c = a \star (b \star c)$$​.

**Lưu ý**: trong định nghĩa của nhóm **không có tính giao hoán**. Nghĩa là không phải lúc nào chúng ta cũng có đẳng thức $$\sigma \star \tau = \tau \star \sigma$$​ với mọi $$\sigma, \tau$$​.

Nếu nhóm có tính giao hoán thì được gọi là **nhóm Abel**. Nghĩa là:

* Với mọi $$a, b \in G$$​ thì $$a \star b = b \star a$$​.

Ví dụ về nhóm

1. Xét nhóm $$G=(\mathbb{Z}, +)$$​ gồm các số nguyên và phép cộng 2 số nguyên
   * Tính đóng: dễ thấy phép cộng 2 số nguyên cũng là số nguyên.
   * Tính kết hợp: với mọi $$a, b, c \in \mathbb{Z}$$, ta đã quá quen thuộc $$(a + b) + c = a + (b + c)$$
   * Phần tử đơn vị là 0 vì $$\forall a \in \mathbb{Z}$$, $$a + 0 = 0 + a = a$$.
   * Phần tử nghịch đảo của $$a \in \mathbb{Z}$$ là $$-a$$, vì $$a + (-a) = (-a) + a = 0$$.
   * Nhóm này có tính **giao hoán**, vì $$\forall a, b \in \mathbb{Z}$$, $$a + b = b + a$$.&#x20;
2. Xét nhóm $$Q=(\mathbb{Q}^*, \times)$$​ gồm các số hữu tỷ khác 0 và phép nhân 2 số hữu tỷ.
   * Tính đóng: phép nhân 2 số hữu tỷ khác 0 cho kết quả cũng là số hữu tỷ khác 0.
   * Tính kết hợp: với mọi $$a, b, c \in \mathbb{Q}^*$$ thì $$(a \times b) \times c = a \times (b \times c)$$​.
   * Phần tử đơn vị là 1 vì với mọi $$a \in \mathbb{Q}^*$$​ thì $$a \times 1 = 1 \times a = a$$​.
   * Phần tử nghịch đảo của $$a \in \mathbb{Q}^*$$​ là $$\frac{1}{a}$$.
   * Nhóm $$Q$$​ có tính giao hoán.

Một số tính chất của nhóm:

* Trong nhóm có duy nhất một phần tử đơn vị. Nói cách khác, nếu $$e$$ và $$e'$$ là hai phần tử đơn vị của nhóm thì $$e=e'$$.
* Với mọi $$g \in G$$, tồn tại duy nhất một phần tử nghịch đảo của $$g$$.
* Nếu $$g^{-1}$$ là nghịch đảo của $$g$$ thì $$(g^{-1})^{-1} = g$$
* Với $$a$$, $$b \in G$$, $$(ab)^{-1} = b^{-1} a^{-1}$$.
* Phép lũy thừa: ta thực hiện toán tử $$k$$ lần $$g \star g \star \cdots \star g = g^k$$
