# Tác động nhóm

Cho tập hợp $$M$$ có hữu hạn phần tử và nhóm hữu hạn $$G$$.

**Định nghĩa 1**. **Orbit**. Tập con $$G(m) = \{gm \, \vert \, g \in G\} \subset M$$ được gọi là **orbit** của phần tử $$m \in M$$.

Khi đó, **tác động nhóm** của $$G$$ lên tập $$M$$ là quan hệ tương đương, nghĩa là:

Với mọi $$n, m \in M$$, ta nói $$n$$ có quan hệ với $$m$$, được ký hiệu là $$n \widetilde{G} m$$, khi và chỉ khi tồn tại $$g \in G: gn = m$$. Khi đó $$G(n) = G(m)$$.

Nếu các phần tử trong $$M$$ tạo thành các lớp tương đương theo quan hệ trên thì

$$M = G(m_1) \cup G(m_2) \cup \cdots \cup G(m_k)$$ với $$(m_i, m_j)$$ không tương đương nhau đôi một.

**Định nghĩa 2**. **Stabilizer**. Tập con $$G_m = \{g \in G \, \vert \, gm = m\} \subset G$$ được gọi là **stabilizer** của phần tử $$m \in M$$.

**Nhận xét**. Ta thấy $$\lvert Gm \rvert = [G, G_m]$$, hay $$\lvert Gm \rvert = \frac{\lvert G \rvert}{\lvert G_m \rvert}$$. Từ đó $$\lvert G \rvert = \lvert G_m \rvert \cdot \lvert Gm \rvert$$.

**Nhận xét 2**. Hai lớp tương đương hoặc rời nhau, hoặc trùng nhau

$$G(m_1) \cap G(m_2) = \begin{cases}G(m_1) \equiv G(m_2) \\ \emptyset\end{cases}$$
