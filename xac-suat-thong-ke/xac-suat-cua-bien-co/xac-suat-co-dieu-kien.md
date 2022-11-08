# Xác suất có điều kiện

Xác suất mà biến cố $$B$$​ xảy ra với điều kiện biến cố $$A$$​ đã xảy ra trước đó được ký hiệu và định nghĩa là

$$P(B|A) = \frac{P(AB)}{P(A)}$$​

Nghĩa là xác suất khi cả $$A$$​ và $$B$$​ cùng xảy ra (biến cố) chia cho xác suất $$A$$​ (không gian mẫu).

Trong trường hợp này, công thức nhân xác suất ở trước không còn đúng nữa vì các biến cố không độc lập nhau, nên ta có:

$$P(AB) = P(B|A)\cdot P(A) = P(A|B) \cdot P(B)$$​

**Tổng quát**, với hệ $$n$$ biến cố **không độc lập**:

$$P(A_1 A_2 \cdots A_n) = P(A_1) P(A_2 | A_1) P(A_3 | A_2 A_1) \cdots P(A_n | A_{n-1} \cdots A_1)$$​
