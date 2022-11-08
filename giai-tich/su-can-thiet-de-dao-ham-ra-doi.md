# Sự cần thiết để đạo hàm ra đời

Trên thế giới có rất nhiều đạo. Mình (cũng như nhiều thế hệ học sinh, sinh viên khác) đã dành thanh xuân của bản thân cho đạo ..... hàm :))))

Chúng ta hãy cùng ôn lại kỷ niệm với người bạn _đạo hàm_ này nhé :))))

**Hiện tượng vật lý**: xét sự chuyển động của chất điểm. Để đơn giản mình xét sự chuyển động trên trục $$Ox$$ với vị trí được biểu diễn bằng tọa độ trên trục.

Xét sự chuyển động của chất điểm từ vị trí $$s_1$$ (vào thời điểm $$t_1$$) tới vị trí $$s_2$$ (vào thời điểm $$t_2$$). Vận tốc của chất điểm lúc này là $$v = \frac{s_2-s_1}{t_2-t_1}$$ khi phân bổ đều trên toàn đoạn đường. Chúng ta thường ký hiệu sự biến thiên (sau và trước) của một đại lượng bằng chữ cái Hy Lạp **delta** $$\Delta$$. Ở đây $$v = \frac{\Delta s}{\Delta t}$$.

Vấn đề ở đây là, chúng ta thường quan tâm vận tốc tức thời tại 1 thời gian nhất định, điều vốn dĩ là vô lý vì chất điểm phải chuyển động một quãng đường thì mới có vận tốc chứ? Một cách khắc phục là khiến sự chênh lệch thời gian là rất nhỏ, hay nói cách khác, $$\Delta t \rightarrow 0$$.

Trong nhiều trường hợp, tọa độ chuyển động của chất điểm được biểu diễn bằng hàm theo thời gian, nghĩa là $$y=f(t)$$. Lúc này vận tốc tức thời là $$v = \frac{\Delta f(t)}{\Delta t}$$ khi $$\Delta t \rightarrow 0$$.

Còn rất nhiều ví dụ thực tế về vật lý mà đại lượng chúng ta cần tìm có dạng $$\frac{\Delta y}{\Delta x}$$ khi $$\Delta x \rightarrow 0$$. Từ đây nhu cầu về một khái niệm cho phép chúng ta tính được giá trị của đại lượng có dạng trên ra đời. Anh bạn này được gọi là **đạo hàm** (**derivative**).

### 1. Định nghĩa đạo hàm

Đạo hàm của hàm $$y=f(x)$$ tại điểm $$x=x_0$$ là giới hạn:

$$\lim_{x\to x_0}\frac{f(x)-f(x_0)}{x-x_0}$$

Nếu giới hạn trên tồn tại, ta nói $$f(x)$$ _khả vi_ (_differentiable_) tại điểm $$x=x_0$$ và ký hiệu $$f'(x_0) = \displaystyle{\lim_{x\to x_0}\frac{f(x)-f(x_0)}{x-x_0}}$$.

Nếu hàm số khả vi tại tất cả điểm trên khoảng $$(a, b)$$, ta nói $$f(x)$$ _khả vi trên khoảng_ $$(a, b)$$.

**Ví dụ 1**. Xét hàm số $$f(x) = x^2 + x + 3$$. Tính đạo hàm tại $$x_0 = 1$$.

Ta có $$f(x) - f(x_0) = x^2 + x + 3 - (1^2 + 1 + 3) = x^2 + x - 2$$.

Suy ra $$\frac{f(x)-f(x_0)}{x-x_0} = \frac{x^2 + x - 2}{x - 1} = x+2$$.

Vậy $$f'(1) = \displaystyle{\lim_{x \to 1} x+2 = 3}$$.

**Một số cách ký hiệu khác**

Đặt $$\Delta y = f(x)-f(x_0)$$. Khi đó $$\Delta y$$ được gọi là _số gia_ của hàm $$f(x)$$.

Đặt $$\Delta x = x - x_0$$. Đạo hàm được viết lại $$f'(x_0) = \displaystyle{\lim_{\Delta x \to 0} \frac{\Delta y}{\Delta x}}$$.

**Ví dụ 2**. Xét hàm số $$f(x) = x^3$$. Tính đạo hàm của hàm số trên $$\mathbb{R}$$.

Với mọi $$x_0 \in \mathbb{R}$$, ta có:

$$f(x) - f(x_0) = x^3 - x_0^3$$. Suy ra $$\frac{f(x)-f(x_0)}{x-x_0} = \frac{x^3 - x_0^3}{x - x_0} = \frac{(x-x_0)(x^2 + x x_0 + x_0^2)}{x - x_0} = x^2 + x x_0 + x_0^2$$.

Do đó $$f'(x_0) = \displaystyle{\lim_{x \to x_0} (x^2 + x x_0 + x_0^2)} = 3x_0^2$$.

Ta thấy rằng $$x_0$$ có thể nhận tất cả giá trị trên $$\mathbb{R}$$ nên thay $$x_0$$ thành $$x$$ ta có đạo hàm của $$f(x)=x^3$$ trên $$\mathbb{R}$$ là $$f'(x)=3x^2$$.
