# Hàm Mebius

Đây là hàm có tính chất thú vị trong số học.

Với số nguyên dương $$n$$​, hàm Mebius của $$n$$​ được ký hiệu là $$\mu(n)$$​ và được định nghĩa như sau:

$$\mu(n) = \begin{cases}1 \, & \text{khi} \, n = 1 \\ (-1)^k \, & \text{khi} \, n = p_1 p_2 \cdots p_k \\ 0 \, & \text{các trường hợp khác}\end{cases}$$

Ý nghĩa của điều kiện thứ 2 là $$n$$​ bằng tích các số nguyên tố với lũy thừa bằng 1. Do đó điều kiện thứ 3 tương đương có số nguyên tố với lũy thừa lớn hơn 2 là ước của $$n$$​ ($$\exists p_i: \, p_i^2 \vert n$$).

### Tính chất hàm Mebius

1. Nếu $$(n_1, n_2) = 1$$​ thì $$\mu(n_1 n_2) = \mu(n_1) \mu(n_2)$$​. Tính chất này khá dễ thấy.
2. $$\displaystyle{\sum_{d \vert n} \mu(d) = 0}$$ với $$n = p_1 p_2 \cdots p_k$$. Để chứng minh mình xét các trường hợp:

TH1: với $$d = 1$$ thì $$\mu(d)=1$$​

TH2: với $$d = p_i$$  thì $$\mu(d) = (-1)^1 = 1$$​

TH3: với $$d = p_i p_j$$​ thì $$\mu(d) = (-1)^2 = 1$$ ($$d$$​ là tích 2 số nguyên tố)

..........................

TH$$t$$: với $$d = p_{i_1} p_{i_2} \cdots p_{i_t}$$ thì $$\mu(d) = (-1)^t$$ ($$d$$​ là tích $$t$$​ số nguyên tố)

Với mỗi số trường hợp, số cách chọn $$d$$​ là $$C^t_k$$​ (chọn $$t$$​ số nguyên tố từ $$k$$​ số nguyên tố). Do đó

$$\displaystyle{\sum_{d \vert n} \mu(d) = 1 - C^1_k + C^2_k + \cdots + (-1)^k C^k_k = 0}$$​ (dùng nhị thức Newton suy ra điều phải chứng minh).
