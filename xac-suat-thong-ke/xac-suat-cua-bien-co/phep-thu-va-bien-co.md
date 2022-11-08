# Phép thử và biến cố

Chúng ta gọi tập hợp tất cả các trường hợp khi thực hiện phép thử là **không gian mẫu** và ký hiệu là $$\Omega$$.&#x20;

Mỗi phần tử $$\omega \in \Omega$$ trong không gian mẫu được gọi là **biến cố sơ cấp**.

Mỗi tập con $$A \in \Omega$$​ được gọi là một **biến cố** (events) và $$\Omega_A$$​ là **không gian biến cố** chứa các phần tử của $$A$$​.

**Định nghĩa thống kê của xác suất**

Trong một phép thử có $$n$$ khả năng có thể xảy ra. Xét một biến cố $$A$$ xảy ra khi thực hiện phép thử có $$k$$ khả năng xảy ra.&#x20;

Khi đó xác suất của biến cố $$A$$ ký hiệu là $$P(A)$$ và được tính $$P(A) = \frac{k}{n}=\frac{\vert \Omega \vert}{\vert \Omega_A \vert}$$

Dễ thấy, do biến cố $$A$$ là một trường hợp nhỏ trong tổng thể tất cả trường hợp khi thực hiện phép thử, do đó $$0 \leq k \leq n$$. Nghĩa là $$0 \leq P(A) \leq 1$$ với mọi biến cố $$A$$ bất kì.

Ví dụ:  Xét phép thử tung 2 đồng xu. Gọi $$A$$ là biến cố 2 đồng xu cùng mặt.

Ta ký hiệu $$S$$ là đồng xu sấp, $$N$$ là đồng xu ngửa. Khi đó các trường hợp có thể xảy ra của phép thử là $$S-S$$, $$S-N$$, $$N-S$$, $$N-N$$ (4 trường hợp). Như vậy $$\Omega = \{S-S, S-N, N-S, N-N\}$$

Trong khi đó, các trường hợp có thể xảy ra của biến cố $$A$$ là $$S-S$$, $$N-N$$ (2 trường hợp). Như vậy $$\Omega_A = \{S-S, N-N\}$$.

Kết luận: $$P(A) = \frac{|\Omega |}{| \Omega_A |} = \frac{2}{4} = \frac{1}{2}$$
