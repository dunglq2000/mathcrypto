# Phương pháp Coppersmith mở rộng (phần 1)

### Dạng đơn giản

Giả sử $$k(x)$$​ có bậc là $$h$$​. Đặt $$k(x) = c_0 + c_1 x + \cdots c_h x^h$$​.

Khi đó ​$$G(x) = k(x) \cdot F(x) + M \cdot g(x)$$

$$= (c_0 + c_1 x + \cdots c_h x^h) \cdot (a_0 + a_1 x + \cdots + x^d) + M \cdot (b_0 + b_1 x + \cdots + b_d x^d)$$

$$=c_0 \cdot F(x) + c_1 \cdot xF(x) + \cdots c_h \cdot x^h F(x) + M \cdot (b_0 + b_1 x + \cdots b_d x^d)$$

Lúc này mỗi đại lượng $$F(x)$$​, $$xF(x)$$​, $$\cdots$$​, $$x^h F(x)$$​ sẽ khiến hệ số của $$F(x)$$​ ban đầu tăng bậc. Nói cách khác hệ số $$a_i$$ của $$x^i$$​ trong $$F(x)$$​ sẽ là hệ số của $$x^{i+j}$$​ trong $$x^j F(x)$$​.

Sách giáo khoa nói rằng nếu mình chọn $$h=d-1$$​ thì phương pháp Coppersmith sẽ cho ra kết quả nếu $$X$$​ được chọn thỏa $$X \approx M^{1/(2d-1)}$$.

Tương tự, mình sẽ có các vector trong lattice như sau:

$$\bm{v}_0 = (M, 0, 0, \cdots, 0, 0, 0, 0, \cdots)$$​

$$\bm{v}_1 = (0, MX, 0, \cdots, 0, 0, 0, 0, \cdots)$$

vân vân

$$\bm{v}_{d-1} = (0, 0, 0, \cdots, MX^{d-1}, 0, 0, 0, 0, \cdots)$$

$$\bm{v}_d = (a_0, a_1 X, a_2 X^2, \cdots, a_{d-1} X^{d-1}, X^d, 0, 0, \cdots)$$

Sau đó thêm các vector khi shift vào (tương ứng với $$xF(x)$$​, $$x^2 F(x)$$​, $$\cdots$$​

$$\bm{v}_{d+1} = (0, a_0 X, a_1 X^2, a_2 X^3, \cdots, a_{d-1} X^d, a_d X^{d+1}, 0, 0, \cdots)$$ tương ứng $$xF(x)$$​.

$$\bm{v}_{d+2} = (0, 0, a_0 X^2, a_1 X^3, \cdots, a_{d-2} X^d, a_{d-1} X^{d+1}, a_d X^{d+2}, 0, \cdots)$$ tương ứng $$x^2F(x)$$​.

vân vân

Mình update code bài trước như sau:

```python
from sage.all import *

def small_roots(f, M, X):
    d = f.degree()
    B = []
    for i in range(d):
        b = [0] * (2*d)
        b[i] = M * X**i
        B.append(b)
    for i in range(d):
        g = x**i * f
        b = [v * X**u for u, v in enumerate(g.coefficients(sparse=False))]
        b = b + [0] * (2*d - len(b))
        B.append(b)
    B = Matrix(ZZ, B)
    print(B)
    B = B.LLL()
    bf = B[0]
    g = sum((j // (X**i)) * x**i for i, j in enumerate(bf))
    roots = g.roots()
    return [root[0] for root in roots]
```

Test thử theo sách giáo khoa thì vẫn đúng :))))

```python
M = 10001
X = 10
P = PolynomialRing(ZZ, 'x')
x = P.gen()
f = x**3 + 10*x**2 + 5000*x - 222
print(small_roots(f, M, X))
```

Tuy nhiên vấn đề ở đây là bound của nghiệm bị thu hẹp lại. Ban nãy mình nói rằng nếu chọn $$h=d-1$$​ thì nghiệm cho kết quả nếu $$X \approx M^{1/(2d-1)}$$​. Ở đây $$M = 10001$$​ nên $$X \approx 4$$​. Trong khi ở bài viết trước thì $$X = 10$$​. Do đó có thể thấy việc mở rộng này đôi khi kém hiệu quả tùy thuộc vào $$h$$​.
