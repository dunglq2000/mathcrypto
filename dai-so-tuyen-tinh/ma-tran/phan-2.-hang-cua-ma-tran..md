# Định thức và hạng của ma trận

Trong các bài viết của mình thì vector sẽ được ký hiệu bởi chữ thường in đậm (ví dụ $$\bm{v},\ \bm{x}, \cdots$$)​; ma trận sẽ được ký hiệu bởi chữ hoa in đậm (ví dụ $$\bm{A},\ \bm{B}, \cdots$$​); các đại lượng vô hướng (số) được ký hiệu bởi chữ thường không in đậm (ví dụ $$x_1,\ N,\ t, \cdots$$).

Ví dụ vector $$\bm{a} = (x_1, x_2, \cdots, x_n)$$​ trong đó $$x_i$$​ là các tọa độ.

Ví dụ ma trận $$\bm{A} = \begin{pmatrix}x_{11} & x_{12} & \cdots & x_{1n} \\ x_{21} & x_{22} & \cdots & x_{2n} \\ \cdots & \cdots & \cdots & \cdots \\ x_{n1} & x_{n2} & \cdots & x_{nn}\end{pmatrix}$$

### 1. Định thức của ma trận (Determinant)

**Định nghĩa**. Cho tập hợp $$A = \{1, 2, \cdots, n\}$$ và xét hoán vị $$\sigma$$ trên ​. Ta gọi 2 phần tử $$i$$​ và $$j$$​ tạo thành **nghịch thế** (inversion) nếu $$i < j$$​ và $$\sigma(i) > \sigma(j)$$.

Đặt $$\sigma = \{k_1, k_2, \cdots, k_n\}$$​ là một hoán vị của $$A$$​. Ta ký hiệu $$P\{k_1, k_2, \cdots, k_n\}$$ là số lượng nghịch thế của $$\sigma$$​ và đặt $$(-1)^{P\{k_1, k_2, \cdots, k_n\}} = sign\{k_1, k_2, \cdots, k_n\}$$.​

Ví dụ với $$n=4$$​, $$A = \{1, 2, 3, 4\}$$​. Xét hoán vị $$\sigma = \{4, 2, 1, 3\}$$​.

Ta nhận thấy các cặp nghịch thế $$(4, 2),\ (4, 1),\ (4, 3),\ (2, 1)$$​ gồm 4 cặp nghịch thế. Vậy $$P\{4, 2, 1, 3\} = 4$$ và $$sign\{4, 2, 1, 3\}=(-1)^4=1$$​.

**Định nghĩa**. Khi đó định thức của ma trận $$\bm{A} = \begin{pmatrix}a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \cdots & \cdots & \cdots & \cdots \\ a_{n1} & a_{n2} & \cdots & a_{nn}\end{pmatrix}$$​ được định nghĩa là:

$$\det(\bm{A})=\displaystyle{\sum_{(i_1, i_2, \cdots, i_n)} a_{1, i_1} \cdot a_{2, i_2} \cdot a_{n, i_n} \cdot sign\{i_1, i_2, \cdots, i_n\}}$$​ với mọi hoán vị $$(i_1, i_2, \cdots, i_n)$$ của $$(1, 2, \cdots, n)$$. Như vậy có $$n!$$​ phần tử cho tổng trên.

Ví dụ: tính định thức ma trận $$\bm{A}=\begin{pmatrix}1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9\end{pmatrix}$$​.

Xét hoán vị $$\sigma_1 = \{1, 2, 3\}$$​. Khi đó $$P\{1, 2, 3\}=0$$​, $$a_{11} \cdot a_{22} \cdot a_{33} \cdot (-1)^0 = 1 \cdot 5 \cdot 9 \cdot 1 = 45$$​.

Xét hoán vị $$\sigma_2 = \{1, 3, 2\}$$​. Khi đó $$P\{1, 3, 2\} = 1$$​, $$a_{11} \cdot a_{23} \cdot a_{32} \cdot (-1)^1 = 1 \cdot 6 \cdot 8 \cdot (-1) = -48$$.

Xét hoán vị $$\sigma_3 = \{2, 1, 3\}$$​. Khi đó $$P\{2,1,3\}=1$$​, $$a_{12} \cdot a_{21} \cdot a_{33} \cdot (-1)^1 = 2 \cdot 4 \cdot 9 \cdot (-1) = -72$$.

Xét hoán vị $$\sigma_4=\{2,3,1\}$$. Khi đó $$P\{2, 3, 1\} = 2$$​, $$a_{12} \cdot a_{23} \cdot a_{31} \cdot (-1)^2 = 2 \cdot 6 \cdot 7 \cdot 1 = 84$$​.

Xét hoán vị $$\sigma_5=\{3, 1, 2\}$$. Khi đó $$P\{3, 1, 2\} = 2$$​, $$a_{13} \cdot a_{21} \cdot a_{32} \cdot (-1)^2 = 3 \cdot 4 \cdot 8 \cdot 1 = 96$$​.

Xét hoán vị $$\sigma_6=\{3, 2, 1\}$$​. Khi đó $$P\{3, 2, 1\}=3$$​, $$a_{13} \cdot a_{22} \cdot a_{31} \cdot (-1)^3 = 3 \cdot 5 \cdot 7 \cdot  (-1) = -105$$​.

Như vậy $$\det(A)=45-48-72+84+96-105=0$$​.

Định thức của ma trận còn được định nghĩa như sau:

**Định nghĩa đệ quy của định thức**

* Với ma trận $$1 \times 1$$là $$\bm{A}=\begin{pmatrix}a_{11}\end{pmatrix}$$​ thì $$\det(\bm{A})=a_{11}$$​
* Với ma trận $$2 \times 2$$ là $$\bm{A} = \begin{pmatrix}a_{11} & a_{12} \\ a_{21} & a_{22}\end{pmatrix}$$​ thì $$\det(\bm{A})=a_{11}a_{22} - a_{21}a_{12}$$
* Với ma trận $$n \times n$$, gọi $$\bm{M}_{ij}$$ là ma trận có được từ ma trận$$\bm{A}$$khi bỏ đi hàng $$i$$​ và cột $$j$$​ của ma trận $$\bm{A}$$ và ký hiệu $$A_{ij}=(-1)^{i+j}\det (\bm{M}_{ij})$$. Khi đó:

**Định lý Laplace**

Khai triển theo cột $$j$$​: $$\det(\bm{A})=\displaystyle{\sum_{i=1}^na_{ij} A_{ij}} = a_{1j} A_{1j} + a_{2j} A_{2j} + \cdots + a_{nj} A_{nj},\ j = \overline{1, n}$$​.

Khai triển theo hàng $$i$$​: $$\det(\bm{A})=\displaystyle{\sum_{j=1}^n a_{ij} A_{ij}} = a_{i1} A_{i1} + a_{i2} A_{i2} + \cdots + a_{in} A_{in},\ i = \overline{1, n}$$.​

### 2. Ma trận nghịch đảo (Inverse of matrix)

Ma trận $$\bm{A}^{-1}$$​ được gọi là **ma trận nghịch đảo** của ma trận vuông $$\bm{A}$$ nếu $$\bm{A}^{-1} \cdot \bm{A} = \bm{A} \cdot \bm{A}^{-1} = \bm{I}$$​. Trong đó $$\bm{I}$$ là ma trận đơn vị cùng kích thước với $$\bm{A}$$​.

$$\bm{A}^{-1}=\frac{1}{\det(\bm{A})}[(A_{ij})_n]^T=\frac{1}{\det(\bm{A})}\begin{pmatrix} A_{11} & A_{21} & \cdots & A_{n1} \\ A_{12} & A_{22} & \cdots & A_{n2} \\ \cdots & \cdots & \cdots & \cdots \\ A_{1n} & A_{2n} & \cdots & A_{nn} \end{pmatrix}$$​.

Như vậy, điều kiện cần và đủ để một ma trận có nghịch đảo là định thức khác 0.

### 3. Hạng của ma trận

**Định nghĩa**: cho ma trận $$\mathbf{A}_{m \times n}$$. **Hạng** của ma trận là cấp của ma trận con lớn nhất có định thức khác 0. Nghĩa là một ma trận vuông mà là ma trận con (lấy 1 phần của ma trận gốc) kích thước $$r \times r$$ mà có định thức khác 0, thì hạng của ma trận khi đó là $$r$$. Dễ thấy do là ma trận con, và vuông, nên $$r \leq \min(m, n)$$.

Ví dụ, ma trận $$\bm{A} = \begin{pmatrix}1 & 2 & 3 \\ 2 & 4 & 6 \\ 1 & 2 & 4\end{pmatrix}$$ có định thức $$\det(\bm{A}) = 0$$. Nhưng ma trận con của $$\bm{A}$$ là $$\bm{B} = \begin{pmatrix}2 & 3 \\ 2 & 4\end{pmatrix}$$ (lấy dòng 1 và 3, lấy cột 2 và 3) có định thức $$\det(\bm{B}) = 2 \neq 0$$, do đó $$r = \text{rank}(\bm{A}) = 2$$ ($$\text{rank}(\bm{A})$$ nghĩa là hạng của $$\bm{A}$$).

Tuy nhiên với ma trận cỡ lớn thì không dễ gì tìm được ma trận con như vậy. Thông thường chúng ta sẽ đưa về ma trận bậc thang để biết được hạng ma trận. **Số dòng** khác $$\vec{0}$$ của ma trận bậc thang chính là hạng của ma trận ban đầu.

Tại sao hạng lại quan trọng? Vì hạng sẽ cho chúng ta biết nhiều thông tin hơn và làm được nhiều thứ hơn. :)))) Nói không thì khá mơ hồ. Các bài viết sau sẽ giải đáp.
