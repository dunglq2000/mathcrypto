# Trường nguyên tố

Trường số nguyên tố $$GF(p)$$​ (với $$p$$​ là số nguyên tố) sẽ là "nạn nhân" của bài viết này :))))

Cho số nguyên tố $$p$$​. Mình xét tập hợp các đồng dư modulo $$p$$​ là&#x20;

$$C = \{0, 1, 2, \cdots, p-2, p-1\}$$​&#x20;

, cùng với phép cộng và phép nhân 2 số nguyên. Như vậy tập hợp trên tạo thành một vành. Do $$p$$​ là số nguyên tố nên với mọi $$g \in C$$​ và $$g \neq 0$$​ thì luôn tồn tại $$h$$​ sao cho $$gh \equiv 1 \pmod{p}$$​. Nghĩa là luôn tồn tại nghịch đảo cho mọi phần tử.

**Kết luận**. Tập hợp $$C$$​ với phép cộng và nhân số nguyên tạo thành một trường.

Chúng ta ký hiệu trường hữu hạn các đồng dư modulo $$p$$​ là $$\mathbb{F}_p$$ hoặc $$GF(p)$$ ($$GF$$​ nghĩa là Galois Field, trường Galois, vì sự đóng góp của ông cho lý thuyết nhóm cũng như trường này là cực kì quan trọng).

Bây giờ chúng ta chỉ xét tập hợp $$C'=\{1, 2, \cdots, p-2, p-1\} \subset C$$​ và phép nhân số nguyên modulo $$p$$​. Khi đó $$(C', \times \bmod{p})$$ tạo thành một nhóm có order là $$p-1$$​.

**Tính chất** của $$GF(p)$$​ là:

* order đối với phép nhân là $$p-1$$​
* luôn tồn tại nghịch đảo của phép nhân đối với mọi $$g$$​. Nghĩa là luôn tồn tại $$h$$​ sao cho $$g \times h \equiv 1 \pmod p$$​

**Ứng dụng** của $$GF(p)$$​ trong mật mã học:

* ElGamal
* Elliptic Curve trên $$GF(p)$$​
