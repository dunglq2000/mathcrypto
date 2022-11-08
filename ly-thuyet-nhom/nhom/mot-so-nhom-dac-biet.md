# Một số nhóm đặc biệt

### 1. Nhóm modulo $$\mathbb{Z}/n\mathbb{Z}$$

Tập hợp các đồng dư modulo $$n$$ cùng với phép cộng số nguyên modulo $$n$$​ tạo thành một nhóm. Nghĩa là $$(\mathbb{Z}/n\mathbb{Z}, +)$$.

Ví dụ, với $$n=5$$, bảng sau thể hiện phép cộng các số modulo 5:

| $$+$$ | 0 | 1 | 2 | 3 | 4 |
| ----- | - | - | - | - | - |
| 0     | 0 | 1 | 2 | 3 | 4 |
| 1     | 1 | 2 | 3 | 4 | 0 |
| 2     | 2 | 3 | 4 | 0 | 1 |
| 3     | 3 | 4 | 0 | 1 | 2 |
| 4     | 4 | 0 | 1 | 2 | 3 |

Ta có thể ký hiệu $$\mathbb{Z}/n\mathbb{Z}$$​ thành $$\mathbb{Z}_n$$​ cho gọn.

### 2. General Linear Group (GL)

Trên $$\mathbb{R}$$​ ta xét tập hợp các ma trận $$n \times n$$​ có định thức khác 0 và phép nhân 2 ma trận. Khi đó tập hợp này tạo thành một nhóm và được ký hiệu là $$GL_n(\mathbb{R})$$​ (ma trận vuông cấp $$n$$​).

Ta chứng minh rằng tập hợp trên là nhóm.

* Với mọi ma trận $$A, B \in GL_n(\mathbb{R})$$ ta có $$\det(AB) = \det(A)\cdot\det(B)$$​ mà định thức cả 2 ma trận đều khác 0 nên tích của chúng cũng khác 0. Do đó ma trận $$AB$$ thuộc $$GL_n(\mathbb{R})$$​.
* Tính kết hợp: phép nhân ma trận có tính kết hợp nên ta dễ dàng suy ra.
* Phần tử đơn vị là ma trận đơn vị cấp $$n.$$​
* Phần tử nghịch đảo của ma trận $$A$$ bất kì luôn tồn tại vì định thức của $$A$$​ khác 0.

Như vậy $$GL_n(\mathbb{R})$$​ tạo thành nhóm.

### 3. Nhóm Dihedral (Dihedral Group)

Nhóm Dihedral có $$2n$$ phần tử. Mỗi phần tử có dạng $$s^i r^j$$ với $$0 \leq i \leq 1$$ và $$0 \leq j \leq n-1$$ với toán tử $$\star$$ được định nghĩa là: phần tử đơn vị là $$e$$, $$r^n = s^2 = e$$ và $$rs = sr^{-1}$$.

Ví dụ mình xét $$n=3$$.

* Nhóm Dihedral lúc này gồm các phần tử $$\{e, r, r^2, s, sr, sr^2\}$$ với toán tử $$\star$$ được định nghĩa là: phần tử đơn vị là $$e$$, $$r^3=s^2=e$$ và $$rs = sr^{-1}$$
* Sử dụng định nghĩa với toán tử như trên ta có thể tính được như sau:&#x20;
  * Với $$r$$ và $$r^2$$ thì $$(r)(r^2) = r^3 = e$$. Như vậy $$r^2$$ là nghịch đảo của $$r$$ và ngược lại.
  * Với $$r$$ và $$s$$ thì $$(r)(s) = sr^{-1} = sr^{-1}r^{-2}r^2 = sr^{-3}r^2 = sr^2$$, nhưng $$(s)(r)=sr \neq sr^2$$. Do đó nhóm Dihedral không có tính giao hoán.
