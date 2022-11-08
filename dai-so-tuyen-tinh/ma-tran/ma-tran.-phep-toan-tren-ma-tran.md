# Ma trận. Phép toán trên ma trận

2 khái niệm cơ bản của đại số tuyến tính là ma trận (matrix) và vector.

### **1. Vector**

Ở cấp 3 mình được học về tích vô hướng của 2 vector trong $$Oxy$$ và $$Oxyz$$. Tổng quát lên cho bộ $$n$$ số, giả sử $$\bm{a} = (a_1, a_2, \cdots, a_n)$$ và $$\bm{b} = (b_1, b_2, \cdots, b_n)$$. Khi đó tích của 2 vector trên là $$\bm{a} \cdot \bm{b} = a_1 b_1 + a_2 b_2 + \cdots a_n b_n$$.

### **2. Ma trận và các phép toán trên ma trận**

Một ma trận $$a_{m \times n}$$ là một bảng gồm $$m$$ hàng và $$n$$ cột.

$$\begin{pmatrix}a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \cdots & \cdots & \cdots & \cdots \\ a_{m1} & a_{m2} & \cdots & a_{mn}\end{pmatrix}$$

Trong đó $$a_{ij}$$ biểu diễn phần tử tại hàng $$i$$ và cột $$j$$. Khi $$m=n$$ thì ta gọi là **ma trận vuông**.

#### a. Phép cộng ma trận

Để cộng/trừ 2 ma trận $$a_{m \times n}$$ và $$b_{m \times n}$$ thì ta cộng/trừ các phần tử tương ứng, tức là $$a_{ij} \pm b_{ij}$$. Như vậy để cộng 2 ma trận thì **KÍCH THƯỚC** phải bằng nhau.

#### b. Phép nhân ma trận

Để nhân ma trận, giả sử $$c_{m \times p} = a_{m \times n} \cdot b_{n \times p}$$ (chú ý rằng để nhân ma trận thì **số cột ma trận trước phải bằng số hàng ma trận sau**, lý do thì sau đây mình sẽ giải thích)

Phần tử $$c_{ij}$$ được tính như sau: $$c_{\textbf{ij}} = \displaystyle{\sum_{k=1}^{n}a_{\textbf{i}k} b_{k\textbf{j}}}$$. Nghĩa là phần tử ở hàng $$i$$ và cột $$j$$ của $$c$$ là tích vector hàng $$i$$ của $$a$$ và vector cột $$j$$ của $$b$$.

$$\begin{pmatrix}\cdots & \cdots & \cdots \\ \cdots & c_{ij} & \cdots \\ \cdots & \cdots & \cdots\end{pmatrix} = \begin{pmatrix}\cdots & \cdots & \cdots & \cdots \\ a_{i1} & a_{i2} & \cdots & a_{in} \\ \cdots & \cdots & \cdots & \cdots\end{pmatrix} \cdot \begin{pmatrix}\cdots & b_{1j} & \cdots \\ \cdots & b_{2j} & \cdots \\ \cdots & \cdots & \cdots \\ \cdots & b_{nj} & \cdots\end{pmatrix}$$

### 3. Một số loại ma trận đặc biệt

#### a. Ma trận đường chéo chính

Đường chéo chính của ma trận vuông $$a_{n \times n}$$ là các phần tử $$a_{ii}$$ với $$i = 1, \cdots, n$$.

Ma trận đường chéo chính có tất cả phần tử không nằm trên đường chéo chính bằng 0. Ví dụ:

$$\bm{A} = \begin{pmatrix}1 & 0 & 0 & 0 \\ 0 & 2 & 0 & 0 \\ 0 & 0 & 3 & 0 \\ 0 & 0 & 0 & 4 \end{pmatrix}$$

#### b. Ma trận đơn vị (Identity)

Ma trận đơn vị kích thước $$n \times n$$ có dạng

$$\bm{I_n} = \begin{pmatrix}1 & 0 & \cdots & 0 & 0 \\ 0 & 1 & \cdots & 0 & 0 \\ \cdots & \cdots & \cdots & \cdots & \cdots \\ 0 & 0 & \cdots & 0 & 1\end{pmatrix}_{n \times n}$$

Như vậy ma trận đơn vị là một trường hợp riêng của ma trận đường chéo chính.

Tính chất của ma trận đơn vị: với mọi ma trận vuông $$\bm{A}$$ thì $$\bm{I} \cdot \bm{A} = \bm{A} \cdot \bm{I} = \bm{A}$$ (có thể dễ dàng kiểm chứng bằng phép nhân ma trận).

#### c. Ma trận tam giác trên/dưới

Ma trận tam giác trên có tất cả các phần tử dưới đường chéo chính bằng 0. Ví dụ:

$$\begin{pmatrix}1 & 1 & 4 & 8 \\ 0 & 3 & 0 & 5 \\ 0 & 0 & 5 & 7 \\ 0 & 0 & 0 & 10\end{pmatrix}$$

Tương tự, ma trận tam giác dưới có tất cả phần tử trên đường chéo chính bằng 0.

#### d. Ma trận bậc thang (Echelon form)

**Định nghĩa**. Ma trận bậc thang là ma trận mà phần tử khác 0 đầu tiên của mỗi hàng nằm bên phải phần tử khác 0 đầu tiên của hàng trên nó. Ví dụ:

$$\begin{pmatrix}3 & 0 & 4 & 5 \\ 0 & 1 & 2 & 2 \\ 0 & 0 & 0 & 4\end{pmatrix}$$ hoặc $$\begin{pmatrix}1 & 1 & 4 & 4 \\ 0 & 1 & 0 & 1 \\ 0 & 0 & 5 & 5 \\ 0 & 0 & 0 & 10\end{pmatrix}$$

Ở ma trận đầu, phần tử khác 0 đầu tiên của hàng đầu tiên là 3, phần tử khác 0 đầu tiên của hàng thứ hai là 1 (nằm ở cột bên phải số 3), phần tử khác 0 đầu tiên của hàng thứ ba là 4 (nằm ở cột bên phải số 1).
