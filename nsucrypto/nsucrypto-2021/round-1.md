# Round 1

### Problem 3. A space message

Bài này có 4 kiểu ký tự.

* Loại 1: bình thường (noun)
* Loại 2: lật ngược loại 1 theo trục dọc (nuon)
* Loại 3: lật ngược loại 1 theo trục ngang (uonu)
* Loại 4: lật ngược loại 3 theo trục dọc (unou)

Tìm các ký tự theo từng loại mình có:

* Đối với loại 1: the, re, is, no, si, gnal. Như vậy message là "There is no signal".
* Đối với loại 2: cosmos, com, pa, sends, ssi, signals, on, to us. Như vậy message là "Cosmos compassion sends signals to us".
* Đối với loại 3 (viết từ dưới lên): cosmos, is, empty. Như vậy message là "Cosmos is empty".
* Đối với loại 4 (cũng ghi từ dưới lên): no, si, gnal, is, no, sig, nal, there. (có dấu chấm). Như vậy message là "no signal is no signal there".

Đáng tiếc là message cuối cùng khi kết hợp 4 message trên sai nên không được trọn điểm :((((

Đáp án của BTC là:

_cosmos sends signals to us:_

_compassion_

_there is no signal_

_cosmos is empty_

_there is no signal_

_no signal_

### 4. Elliptic Curve Points

Bài này mình không giải ra nhưng hóa ra lại không quá phức tạp :(( huhu

**Đề bài**. Cho đường cong elliptic trên $$\mathbb{F}_p$$​:

$$E(\mathbb{F}_p) = \{(x, y) \in \mathbb{F}_p^2: y^2 = x^3 + ax + b\} \cup \{ \mathcal{O} \}$$

Giả sử $$b=0$$​. Gọi $$R \in E(\mathbb{F}_p)$$ là điểm thuộc đường cong có order lẻ và $$R \neq \mathcal{O}$$. Gọi $$H = \langle R \rangle$$ là subgroup sinh bởi $$R$$​.

Chứng minh rằng, nếu điểm $$(u, v) \in H$$​ thì $$u$$​ là số chính phương modulo $$p$$​ (quadratic residue).

**Giải**. Gọi $$Q = (x', y') \in H$$. Do $$R$$​ có order lẻ nên $$Q$$​ có order lẻ là $$n$$ (vì order của $$Q$$​ là ước của order của $$R$$). Xét điểm $$P = \frac{n+1}{2} Q$$​, do $$n$$​ lẻ nên dễ thấy $$P \in H$$​. Đặt $$P = (x, y)$$​.

Do $$2P = (n+1)Q = Q$$​ ($$Q$$​ có order là $$n$$​) nên theo công thức cộng 2 điểm trên elliptic thì:

$$\begin{align*}x' & = \Big(\frac{3x^3 + a}{2y}\Big)^2-2x \\& =\frac{9x^2+6x^2a + a^2 - 8xy^2}{(2y)^2} \\ & = \frac{9x^4 + 6x^2 a + a^2 - 8x(x^3 + ax)}{(2y^2)} \\ & = \frac{x^4-2x^2a + a^2}{(2y)^2} \\ & = \Big(\frac{x^2-a}{2y}\Big)^2\end{align*}$$

Như vậy $$x'$$ là số chính phương modulo $$p$$ và ta có điều phải chứng minh.​
