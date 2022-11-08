# Tổng và tích hai biến cố

### 1. Phép cộng xác suất

Tổng của 2 biến cố $$A$$​ và $$B$$​ là hợp của chúng $$A \cup B$$​.

Khi đó tổng xác suất của 2 biến cố là $$P(A \cup B)$$​ hoặc $$P(A+ B)$$​.

Nếu 2 biến cố $$A$$​ và $$B$$​ **xung khắc** thì $$A \cap B = \emptyset$$​ và:

$$P(A + B) = P(A) + P(B)$$​

Đặc biệt, với 2 biến cố **đối lập** $$A$$​ và $$\bar{A}$$​:

$$1 = P(\Omega) = P(A + \bar{A}) = P(A) + P(\bar{A})$$​

Như vậy nếu biết xác suất của $$A$$​ ta có thể tìm xác suất của $$\bar{A}$$​.

**Tổng quát** khi giao của 2 biến cố khác rỗng, tức là $$A \cap B \neq \emptyset$$​:

$$P(A + B) = P(A) + P(B) - P(A \cap B)$$

**Hệ quả**: với tập hợp các biến cố $$A_1, A_2, \cdots, A_n$$​ xung khắc đôi một, $$A_i \cap A_j = \emptyset,\ i\neq j$$​ thì xác suất của tổng bằng tổng các xác suất:

$$P(A_1 + A_2 + \cdots + A_n) = P(A_1) + P(A_2) + \cdots + P(A_n)$$​.

### 2. Phép nhân xác suất

Ở đây ta mới chỉ xét về phép nhân 2 biến cố độc lập. Trường hợp không độc lập sẽ xét ở các bài sau.

Tích của 2 biến cố là giao của chúng $$A \cap B$$

Khi đó tích xác suất của 2 biến cố được ký hiệu $$P(A \cap B)$$​ hoặc $$P(AB)$$​.

Nếu $$A$$​ và $$B$$​ là 2 biến cố **độc lập** thì $$P(AB) = P(A) \cdot P(B)$$​.

Hệ quả: với các biến cố độc lập $$A_1, A_2, \cdots, A_n$$​ thì xác suất của tích bằng tích các xác suất:

$$P(A_1 \cdot A_2 \cdots A_n) = P(A_1) \cdot P(A_2) \cdots P(A_n)$$​.
