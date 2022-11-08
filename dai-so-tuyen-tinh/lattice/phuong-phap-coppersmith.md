# Phương pháp Coppersmith

Giả sử mình có phương trình $$F(x) \equiv 0 \bmod M$$​. Với số $$X$$​ cố định cho trước, phương pháp Coppersmith cho phép tìm nghiệm $$x_0$$ nhỏ thỏa mãn $$\lvert x_0 \rvert \leq X$$​.

Ý tưởng của phương pháp này là thay vì tìm nghiệm $$x_0$$ của $$F(x)$$​ trên modulo $$M$$​, chúng ta sẽ mở rộng lên, tìm một hàm $$G(x)$$​ nào đó mà có nghiệm $$x_0$$​ trên $$\mathbb{Z}$$​.

Đơn giản nhất là $$G(x) = k \cdot F(x) + M \cdot g(x)$$​, $$k \in \mathbb{Z}$$ và $$\deg g(x) \leq \deg F(x)$$. Rõ ràng khi modulo 2 vế cho $$M$$​ thì $$G(x_0) = F(x_0) = 0 \bmod M$$​.

Phương pháp này giúp tìm nghiệm của một đa thức bậc nhỏ modulo $$M$$​. Do đó giả mình đặt:

$$F(x) = a_0 + a_1 x + \cdots + a_d x^d$$​ với $$a_i \in \mathbb{Z}$$

Lúc này chúng ta sẽ tìm hàm $$G(x)$$​ trên với hệ số nhỏ.

Giả sử $$g(x) = b_0 + b_1 x + \cdots + b_d x^d$$ với $$b_i \in \mathbb{Z}$$.

Khi đó $$G(x) = (k \cdot a_0 + M \cdot b_0) + (k \cdot a_1 + M \cdot b_1) x + \cdots + (k \cdot a_d + M \cdot b_d) x^d$$. Khi đó các hệ số $$k \cdot a_0 + M \cdot b_0$$​, $$k \cdot a_1 + M \cdot b_1$$​, $$\cdots$$​, $$k \cdot a_d + M \cdot b_d$$ nhỏ so với $$M$$​.

Do đó với số $$X$$​ cho trước, nếu ta xây lattice ($$d+2$$ vector) sau:

$$\bm{v}_0 = (M, 0, 0, \cdots, 0, 0)$$

$$\bm{v}_1 = (0, MX, 0, \cdots, 0, 0)$$

vân vân

$$\bm{v}_d = (0, 0, 0, \cdots, 0, MX^d)$$​

$$\bm{v}_{d+1} = (a_0, a_1 X, a_2 X^2, \cdots, a_{d-1} X^{d-1}, a_d X^d)$$

Khi đó hệ số của mỗi dòng từ $$\bm{v}_0$$​ tới $$\bm{v}_d$$​ là $$b_0$$​ tới $$b_d$$​. Còn hệ số của $$\bm{v}_{d+1}$$​ là $$k$$​.

Tuy nhiên chúng ta thường sẽ biến đổi để đa thức trở thành monic ($$a_d = 1$$​). Khi đó chúng ta bỏ đi $$v_d$$​ và còn $$d+1$$​ vector trong lattice.

```python
from sage.all import *

def small_roots(f, M, X):
    d = f.degree()

    P = f.base_ring()
    B = []
    for i in range(d):
        b = [0] * (d + 1)
        b[i] = M * X**i
        B.append(b)
    B.append([j * X**i for i, j in enumerate(f.coefficients())])
    B = Matrix(ZZ, B)
    B = B.LLL()
    bf = B[0]
    g = sum((j // (X**i)) * x**i for i, j in enumerate(bf))
    roots = g.roots()
    return [root[0] for root in roots]
```

Test thử theo sách giáo khoa thì code cũng oke :))

```python
M = 10001
X = 10
P = PolynomialRing(ZZ, 'x')
Q = PolynomialRing(Zmod(M), 'xn')
x = P.gen()
xn = Q.gen()
f = x**3 + 10*x**2 + 5000*x - 222
g = f.change_ring(Q).subs(x=xn)
print(small_roots(f, M, X))
print(g.small_roots(X=10))
```

&#x20;Có vẻ hàm **small\_roots** mình tự chế và hàm có sẵn trong SageMath cho ra cùng kết quả :))
