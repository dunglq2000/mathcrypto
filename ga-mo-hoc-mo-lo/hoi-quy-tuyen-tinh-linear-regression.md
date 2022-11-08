# Hồi quy tuyến tính (Linear Regression)

Bài toán Linear Regression được hình thành từ việc nhận xét rằng, giả sử chúng ta có $$N$$bộ (input, output) mà output "có lẽ" có quan hệ tuyến tính với input. Cụ thể, với mỗi output $$y$$​ và input $$\mathbf{x} = (x_1, x_2, \cdots, x_t)$$, ta tìm hàm tuyến tính $$\hat{y} = f(\mathbf{x}) \approx y$$ sao cho sai số nhỏ nhất có thể.

Ở cấp 2 và 3 chúng ta đã biết, trong mặt phẳng 2 chiều, giả sử chúng ta có 2 điểm $$P=(x_P, y_P)$$​ và $$Q = (x_Q, y_Q)$$​ thì ta có thể tìm đường thẳng đi qua 2 điểm này với dạng $$ax + by + c = 0$$​. Tương tự, trong mặt phẳng 3 chiều, với 3 điểm $$P=(x_P, y_P, z_P)$$​,  $$Q = (x_Q, y_Q, z_Q)$$ và $$R = (x_R, y_R, z_R)$$ thì ta có thể tìm mặt phẳng đi qua 3 điểm với dạng $$ax + by + cz + d = 0$$. Tổng quát, với hệ không gian $$n$$​ chiều ta có thể tìm được siêu phẳng đi qua $$n$$​ điểm.

Quay lại bài toán, để thể hiện hàm tuyến tính ở đây, cách đơn giản nhất là:

$$\hat{y} = f(\mathbf{x}) = f(1, x_1, x_2, \cdots, x_t) = w_0 + w_1 \cdot x_1 + w_2 \cdot x_2 + \cdots + w_t \cdot x_t$$

Ở đây do có hạng tử tự do nên mình thêm số $$1$$​ vào. Như vậy vector $$\mathbf{x} = (1, x_1, x_2, \cdots, x_t)$$​ và $$\mathbf{w} = (w_0, w_1, w_2, \cdots, w_t)$$​ thì $$\hat{y} = f(\mathbf{x}) = \mathbf{x} \cdot \mathbf{w}$$ (tích vô hướng).

Giả sử ban đầu ta có $$N$$ bộ dữ liệu (input, output) là ($$\mathbf{x_i}, y_i)$$, với $$\mathbf{x}_i = (1, x_{i1}, x_{i2}, \cdots, x_{it})$$, $$i = 1, 2, \cdots, N$$. Chúng ta cần xây dựng một hàm mất mát thể hiện được mối quan hệ giữa các output thực tế $$y$$​ và các output dự đoán $$\hat{y}=f(\mathbf{x})$$​ cho mỗi input, sao cho tổng sai lệch giữa $$y$$ và $$\hat{y}$$ là ít nhất.&#x20;

Để biểu diễn bình phương khoảng cách giữa 2 điểm trong không gian ta thường dùng chuẩn Euclid (Euclidean norm). Với 2 điểm trong không gian $$n$$​ chiều $$x = (x_1, x_2, \cdots, x_t)$$​ và $$y = (y_1, y_2, \cdots, y_t)$$​ thì bình phương khoảng cách (hay chuẩn Euclid) giữa $$x$$​ và $$y$$​ là $$\lVert y - x \rVert^2 = (y_1 -x_1)^2 + (y_2 - x_2)^2 + \cdots (y_t - x_t)^2 = \displaystyle{\sum_{i=1}^t (y_i - x_i)^2}$$​.

Như vậy, với $$N$$​ bộ dữ liệu ban đầu, ta tìm hàm $$\hat{y}=f(\mathbf{x})$$​ sao cho tổng giá trị "khoảng cách" từ $$y$$​ tới $$\hat{y}$$​ là nhỏ nhất. Nghĩa là hàm sau đạt giá trị nhỏ nhất:

$$\mathcal{L}(\mathbf{w}) = \displaystyle{\sum_{i=1}^N} \frac{1}{2} (y_i - \mathbf{x}_i \cdot \mathbf{w})^2$$

Chúng ta cần tìm giá trị của $$\mathbf{w}$$​ để tổng trên đạt giá trị nhỏ nhất, không nhất thiết tìm giá trị nhỏ nhất đó của $$\mathcal{L}$$​. Do $$\mathbf{w}$$​ là vector có $$t+1$$​ tham số, mình lấy đạo hàm riêng cho từng $$w_i$$​ sau đó cho tất cả đạo hàm riêng bằng $$0$$​ và tìm được các $$w_i$$​ thỏa mãn hệ phương trình.

Dễ thấy rằng, do $$\mathbf{x}_i \cdot \mathbf{w} = 1 \cdot w_0 + x_{i1} \cdot w_1 + x_{i2} \cdot w_2 + \cdots + x_{it} \cdot w_t$$​ nên khi lấy đạo hàm riêng cho từng $$w_i$$​ thì các $$w_j$$​ còn lại sẽ bị mất. Do đó:

$$\frac{\partial \mathcal{L}}{\partial w_0} = \displaystyle{\sum_{i=1}^N \frac{1}{2} (y_i - \mathbf{x}_i \cdot \mathbf{w}) \cdot (-1) = \sum_{i=1}^N (\mathbf{x}_i \cdot \mathbf{w} - y_i)}$$

$$\frac{\partial \mathcal{L}}{\partial w_1} = \displaystyle{\sum_{i=1}^N \frac{1}{2} (y_i - \mathbf{x}_i \cdot \mathbf{w}) \cdot(-x_{i1}) = \sum_{i=1}^N x_{i1} \cdot  (\mathbf{x}_i \cdot \mathbf{w} - y_i)}$$

$$\frac{\partial \mathcal{L}}{\partial w_2} = \displaystyle{\sum_{i=1}^N \frac{1}{2} (y_i - \mathbf{x}_i \cdot \mathbf{w}) \cdot(-x_{i2}) = \sum_{i=1}^N x_{i2} \cdot (\mathbf{x}_i \cdot \mathbf{w} - y_i)}$$

Cứ như vậy ta có tổng quát: $$\frac{\partial \mathcal{L}}{\partial w_t} = \displaystyle{\sum_{i=1}^N \frac{1}{2} (y_i - \mathbf{x}_i \cdot \mathbf{w}) \cdot(-x_{it}) = \sum_{i=1}^N x_{it} \cdot (\mathbf{x}_i \cdot \mathbf{w} - y_i)}$$

Khi khai triển tới đây, mình kiểu "The hell cái gì phức tạp vậy" :((((

Sau đó mình nhận ra mỗi đạo hàm riêng là tổng của các tích, nghĩa là mình có thể viết dưới dạng tích của một vector hàng và một vector cột như sau (cho $$w_1$$):

$$\frac{\partial \mathcal{L}}{\partial w_1} = \begin{pmatrix} x_{11} & x_{21} & \cdots & x_{N1}\end{pmatrix} \cdot \begin{pmatrix}\mathbf{x}_1 \cdot \mathbf{w} - y_1 \\ \mathbf{x}_2 \cdot \mathbf{w} - y_2 \\ \cdots \\ \mathbf{x}_N \cdot \mathbf{w} - y_N\end{pmatrix}$$

Để ý chút thì nếu mình gọi $$\mathbf{X}$$ là ma trận với các hàng là mỗi $$\mathbf{x}_i$$​, và $$\mathbf{y}$$​ là vector cột với các $$y_i$$​, nghĩa là $$\mathbf{X} = \begin{pmatrix}\mathbf{x}_1 \\ \mathbf{x}_2 \\ \cdots \\ \mathbf{x}_t\end{pmatrix}$$​ và $$y = \begin{pmatrix}y_1 \\ y_2 \\ \cdots \\ y_t\end{pmatrix}$$​ thì mình có$$\begin{pmatrix}\mathbf{x}_1 \cdot \mathbf{w} - y_1 \\ \mathbf{x}_2 \cdot \mathbf{w} - y_2 \\ \cdots \\ \mathbf{x}_t \cdot \mathbf{w} - y_t\end{pmatrix} = \mathbf{X} \mathbf{w} - \mathbf{y}$$.

Mình cần hệ phương trình các đạo hàm riêng đều bằng $$0$$​, tương đương với việc vector $$\begin{bmatrix}\frac{\partial\mathcal{L}}{\partial w_0} \\ \frac{\partial \mathcal{L}}{\partial w_1} \\ \cdots \\ \frac{\partial \mathcal{L}}{\partial w_t}\end{bmatrix} = \begin{pmatrix} 1 & 1 & \cdots & 1 \\ x_{11} & x_{21} & \cdots & x_{N1} \\ x_{12} & x_{22} & \cdots & x_{N2} \\ \cdots & \cdots & \cdots & \cdots \\ x_{1t} & x_{2t} & \cdots & x_{Nt}\end{pmatrix} \cdot (\mathbf{X} \mathbf{w} - \mathbf{y}) = \mathbf{X}^{T} \cdot (\mathbf{X} \mathbf{w} - \mathbf{y}) = \mathbf{0}$$

Ở đây $$\mathbf{X}^T$$​ là chuyển vị (transpose) của ma trận $$\mathbf{X}$$​. Như vậy nghiệm của hệ phương trình trên (theo $$\mathbf{w}$$​) là nghiệm của bài toán.

Như đã nói, ta cần giải hệ phương trình $$\mathbf{X}^T \mathbf{X} \mathbf{w} - \mathbf{X}^T \mathbf{y} = \mathbf{0}$$. Đặt $$\mathbf{X}^T \mathbf{X} = A$$​ và $$\mathbf{X}^T \mathbf{y}=b$$ thì $$\mathbf{A} \mathbf{w} = \mathbf{b}$$. Thông thường chúng ta sẽ tìm nghịch đảo của $$\mathbf{A}$$​ rồi từ đó suy ra nghiệm, tuy nhiên nếu đã học môn Đại số tuyến tính hẳn các bạn cũng biết là hệ phương trình có thể có nghiệm duy nhất, vô nghiệm, vô số nghiệm. Ở 2 trường hợp sau sẽ không tìm được nghịch đảo, khi đó chúng ta dùng khái nghiệm **giả nghịch đảo** (**pseudo inverse**) và ký hiệu giả nghịch đảo của ma trận $$\mathbf{A}$$​ là $$\mathbf{A}^+$$​. Như vậy $$\mathbf{w} = \mathbf{A}^+ \mathbf{b}$$​.
