# Nhóm con (Subgroup). Phần tử sinh (Generator)

Cho nhóm $$(G, \star)$$​. Một tập hợp con $$H$$ của $$G$$ được gọi là nhóm con nếu các phần tử của nó đóng trên $$H$$​. Nghĩa là với mọi $$h_1, h_2 \in H$$thì $$h_1 \star h_2 \in H$$​.

Nếu $$H = \{e\}$$​ thì $$H$$​ được gọi là **nhóm con tầm thường** (trivial subgroup) của $$G$$​.

Nếu $$H \subsetneq G$$​, tức $$H$$ là **tập con thực thụ** của $$G$$​ thì $$H$$ được gọi là **nhóm con thực thụ** (proper subgroup) của $$G$$​.

**Định nghĩa về lũy thừa**. Xét $$g \in G$$​. Ta thực hiện toán tử $$k$$​ lần và ký hiệu lũy thừa như sau:

$$g \star g \star \cdots \star g = g^k$$

Ký hiệu $$g^0=e$$​ và $$g^{-n} = (g^{-1})^n$$.&#x20;

Ta viết $$\langle g \rangle = \{g^0, g^1, \cdots, \}$$​ là tập hợp tất cả các lũy thừa của $$g$$​.&#x20;

Dễ thấy $$\langle g \rangle$$ là một nhóm con của $$G$$. Nếu $$\langle g \rangle = G$$​ thì ta nói $$g$$​ là **phần tử sinh** (generator) của nhóm $$G$$.

Ví dụ: nhóm $$(\mathbb{Z}, +)$$​ gồm tập hợp các số nguyên và phép cộng số nguyên tạo thành một nhóm với phần tử sinh là $$1$$​.

Ví dụ: nhóm $$2\mathbb{Z} = \{\cdots, -4, -2, 0, 2, 4, \cdots, \}$$​ với phép cộng số nguyên cũng tạo thành nhóm với phần tử sinh là $$2$$​. Ta thấy rằng nhóm $$2\mathbb{Z}$$ là nhóm con của $$\mathbb{Z}$$​.
