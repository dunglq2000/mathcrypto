# Tập thương và trường

**Định nghĩa 1**. Vành $$R$$ được gọi là **vành với phần tử đơn vị** (phần tử 1) nếu tồn tại phần tử $$1 \neq 0$$ sao cho tồn tại phần tử $$1$$ sao cho $$\forall r \in R, \, r \cdot 1 = 1 \cdot r = r$$.

**Định nghĩa 2**. Vành $$R$$ được gọi là **vành giao hoán với phần tử đơn vị** nếu nó là vành với phần tử đơn vị và có tính giao hoán đối với phép nhân. Nghĩa là $$\forall a, b \in R, \, a \cdot b = b \cdot a$$.

**Định nghĩa 3**. Vành $$R$$ được gọi là **trường** nếu nó là vành giao hoán với phần tử đơn vị và tồn tại nghịch đảo đối với phép nhân cho mọi phần tử khác 0. Nghĩa là với mọi $$g \in R, \, g \neq 0$$, tồn tại $$g^{-1}$$ sao cho $$g \cdot g^{-1} = g^{-1} \cdot g = 1$$

**Định lý**. Gọi $$R$$ là vành giao hoán với phần tử đơn vị. Khi đó, với $$I$$ là ideal của $$R$$ thì $$R/I$$ là trường khi và chỉ khi $$I$$ là maximal ideal.

**Chứng minh**

1. Điều kiện cần

Ta có $$I$$ là maximal. Ta có nhận xét rằng $$a + I \neq 0 \Leftrightarrow a \not\in I$$. Vì nếu $$a \in I$$ thì tồn tại $$-a \in I$$ và $$a + (-a) = 0$$.

Theo định nghĩa vành thì $$a R$$ cũng là ideal nên $$I + aR$$ cũng là ideal.

Do $$a \not\in I$$, giả sử $$a \in I + aR$$ nên $$I \subset I + aR$$. Do $$I$$ là maximal nên $$I + aR = R$$. Do đó tồn tại $$n \in I, b \in R$$ sao cho $$n + a b = 1$$. Nghĩa là tồn tại nghịch đảo đối với phép nhân của phần tử $$a$$ nên $$R/I$$ là trường.

1. Điều kiện đủ

Giả sử $$I$$ không là maximal. Khi đó tồn tại $$I'$$ mà $$I \subset I' \subset R$$. Do đó tồn tại phần tử $$a \in I'$$, $$a \not\in I$$ sao cho $$a + I \neq 0$$.

Gọi $$b$$ là phần tử nghịch đảo của $$a$$ do $$R/I$$ là trường. Ta có $$(a + I) \cdot (b + I) = (a \cdot b) + I = 1 + I$$. Tức là tồn tại $$n \in I \subset I'$$ mà $$a b = 1 + n$$. Do $$a, b \in I' \Rightarrow 1 \in I'$$. Vậy $$I' = R$$, vô lý. Do đó $$I$$ là maximal.
