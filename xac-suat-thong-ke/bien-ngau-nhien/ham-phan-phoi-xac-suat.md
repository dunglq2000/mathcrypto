# Hàm phân phối xác suất

**Định nghĩa**. Hàm phân phối xác suất (hay hàm phân phối tích lũy) của biến ngẫu nhiên $$X$$, ký hiệu $$F(x)$$​, là xác suất để $$X$$​ nhận **giá trị nhỏ hơn** $$x$$​ với mọi $$x \in \mathbb{R}$$​.

Tức là:

$$F(x) = P(X < x),\ \forall x \in \mathbb{R}$$

Do đó:

* Đối với biến ngẫu nhiên rời rạc $$X$$​với phân phối xác suất $$P(X = x_i) = p_i$$ thì: $$F(x) = \displaystyle{\sum_{x_i < x}p_i}$$.
* Đối với biến ngẫu nhiên liên tục $$X$$​ với hàm mật độ $$f(x)$$​ thì: $$F(x) = \displaystyle{\int_{-\infty}^x f(x)\,dx}$$.

Chúng ta rút ra một số nhận xét sau:

* Nếu biến ngẫu nhiên $$X$$​ là rời rạc với phân phối xác suất $$P(X=x_i)=p_i$$​ thì $$F(x) = \displaystyle{\sum_{x_i < x} p_i}$$.
* Nếu biến ngẫu nhiên $$X$$​ là liên tục với hàm mật độ $$f(x)$$​ thì $$F(x) = \displaystyle{\int_{-\infty}^x f(t) dt}$$​.

Cụ thể, đối với biến ngẫu nhiên rời rạc $$X$$​ nhận các giá trị trong $$[x_1, x_n]$$ và $$x_1 < x_2 < \cdots < x_n$$, $$P(X=x_i) = p_i$$ thì ta có hàm phân phối xác suất của $$X$$ là:

$$F(x) = \begin{cases}0\ & \text{khi}\ x \leq x_1 \\ p_1 & \text{khi}\ x_1 < x \leq x_2 \\ p_1 + p_2 \ & \text{khi} \ x_2 < x \leq x_3 \\ \cdots \\ p_1 + p_2 + \cdots + p_n \ & \text{khi} \ x_{n-1} < x \leq x_n  \\ 1 \ & \text{khi} \ x_n < x\end{cases}$$

Tương tự, đối với biến ngẫu nhiên liên tục $$X$$​ có hàm mật độ

$$f(x) = \begin{cases}\varphi(x),\ & x \in [a, b] \\ 0,\ & x \not\in [a, b]\end{cases}$$.

Hàm phân phối xác suất lúc này là:

$$F(x) = \begin{cases}0 & \text{khi} \ x \leq a \\ \displaystyle{\int_a^x \varphi (t)\, dt} & \text{khi} \ a < x \leq b \\ 1 & \text{khi} \ b < x\end{cases}$$.

**Tính chất của hàm phân phối xác suất**

* Hàm $$F(x)$$​ xác định với mọi $$x \in \mathbb{R}$$​.
* $$0 \leq F(x) \leq 1$$​, $$\forall x \in \mathbb{R}$$; $$F(-\infty​)=0$$​; $$F(+\infty)=1$$​.
* $$F(x)$$​ không giảm và liên tục phải tại mọi $$x \in \mathbb{R}$$​.
* $$P(a \leq X < b) = F(b) - F(a)$$​. Lưu ý là dấu bằng có thể có hoặc không.

Như vậy, đối với biến ngẫu nhiên rời rạc $$X$$​ thì:

$$p_i = F(x_{i+1}) - F(x_i),\ \forall i$$​

Đối với biến ngẫu nhiên liên tục $$X$$​ thì:

$$P(a \leq X \leq b) = P(a < X \leq b) = P(a \leq X < b) = P(a < X < b) = F(b) - F(a)$$​

Và nếu $$X$$​ là biến ngẫu nhiên liên tục có hàm mật độ là $$f(x)$$​ thì

$$F'(x) = f(x)$$​
