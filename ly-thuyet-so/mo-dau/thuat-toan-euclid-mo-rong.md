# Thuật toán Euclid mở rộng

**Phương trình Diophantine**: với 2 số nguyên $$a$$ và $$b$$, đặt $$d = \gcd(a, b)$$. Khi đó tồn tại 2 số $$x$$ và $$y$$ sao cho $$ax + by = d$$. Thuật toán Euclid mở rộng giúp mình tìm 2 số $$x$$ và $$y$$ này. Lưu ý rằng có nhiều cặp $$(x, y)$$ thỏa mãn phương trình trên nhưng mình chỉ cần 1 cặp là đủ.

Mã giả của thuật toán có thể được viết như sau:

```python
Đặt x_0 = 1, x_1 = 0, y_0 = 1, y_1 = 0
while b != 0 do
    q = a div b
    a, b = b, a - qb                // thuật toán Euclid chuẩn
    x_0, x_1 = x_1, x_0 - q x_1    // tìm hệ số x
    y_0, y_1 = y_1, y_0 - q y_1    // tìm hệ số y
Output (a, x_0, y_0)
```

Các output lần lượt là $$\gcd(a, b), x_0, y_0$$​ thỏa mãn phương trình $$a \cdot x_0 + b \cdot y_0 = \gcd(a, b)$$​.

Các nghiệm khác của phương trình trên có thể được viết dưới dạng:

$$\begin{gather}x_k = x_0 + k \cdot \frac{b}{\gcd(a, b)} \\ y_k = y_0 - k \cdot \frac{a}{\gcd(a, b)}\end{gather} \,$$ với $$k \in \mathbb{Z}$$
