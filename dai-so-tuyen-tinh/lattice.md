# Lattice

Lattice là chủ đề rất hot trong các thuật toán mã hóa hậu lượng tử (post-quantum) nhưng mình chỉ đề cập những điều nền tảng phục vụ giải các bài CTF cũng ở mức nền tảng :))))

**Định nghĩa 1**. Cho $$m, n > 0$$. Gọi $$\bm{b_1}, \cdots, \bm{b_n} \in \mathbb{R}^m$$​ độc lập tuyến tính. Khi đó lattice được span bởi các vector trên là $$L(\bm{b_1}, \cdots, \bm{b_n}) = \Big\{\displaystyle{\sum_{i=1}^n x_i \bm{b_i}} : x_i \in \mathbb{Z}\Big\} = \sum \mathbb{Z} \bm{b_i}$$

Nếu $$n = m$$​ thì ta nói lattice **full-rank**.

Nếu $$\bm{b_i} \in \mathbb{Z}^m$$​ thì lattice là **solid integral**.

**Định nghĩa 2**. Lattice là một discrete subgroup của $$(\mathbb{R}^m, +)$$.

**Bổ đề**. Hai định nghĩa trên về lattice là tương đương nhau.

