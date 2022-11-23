# Nhóm hoán vị

Nhóm hoán vị, hay Permutation Group, đóng vai trò quan trọng trong lý thuyết nhóm lẫn lý thuyết số, và nhiều lý thuyết khác vượt khỏi trình của tác giả bài viết này :v

**Định nghĩa**. Cho tập hợp $$A = \{1, 2, \cdots, n\}$$. Một hoán vị của tập $$A$$ là một cách sắp xếp $$n$$ phần tử đó theo một **trật tự** nhất định. Như vậy theo quy tắc nhân của tổ hợp, nếu tập hợp $$A$$ có $$n$$ phần tử thì sẽ có $$n!$$ hoán vị.

Ví dụ với $$n=3$$ thì các hoán vị là $$(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)$$ (có $$6 = 3!$$ hoán vị).

**Nhận xét**. Một hoán vị là một song ánh từ $$\{1, 2, \cdots, n\}$$ tới $$\{1, 2, \cdots, n\}$$.

Với trật tự ban đầu là $$(1, 2, 3)$$, mỗi hoán vị trong 6 hoán vị sẽ được viết lại như sau:

$$(1, 2, 3) \Leftrightarrow \begin{pmatrix}1 & 2 & 3 \\ 1 & 2 & 3\end{pmatrix}$$

$$(1, 3, 2) \Leftrightarrow \begin{pmatrix}1 & 2 & 3 \\ 1 & 3 & 2\end{pmatrix}$$

$$(2, 1, 3) \Leftrightarrow \begin{pmatrix}1 & 2 & 3 \\ 2 & 1 & 3\end{pmatrix}$$

$$(3, 3, 1) \Leftrightarrow \begin{pmatrix}1 & 2 & 3 \\ 2 & 3 & 1\end{pmatrix}$$

$$(3, 1, 2) \Leftrightarrow \begin{pmatrix}1 & 2 & 3 \\ 3 & 1 & 2\end{pmatrix}$$

$$(3, 2, 1) \Leftrightarrow \begin{pmatrix}1 & 2 & 3 \\ 3 & 2 & 1\end{pmatrix}$$

Tập hợp tất cả các hoán vị của tập $$A = \{1, 2, \cdots, \}$$ cùng với toán tử hợp tạo thành nhóm. Nhóm này gọi là nhóm hoán vị (Symmetric Group hay Permutation Group). Toán tử hợp ở đây là biến đổi nối tiếp 2 hoán vị.

Với ví dụ trên, đặt $$\sigma = \begin{pmatrix}1 & 2 & 3 \\ 2 & 3 & 1\end{pmatrix}$$ và $$\tau = \begin{pmatrix}1 & 2 & 3 \\ 3 & 1 & 2\end{pmatrix}$$ thì $$\sigma \star \tau$$ được tính như sau:

* $$1 \xrightarrow{\sigma} 2 \xrightarrow{\tau} 1$$
* $$2 \xrightarrow{\sigma} 3 \xrightarrow{\tau} 2$$
* $$3 \xrightarrow{\sigma} 1 \xrightarrow{\tau} 1$$

Như vậy $$\sigma \star \tau = \begin{pmatrix}1 & 2 & 3 \\ 1 & 2 & 3\end{pmatrix}$$.

**Tổng quát**. Nhóm hoán vị trên tập $$n$$ phần tử được ký hiệu là $$\mathcal{S}_n$$.

* Phần tử đơn vị của nhóm này là hoán vị đồng nhất, tức là $$\begin{pmatrix} 1 & 2 & \cdots & n \\ 1 & 2 & \cdots & n\end{pmatrix}$$
* Phần tử nghịch đảo luôn tồn tại (chỉ cần viết ngược thứ tự)
* Tính kết hợp

**Nhận xét**. Quan trọng ở thứ tự biến đổi, miễn không làm thay đổi nó thì viết sao cũng được.

Ví dụ $$\begin{pmatrix} 1 & 2 & 3 & 4 \\ 2 & 4 & 1 & 3\end{pmatrix}$$ tương đương với $$\begin{pmatrix}2 & 4 & 3 & 1 \\ 4 & 3 & 1 & 2\end{pmatrix}$$ (vì $$1 \mapsto 2, 2 \mapsto 4, 3 \mapsto 1, 4 \mapsto 3$$).
