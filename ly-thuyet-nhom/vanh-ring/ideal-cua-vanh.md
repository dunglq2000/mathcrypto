# Ideal của vành

**Định nghĩa 1**. Cho vành $$(R, +, \cdot)$$. Một tập hợp con $$I$$ của $$R$$ được gọi là ideal của vành trên nếu:

* $$(I, +)$$ là nhóm con của $$(R, +)$$
* Với mọi $$r \in R$$ và với mọi $$x \in I$$ thì $$rx \in I$$

Do $$r$$ đứng bên trái $$x$$ nên ideal trên gọi là **left ideal**, còn **right ideal** thì ngược lại.

**Tính chất của ideal**

Giả sử vành $$R$$ có ideal $$I$$. Khi đó:

* $$RI \subset I$$ và $$IR \subset I$$
* $$\forall a, b \in R$$ thì $$(a+I) + (b+I) = (a + b) + I$$ và $$(a+I) \cdot (b+I) = (a \cdot b) + I$$

**Định nghĩa 2**. Nếu $$I = aR$$ với $$a \in R$$ thì $$I$$ được gọi là **principal ideal**.

**Định nghĩa 3**. Nếu không tồn tại tập con thực thụ $$I'$$ mà $$I \subset I' \subset R$$ thì $$I$$ được gọi là **maximal ideal**.

**Lưu ý**. Theo toán rời rạc, ở đây **maximal** mang nghĩa tối đại (khác với giá trị lớn nhất).

**Bổ đề 1**. Xét vành số nguyên $$\mathbb{Z}$$. Khi đó mọi ideal của $$\mathbb{Z}$$ đều là principal.

**Chứng minh**. Giả sử ideal $$I$$ có phần tử dương nhỏ nhất là $$n$$. Ta sẽ chứng minh tất cả phần tử trong ideal $$I$$ có dạng $$qn$$.

Theo định nghĩa của ideal, do $$\forall q \in \mathbb{Z}$$ và $$n \in I$$ nên $$qn \in I$$. Giả sử có phần tử $$a = qn + r \in I$$ với $$0 \leq r < n$$. Khi đó $$r = a - qn \in I$$ mà phần tử dương nhỏ nhất trong $$I$$ là $$n$$, nên $$r = 0$$. Như vậy mọi phần tử trong $$I$$ có dạng $$qn$$, tương đương việc mọi ideal có dạng $$n \mathbb{Z}$$ (điều phải chứng minh).

**Bổ đề 2**. Ideal $$I$$ của $$\mathbb{Z}$$ là maximal khi và chỉ khi $$I = n \mathbb{Z}$$ với $$n$$ là số nguyên tố.

**Chứng minh**. Giả sử $$n$$ không là số nguyên tố nên $$n = n_1 \cdot n_2$$ với $$1 < n_1 \leq n_2$$. Khi đó $$n \mathbb{Z} \subset n_1 \mathbb{Z} \subset \mathbb{Z}$$ nên $$n \mathbb{Z}$$ không phải maximal. Như vậy $$n$$ phải là số nguyên tố.
