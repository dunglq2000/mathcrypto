# Định lý Euler

**Định nghĩa**. Cho $$n$$ là số nguyên dương. Tập hợp các đồng dư thức modulo $$n$$ là $$S = \{0, 1, 2, \cdots, n-1\}$$ tạo thành một **hệ thặng dư đầy đủ** modulo $$n$$​.

**Định nghĩa**. Cho $$n$$​ là số nguyên dương. Tập hợp các đồng dư nguyên tố cùng nhau với $$n$$ là $$T = \{k \vert 1 \leq k < n, \, \gcd(k, n) = 1$$ và được gọi là **hệ thặng dư thu gọn** modulo $$n$$​. Số lượng phần tử của tập hợp này là $$\varphi$$-hàm Euler của $$n$$​.

**Định lý Euler**: cho $$a$$ và $$n$$ là 2 số nguyên dương và $$\gcd(a, n)=1$$. Khi đó $$a^{\phi(n)} = 1 \pmod n$$.

Chứng minh:

Đặt $$T = \{g_1, g_2, \cdots, g_{\varphi(n)}\}$$. Khi đó nếu mình nhân tất cả phần tử của $$T$$​ với $$a$$​ trong modulo $$n$$, mình sẽ nhận lại được tập $$T$$ với thứ tự khác. Nghĩa là:

$$\{a \cdot g_1 \bmod n,\cdots, a \cdot g_{\varphi(n)} \bmod n\} \equiv \{g_1, \cdots, g_{\varphi(n)}\}$$

Nhận xét này đúng vì nếu mình có 2 phần tử $$a \cdot g_i \equiv a \cdot g_j \bmod n$$​, do $$\gcd(a, n)=1$$​ nên giản lược $$a$$​ 2 vế mình có $$g_i \equiv g_j \bmod n$$. Đồng nghĩa nếu $$g_i \not\equiv g_j \bmod n$$​ thì $$a \cdot g_i \not\equiv a \cdot g_j \bmod n$$​.

Như vậy mình lấy tích các phần tử ở 2 trường hợp thì chúng bằng nhau modulo $$n$$​.

$$a \cdot g_1 \cdots a \cdot g_{\varphi(n)} \equiv g_1 \cdots g_{\varphi(n)} \bmod n$$​ mà $$\gcd(g_i, n)=1$$​ nên mình có thể giản lược $$g_i$$​ ở 2 vế. Kết quả là $$a^{\varphi(n)} \equiv 1 \bmod n$$​. Điều phải chứng minh.
