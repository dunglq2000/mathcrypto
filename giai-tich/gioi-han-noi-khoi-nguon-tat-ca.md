# Giới hạn, nơi khởi nguồn tất cả

Một vĩ nhân từng nói: **Bước đi ngàn dặm, khởi đầu một bước chân**.

Giới hạn (Limit) là khái niệm cơ sở trong giải tích. Chúng ta xem xét một chút nhé :))

Khi Cauchy định nghĩa lại giới hạn theo ngôn ngữ $$\delta - \varepsilon$$ đã gây ra những làn sóng tranh cãi dữ dội nhưng đồng thời cũng làm mới hoàn toàn cái nhìn của mọi người về giải tích, bây giờ mình sẽ ngồi mổ xẻ, săm soi chúng :))))

Xét dãy số $$\{a_n\}$$ gồm các số $$a_1, a_2, \cdots$$. Dãy số có thể được biểu diễn bởi công thức tổng quát, công thức truy hồi, không có công thức chung, ...

### 1. Giới hạn dãy số

**Định nghĩa 1.1**. Dãy số $$\{a_n\}$$ được gọi là **có giới hạn hữu hạn** $$L$$ nếu:

Với mọi số $$\varepsilon > 0$$, tồn tại $$n_0 > 0$$ sao cho với mọi $$n \geq n_0$$ thì $$\vert a_n - L \vert < \varepsilon$$.

Một cách hình ảnh, trên trục $$Ox$$ ta vẽ đường tròn tâm $$L$$ và bán kính $$\varepsilon$$ rất nhỏ. Khi đó tất cả các số hạng của dãy số kể từ số hạng nào đó sẽ luôn nằm trong hình tròn này. Khi $$\varepsilon$$ cực kì nhỏ, các số hạng của dãy số về sau gần như nằm sát $$L$$ (có thể đạt hoặc không đạt $$L$$).

**Định nghĩa 1.2**. Dãy số $$\{a_n\}$$ được gọi là **có giới hạn vô hạn** nếu:

Với mọi số $$M > 0$$, tồn tại $$n_0 > 0$$ sao cho với mọi $$n \geq n_0$$ thì $$\vert a_n \vert > M$$.

Ở trường hợp này, khi ta chọn số $$M$$ dương rất lớn bất kì, thì tất cả số hạng của dãy số kể từ số hạng nào đó luôn lớn hơn $$M$$.

**Ví dụ**. Dãy số $$\{a_n\}$$ cho bởi công thức $$a_n = \frac{1}{n}$$ có giới hạn là 0. Dãy số $$\{b_n\}$$ cho bởi công thức $$b_n = n^2$$ có giới hạn vô hạn.

**Chứng minh**.

a) Xét dãy số $$a_n = \frac{1}{n}$$.

Ta sẽ chứng minh dãy trên có giới hạn là $$0$$. Muốn vậy, với mọi $$\varepsilon > 0$$, ta cần tìm số $$n_0$$ nhỏ nhất sao cho $$\Bigl\lvert \frac{1}{n_0} - 0 \Bigr\rvert < \varepsilon$$.

Tương đương với $$\frac{1}{n_0} < \varepsilon \Leftrightarrow n_0 > \frac{1}{\varepsilon}$$. Tức là $$n_0 \geq \Bigl \lceil \frac{1}{\varepsilon} \Bigr \rceil$$.

Vậy theo định nghĩa, với mọi số $$\varepsilon > 0$$ thì ta luôn tìm được $$n_0$$ thỏa bất đẳng thức trên, nên dãy có giới hạn là 0.

b) Xét dãy số $$b_n = n^2$$.

Ta sẽ chứng minh dãy trên có giới hạn vô cực. Như vậy, với mọi $$M > 0$$ ta tìm số $$n_0$$ nhỏ nhất để $$b_{n_0} > M$$.

Dễ thấy rằng khi $$b_{n_0} > M \Leftrightarrow n_0^2 > M$$. Tương đương $$n_0 > \sqrt{M}$$. Vậy $$n_0 \geq \lceil \sqrt{M} \rceil$$.

Theo định nghĩa, với mọi số $$M > 0$$ thì ta tìm được $$n_0$$ thỏa bất đẳng thức trên, nên dãy có giới hạn vô cực.

### 2. Giới hạn hàm số

Cơ bản thì giới hạn hàm số khá giống giới hạn dãy số.

**Định nghĩa 2.1**. Cho hàm số $$f(x)$$. Xét điểm $$x_0$$. Ta nói **hàm số có giới hạn hữu hạn** $$L$$ **khi** $$x$$ **tiến về** $$x_0$$ nếu:

Với mọi $$\varepsilon > 0$$, tồn tại $$\delta > 0$$ sao cho với mọi $$x$$ mà $$\vert x - x_0 \vert < \delta$$ thì $$\vert f(x) - L \vert < \varepsilon$$.

**Ký hiệu**: $$\displaystyle{\lim_{n \to \infty}} a_n = L$$.

Lúc này chúng ta tưởng tượng trên mặt phẳng 2 chiều $$Oxy$$. $$Ox$$ biểu diễn các giá trị của tập xác định $$x$$ còn $$Oy$$ biểu diễn các giá trị của $$f(x)$$. Khi đó nếu ta chọn một số $$\varepsilon$$ nhỏ bất kì và vẽ đường tròn với tâm ở $$(x_0, L)$$, bán kính $$\varepsilon$$, thì khi $$x$$ càng gần với $$x_0$$, giá trị $$f(x)$$ tương ứng sẽ càng gần với $$L$$. Ở đây $$\delta$$ thường có liên hệ với $$\varepsilon$$ bằng một cách nào đó.

**Định nghĩa 2.2**. Cho hàm số $$f(x)$$. Xét điểm $$x_0$$. Ta nói **hàm số có giới hạn vô cực khi** $$x$$ **tiến về** $$x_0$$ nếu:

Với mọi $$M > 0$$, tồn tại $$\delta > 0$$ sao cho với mọi $$x$$ mà $$\vert x - x_0 \vert < \delta$$ thì $$\vert f(x) \vert > M$$.

Ở đây dấu giá trị tuyệt đối biểu thị rằng $$f(x)$$ có thể tiến về dương vô cực lẫn âm vô cực tùy trường hợp.

**Ký hiệu**: $$\displaystyle{\lim_{x \to x_0}} f(x) = \infty$$.

**Định nghĩa 2.3**. Cho hàm số $$f(x)$$. Ta nói **hàm số có giới hạn hữu hạn** $$L$$ **khi** $$x$$ **tiến ra dương vô cực** nếu:

Với mọi $$\varepsilon > 0$$, tồn tại $$M > 0$$ sao cho với mọi $$x$$ mà $$x > M$$ thì $$\vert f(x) - L \vert < \varepsilon$$.

**Ký hiệu**: $$\displaystyle{\lim_{x \to \infty}} f(x) = L$$.

**Định nghĩa 2.4**. Cho hàm số $$f(x)$$. Ta nói **hàm số có giới hạn vô cực khi** $$x$$ **tiến ra dương vô cực** nếu:

Với mọi $$M > 0$$, tồn tại $$M' > 0$$ sao cho với mọi $$x$$ mà $$x > M'$$ thì $$\vert f(x) \vert > M$$.

**Ký hiệu**: $$\displaystyle{\lim_{x \to \infty}} f(x) = \infty$$.

Các định nghĩa khi $$x$$ tiến ra âm vô cực cũng tương tự.

### 3. Giới hạn một bên

Đối với hàm số, đôi khi chúng ta chỉ xét việc tiến về một bên của $$x_0$$ (nếu $$x$$ tiến tới $$x_0$$ từ bên trái tức là $$x \leq x_0$$, ngược lại thì $$x \geq x_0$$).

Khi $$x$$ tiến tới $$x_0$$ từ bên trái ta ký hiệu là $$\displaystyle{\lim_{x \to x_0^-} f(x)}$$. Quay lại định nghĩa giới hạn bên trên, số $$\delta$$ chỉ cần $$x - x_0 > -\delta \Leftrightarrow x_0 - x < \delta$$.

Khi $$x$$ tiến tới $$x_0$$ từ bên phải ta ký hiệu là $$\displaystyle{\lim_{x \to x_0^+} f(x)}$$. Theo định nghĩa thì $$x - x_0 < \delta$$.

### 4. Liên tục

Một điều cần lưu ý là ở định nghĩa không nhất thiết có dấu bằng (=) trong các bất phương trình. Nghĩa là giới hạn của dãy số (hàm số) có thể là một giá trị mà dãy số (hàm số) không thể đạt tới được, chỉ tiến về đó thôi. Ví dụ dãy $$a_n = \frac{1}{n}$$ có giới hạn là 0 nhưng không tồn tại $$n$$ để $$\frac{1}{n}$$ bằng chính xác 0.

**Định nghĩa 4.1**. Hàm số $$f(x)$$ được gọi là **liên tục** tại điểm $$x_0$$ nếu:

$$\displaystyle{\lim_{x \to x_0} f(x) = f(x_0)}$$

Theo định nghĩa, hàm số sẽ _không liên tục_ khi một trong các điều kiện sau xảy ra:

* Giới hạn hàm số tại $$x_0$$ không tồn tại (không có giới hạn hoặc giới hạn phải khác giới hạn trái).
* Hàm số không xác định tại $$x_0$$.
* Hàm số xác định tại $$x_0$$ và có giới hạn tại $$x_0$$ nhưng 2 giá trị này khác nhau.

**Ví dụ**. Hàm số $$f(x)=\frac{1}{x}$$ có giới hạn $$\displaystyle{\lim_{x \to x_0^+} f(x) = +\infty}$$ và $$\displaystyle{\lim_{x \to x_0^-} f(x) = -\infty}$$.

Những khái niệm này đều được học ở chương trình phổ thông và đại học nên mình chỉ nhắc lại gọn nhẹ :)))) Tuy nhiên lại rất quan trọng nên mình cần nhắc lại trước khi đi tới các vấn đề sau.
