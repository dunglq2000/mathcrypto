# Các loại morphism

Cho 2 nhóm $$(G, \star)$$ và $$(H, \cdot)$$.

### 1. Homomorphism

**Định nghĩa 1**. Hàm $$f: G \rightarrow H$$ được gọi là **homomorphism** nếu với mọi $$g_1, g_2 \in G$$ thì $$f(g_1) \cdot f(g_2) = f(g_1 \star g_2)$$.

**Tính chất**:

* Gọi $$e_G, e_H$$ lần lượt là phần tử đơn vị của $$G$$ và $$H$$. Khi đó $$f(e_G) = e_H$$.
* Với mọi $$g \in G$$, $$f(g^{-1}) = f(g)^{-1}$$.

### 2. Isomorphism

**Định nghĩa 2**. Hàm $$f: G \rightarrow H$$ được gọi là **isomorphism** nếu nó là song ánh và là homomorphism. Nghĩa là $$f$$ song ánh và với mọi $$g_1, g_2 \in G$$ thì $$f(g_1) \cdot f(g_2) = f(g_1 \star g_2)$$.

**Tính chất**: giống homomorphism nhưng ở đây là map 1-1 (song ánh).

### 3. Automorphism

**Định nghĩa 3**. Hàm $$f: G \rightarrow G$$ được gọi là **automorphism** nếu nó là song ánh lên chính nó.

### Định lý Cayley

**Định lý Cayley**. Mọi nhóm hữu hạn có $$n$$ phần tử đều isomorphic với nhóm con của nhóm hữu hạn $$\mathcal{S}_n$$.
