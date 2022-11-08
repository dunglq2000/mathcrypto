# Phương pháp Coppersmith mở rộng (phần 2)

### Dạng không đơn giản

Coppersmith đã có một ý tưởng đột phá như sau :))))

**Bổ đề**. (_Coppersmith_) Với $$0 < \epsilon < \min \{0,18; 1/d\}$$. Đặt $$F(x)$$​ là đa thức monic bậc $$d$$​ có một hoặc nhiều nghiệm $$x_0$$​ trên modulo $$M$$​ sao cho $$\lvert x_0 \rvert \leq \frac{1}{2} M^{1/d-\epsilon}$$. Khi đó $$x_0$$​ có thể tính với thời gian đa thức giới hạn bởi $$d$$​, $$1/\epsilon$$​ và $$\log(M)$$.

Để chứng minh bổ đề này thì ông Coppersmith đã xây dựng một hệ lattice để tính toán và cũng là cách xây dựng lattice mình sẽ đề cập tới đây. Còn chứng minh thì phức tạp quá nên mình tạm thời bỏ qua :))))

Chúng ta biết rằng $$x_0$$​ là nghiệm của đa thức $$F(x) \equiv 0 \bmod M$$​. Do đó ta suy ra $$F(x_0)^k \equiv 0 \bmod M^k$$​.

Từ nhận xét này, mình mở rộng phần 1 lên tìm nghiệm trong modulo $$M^{h-1}$$​ với $$h$$ là một số được chọn trước.

Với $$k(x) = c_0 + c_1 x + \cdots + c_{d-1} x^{d-1}$$ biểu diễn việc shift thành $$F(x)$$, $$xF(x)$$​, $$x^2 F(x)$$, ..., $$x^{d-1} F(x)$$​.

Mình xét $$h$$​ đa thức sau:

$$M^{h-1} F(x)^0 k(x) \equiv 0 \bmod M^{h-1}$$​

$$M^{h-2} F(x)^1 k(x) \equiv 0 \bmod M^{h-1}$$​

vân vân

$$M^0 F(x)^{h-1} k(x) \equiv 0 \bmod M^{h-1}$$​

Với mỗi đa thức $$M^{h-1-j} F(x)^j$$​ chúng ta có $$d$$​ lần shift tương ứng với từng hệ số của $$k(x)$$​. Cụ thể là $$M^{h-1-j}F(x)^j$$​, $$M^{h-1-j}F(x)^j x$$​, $$M^{h-1-j}F(x)^j x^2$$​, ..., $$M^{h-1-j}F(x)^j x^{d-1}$$​.

Do đó có tất cả $$dh$$​ vector trong lattice. Số $$h$$​ thường được chọn sao cho $$dh \approx \epsilon$$. Và chặn nghiệm $$X$$​ có thể chọn là $$\frac{1}{2}M^{1/d - \epsilon}$$​ theo như bổ đề.

Như vậy mình xây lattice như sau:

1\) Với $$M^{h-1} F(x)^0$$​ thì:

$$\bm{v}_0 = (M^{h-1}, 0, 0, \cdots, 0, 0, \cdots)$$. Tương ứng $$M^{h-1}F(x)^0$$.

$$\bm{v}_1 = (0, M^{h-1} X, 0, \cdots, 0, 0, \cdots)$$. Tương ứng $$M^{h-1}F(x)^0 x$$​.

vân vân

$$\bm{v}_{d-1} = (0, 0, 0, \cdots, M^{h-1} X^{d-1}, 0, \cdots)$$. Tương ứng $$M^{h-1} F(x)^0 x^{d-1}$$​.

2\) Với $$M^{h-2} F(x)$$​ thì:

$$\bm{v}_d = (Ma_0, M a_1 X, M a_2 X^2, \cdots, M a_{d-1} X^{d-1}, M X^d, \cdots)$$. Tương ứng $$M^{h-2} F(x)$$​.

$$\bm{v}_{d+1} = (0, Ma_0 X, Ma_1 X^2, \cdots, M a_{d-2} X^{d-1}, M a_{d-1} X^d, M X^{d+1}, \cdots)$$. Tương ứng $$M^{h-2}F(x) x$$​.

vân vân

$$\bm{v}_{2d-1} = (0, 0, 0, \cdots, M a_0 X^{d-1}, M a_1 X^d, \cdots)$$. Tương ứng $$M^{h-2} F(x) x^2$$​.

Cứ như vậy với $$M^{h-1-j}F(x)^j$$​.

Chạy LLL trên lattice trên sẽ cho kết quả :))))

Code cuối cùng kết thúc chuỗi ngày đau khổ với Coppersmith **1 BIẾN**:

```python
from sage.all import *

def small_roots(f, M, h = None, epsilon = None, X = None):
    d = f.degree()
    if not h:
        h = d
    if not epsilon:
        epsilon = 1/(d*h)
    if not X:
        X = round(0.5*M**(1/d-epsilon))
    B = []
    for j in range(h):
        g = M**(h-1-j) * f**j
        for i in range(d):
            k = g * x**i
            b = [v * X**u for u, v in enumerate(k.coefficients(sparse=False))]
            b = b + [0] * (d*h - len(b))
            B.append(b)

    B = Matrix(ZZ, B)
    B = B.LLL()
    bf = B[0]
    g = sum((j // (X**i)) * x**i for i, j in enumerate(bf))
    roots = g.roots()
    return [root[0] for root in roots]
```

a) Với bộ test

```python
M = (2**30 + 3)*(2**32 + 15)
P = PolynomialRing(ZZ, 'x')
x = P.gen()
f = 1942528644709637042 + 1234567890123456789*x + 987654321987654321*x**2 + x**3
print(small_roots(f, M))
```

cho kết quả $$x_0 = 16384$$ như sách giáo khoa.

b) Với bộ test

```python
M = (2**20 + 7)*(2**21 + 17)
P = PolynomialRing(ZZ, 'x')
x = P.gen()
f = x**3 + (2**25 - 2883584)*x**2 + 46976195*x + 227
print(small_roots(f, M, X = 2**9))
```

cho kết quả $$x_0 = 267$$​ (có vẻ đúng :v)
