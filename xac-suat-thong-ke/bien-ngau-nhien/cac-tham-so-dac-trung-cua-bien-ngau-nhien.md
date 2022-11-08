# Các tham số đặc trưng của biến ngẫu nhiên

### 1. Trung vị (Median)

**Định nghĩa**. Trung vị (median) của BNN, ký hiệu là $$MedX$$​, là số thực $$m$$​ thỏa:

$$P(X \leq m) = P(X \geq m)$$​.

### 2. MODE

**Định nghĩa**. Mode của BNN $$X$$​, ký hiệu là $$ModX$$​, là giá trị $$x_0 \in X$$​ thỏa:

* $$P(X = x_0) \max$$​ nếu $$X$$​ rời rạc
* $$f(x_0) \max$$​ nếu $$X$$​ liên tục với hàm mật độ $$f(x)$$​.

$$ModX$$​ còn được gọi là **giá trị tin chắc nhất** của $$X$$​.

Dễ thấy rằng có thể có nhiều giá trị $$x_0$$​ cho $$P(X=x_0) \max$$​ đối với BNN rời rạc, cũng như nhiều giá trị khiến hàm $$f(x)$$ đạt giá trị lớn nhất. Do đó BNN có thể nhận nhiều MODE.

### 3. Kỳ vọng (Expectation)

**Định nghĩa**. Kỳ vọng (Expectation) của BNN $$X$$​, ký hiệu là $$EX$$​ hay $$M(X)$$​, là một số thực được xác định như sau:

* Đối với BNN $$X$$​ rời rạc với xác suất $$P(X = x_i) = p_i$$ thì $$M(X) = \displaystyle{\sum_i x_i p_i}$$​.
* Đối với BNN $$X$$​liên tục với hàm mật độ $$f(x)$$​ thì $$M(X) = \displaystyle{\int_{-\infty}^{+\infty} x \cdot f(x)\, dx}$$.

**Ý nghĩa của kỳ vọng**

Kỳ vọng của BNN $$X$$​ là **giá trị trung bình theo xác suất** mà $$X$$​ nhận được, phản ánh giá trị trung tâm phân phối xác suất của $$X$$​.

**Kỳ vọng của hàm của biến ngẫu nhiên**

Giả sử $$Y=\varphi(X)$$​ là hàm của biến ngẫu nhiên $$X$$​.

* Nếu $$X$$​ rời rạc thì $$M(Y) = \displaystyle{\sum_i y_i p_i = \sum_i \varphi(x_i) p_i}$$.
* Nếu $$X$$​liên tục thì $$M(Y) = \displaystyle{\int_{-\infty}^{+\infty} y \cdot f(x)\, dx = \int_{-\infty}^{+\infty} \varphi(x) \cdot f(x)\, dx}$$.

**Tính chất của kỳ vọng**

1\) $$M(C) = C$$​ với $$C \in \mathbb{R}$$.

2\) $$M(CX) = C \cdot M(X)$$​ với $$C \in \mathbb{R}$$​.

3\) $$M(X \pm Y) = M(X) \pm M(Y)$$.

4\) $$M(X Y) = M(X) \cdot M(Y)$$​ nếu $$X$$​, $$Y$$​ độc lập.

### 4. Phương sai (Variance hoặc Dispersion)

ĐĐịnh
