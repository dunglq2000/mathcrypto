# Kernel và homomorphism trên vành

Xét vành $$(R, +, \cdot)$$. Khi đó:

* với mọi $$a \in R$$, $$a \cdot 0 = 0 \cdot a = 0$$
* $$(-a) \cdot b = - (a \cdot b)$$

**Định nghĩa 1**. Giả sử ta có 2 vành là $$(R_1, +, \cdot)$$ và $$(R_2, \boxplus, \odot)$$. Xét hàm $$f: \, R_1 \mapsto R_2$$. Khi đó $$f$$ được gọi là **homomorphism** trên 2 vành nếu $$f$$ là homomorphism trên phép cộng và phép nhân. Nghĩa là:

* với mọi $$a, b \in R_1$$, $$f(a) \boxplus f(b) = f(a + b)$$
* với mọi $$a, b \in R_1$$, $$f(a) \odot f(b) = f(a \cdot b)$$

**Định nghĩa**. Nhân (**kernel**) của $$f$$ là $$\text{Ker} f = \{x \vert x \in R_1, f(x) = 0_{2}\}$$ với $$0_{2}$$ là phần tử $$0$$ của $$R_2$$.

**Định lý**. $$\text{Ker} f$$ là một ideal của $$R_1$$.

**Chứng minh**. Ta có $$f(0_1) = 0_2$$ theo định nghĩa homomorphism. Do đó

Với mọi $$a \in R_1$$ và với mọi $$b \in \text{Ker} f$$ thì $$f(a) \odot f(b) = f(a) \odot 0_2 = 0_2 = f(a \cdot b)$$. Do đó $$a \cdot b \in \text{Ker} f \Leftrightarrow R \cdot \text{Ker} f \subseteq \text{Ker} f$$.

Tương tự $$\text{Ker} \cdot R \subseteq \text{Ker} f$$

Do đó $$\text{Ker} f$$ là ideal của $$R$$.
