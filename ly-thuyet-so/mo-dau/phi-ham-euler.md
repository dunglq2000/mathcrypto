# Phi hàm Euler

$$\varphi$$​ hàm Euler (hay Euler's totient phi function) của số nguyên dương $$n$$​ là số lượng số nguyên dương nhỏ hơn $$n$$​ và nguyên tố cùng nhau với $$n$$​. Nói cách khác là đếm xem có bao nhiêu số $$k$$ mà $$1 \leq k < n$$​ và $$\gcd(n, k) = 1$$​.

Ví dụ, với số $$n=5$$​ thì $$\varphi(5)=4$$​ vì các số $$k$$​ thỏa mãn là $$1, 2, 3, 4$$​.

Ví dụ, với số $$n=6$$​ thì $$\varphi(6)=2$$​ vì các số $$k$$​ thỏa mãn chỉ có $$1, 5$$​.

### Tính chất hàm Euler

Nếu $$n=p$$​ là số nguyên tố. Dễ thấy $$\varphi(n)=n-1$$​.

Nếu $$n=p^e$$​ với $$p$$​ là số nguyên tố, $$e \in \mathbb{N}$$​. Để tìm $$\varphi(n)$$​ chúng ta tìm tất cả các số **không nguyên tố cùng nhau** với $$n$$​. Mà $$p$$​ là số nguyên tố nên những số cần tìm sẽ có ước chung là $$p$$​, cụ thể là $$\{1p, 2p, \cdots, p^{e-1} p\}$$​. Tập hợp này gồm $$p^{e-1}$$​ số. Mình trừ đi các số này sẽ có được số $$\varphi(p^e) = p^e - p^{e-1}$$.

Nếu $$\gcd(m, n) = 1$$​ thì $$\varphi(mn) = \varphi(m) \varphi(n)$$​. Đây là tính chất nhân tính của hàm Euler. Để chứng minh mình viết các số từ $$1$$​ tới $$mn$$​ theo dạng $$r + km$$​ ($$1 \leq r \leq m$$​ và $$0 \leq k < n$$​). Như vậy số phần tử nguyên tố cùng nhau với $$m$$ trên mỗi hàng là $$\varphi(m)$$ (tức là chỉ lấy các số $$r$$ mà $$\gcd(r, m) = 1$$). Và mình có $$n$$ hàng như vậy, mình sẽ chỉ lấy hàng $$k$$ mà $$\gcd(k, n) = 1$$ (do $$\gcd(m, n) = 1$$ nên chỉ cần lấy ra các hàng nguyên tố cùng nhau với $$n$$), như vậy có $$\varphi(n)$$ hàng như vậy. Mỗi hàng trong $$\varphi(n)$$ hàng có $$\varphi(m)$$ phần tử nguyên tố cùng nhau với $$m \times n$$, như vậy $$\varphi(m) \varphi(n) = \varphi(mn)$$. Điều phải chứng minh.

Nếu $$n = p_1^{e_1} p_2^{e_2} \cdots p_k^{e_k}$$​ (phân tích thành thừa số nguyên tố). Áp dụng tất cả những điều trên mình có $$\varphi(n) = \displaystyle{\prod_{i=1}^k \varphi(p_i^{e_i}) = \prod_{i=1}^k p_i^{e_i} - p_i^{e_i-1} = \prod_{i=1}^k p_i^{e_i}\Big(1 - \frac{1}{p_i}\Big) = n \prod_{i=1}^k\Big(1-\frac{1}{p_i}\Big)}$$.

**Hệ quả.** Ta có $$\displaystyle{\sum_{d \vert n} \varphi(d) = n}$$

Chứng minh: Giả sử phân tích thừa số nguyên tố của $$n$$ là $$n = p_1^{e_1} p_2^{e_2} \cdots p_k^{e_k}$$. Với mọi $$d \vert n$$​ thì $$d$$​ có dạng $$d = p_1^{f_1} p_2^{f_2} \cdots p_k^{f_k}$$​ với $$0 \leq f_i \leq e_i$$, $$i = 1, \cdots, k$$​.

Khi đó $$\varphi(d) = \displaystyle{\prod_{i=1}^k \varphi(p_i^{f_i})}$$. Do đó $$\displaystyle{\sum_{d \vert n} \varphi(d) = \prod_{i=1}^k (1 + \varphi(p_i) + \varphi(p_i^2) + \cdots + \varphi(p_i^{e_i})) = n}$$. Điều phải chứng minh.
