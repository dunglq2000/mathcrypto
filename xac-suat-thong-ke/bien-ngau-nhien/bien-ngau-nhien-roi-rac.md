# Biến ngẫu nhiên rời rạc

Nếu $$X(\Omega)$$​ là 1 tập hữu hạn $$\{x_1, x_2, \cdots, x_n\}$$​ hoặc vô hạn đếm được thì $$X$$​ được gọi là **biến ngẫu nhiên rời rạc**.

Giả sử $$x_1 < x_2 < \cdots < x_n$$​ với xác suất tương ứng là $$P(\{X=x_i\}=p_i$$, $$i=1,2,\cdots$$ Ta định nghĩa:

**Bảng phân phối xác suất** của $$X$$là:

| $$X$$​ | $$x_1$$ | $$x_2$$ | $$\cdots$$ | $$x_n$$ |
| ------ | ------- | ------- | ---------- | ------- |
| $$P$$​ | $$p_1$$ | $$p_2$$ | $$\cdots$$ | $$p_n$$ |

Khi đó, **hàm mật độ** của $$X$$​ là:

$$f(x) = \begin{cases}p_i \text{ khi } x = x_i,\\ 0 \text{ khi } x \neq x_i,\ \forall i\end{cases}$$

**Tính chất**

* $$p_i \geq 0$$​ và $$\sum p_i = 1$$​, $$i = 1, 2, \cdots$$​
* Nếu $$x \not\in \{x_1, x_2, \cdots, x_n\}$$​ thì $$P(X = x) = 0$$.
* $$P(a < X \leq b) = \displaystyle{\sum_{a < x_i \leq b} p_i}$$​.

**Ví dụ**. Cho BNN rời rạc $$X$$​ có bảng phân phối xác suất như sau:

| $$X$$ | $$-1$$ | $$0$$ | $$1$$    | $$3$$  | $$5$$   |
| ----- | ------ | ----- | -------- | ------ | ------- |
| $$P$$ | $$3a$$ | $$a$$ | $$0.1$$​ | $$2a$$ | $$0.3$$ |
|       |        |       |          |        |         |

Theo định nghĩa, tổng xác suất phải bằng $$1$$​. Như vậy:

$$3a + a + 0.1 + 2a + 0.3 = 1$$​. Suy ra $$a = 0.1$$​.

Giả sử có hàm $$Y=X^2$$​. Khi đó bảng phân phối xác suất của $$Y$$​sẽ là:

$$y=1=1^2=(-1)^2$$. Như vậy $$p(Y=1)=p(X=1)+p(X=-1)=3 \times 0.1 + 0.1 = 0.4$$.

$$y = 0 = 0^2$$​. Như vậy $$p(Y = 0) = p(X = 0) = 0.1$$​.

$$y = 9 = 3^2$$​. Như vậy $$p(Y = 9) = p(X = 3) = 0.2$$​.

$$y = 25 = 5^2$$​. Như vậy $$p(Y = 25) = p(X = 5) = 0.3$$​.
