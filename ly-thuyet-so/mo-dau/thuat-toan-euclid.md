# Thuật toán Euclid

Thuật toán cơ bản và thuộc hàng quan trọng bậc nhất của lý thuyết số.

Thuật toán này dựa trên nhận xét: Nếu ký hiệu $$\gcd(a, b)$$​ là ước chung lớn nhất của $$a$$​ và $$b$$​ thì

$$\gcd(a, b) = \begin{cases} \gcd(b, a \bmod b)\, & \text{nếu} \, b \neq 0 \\ a \, & \text{nếu} \, b = 0 \end{cases}$$

Có thể chứng minh như sau:

Gọi $$d=\gcd(a, b)$$​ thì $$d \vert a$$​ và $$d \vert b$$​. Giả sử $$a \geq b$$​, mình có thể viết $$a = bq + r$$​ với $$0 \leq r < b$$​ (phép chia cơ bản). Do $$d \vert a$$​ và $$d \vert b$$​ nên $$d \vert a -b q = r$$​. Do đó $$\gcd(a, b) = \gcd(b, r)$$​ khi $$b \neq 0.$$​ Quá trình này tiếp diễn tới khi $$a_i = b_i q$$​, khi đó $$\gcd(a_i, b_i) = \gcd(b_i, 0) = b_i$$. Lúc này $$0$$​ trở thành điểm dừng của thuật toán.
