# Phương pháp Coppersmith mở rộng

Ở phương pháp Coppersmith mình đề cập ở bài viết trước, để tìm nghiệm $$x_0$$ của đa thức $$F(x) \equiv 0 \bmod M$$ thì mình tìm một đa thức $$G(x)$$​ cũng có nghiệm $$x_0$$​ trên $$\mathbb{Z}$$​ thay vì trên modulo $$M$$​ (trên $$\mathbb{R}$$​ chúng ta có nhiều phương pháp tính xấp xỉ nghiệm từ đó tìm được nghiệm nguyên của 1 phương trình).

Khi đó $$G(x)$$​ có dạng $$G(x) = k \cdot F(x) + M \cdot g(x)$$​ với $$k \in \mathbb{Z}$$​ và $$g(x)$$​ là đa thức hệ số nguyên với bậc nhỏ hơn hoặc bằng bậc của $$F(x)$$​.

Chúng ta có thể để ý rằng, thay vì dùng mỗi số nguyên $$k$$​, ta có thể mở rộng lên một đa thức $$k(x)$$​ nào đó. Vì $$G(x_0) = k(x_0) \cdot F(x_0) + M \cdot g(x) \equiv k(x_0) \cdot 0 \equiv 0 \bmod M$$. Nghĩa là $$x_0$$​ là nghiệm của $$G(x)$$​ trên modulo $$M$$ và có thể tìm được trên $$\mathbb{Z}$$​.

Giống bài viết trước, mình đặt:

$$F(x) = a_0 + a_1 x + \cdots a_{d-1}x^{d-1} + x_d$$​ ($$F(x)$$​ là đa thức monic đã biết).

$$g(x) = b_0 + b_1 x + \cdots b_d x^d$$​
