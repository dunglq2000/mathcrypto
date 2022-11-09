# AES

AES theo khối 128 bit, sử dụng mô hình mạng SPN với 4 phép biến đổi chính là:

* Add Round Key (ARK)
* Substitute Bytes (SB)
* Shift Rows (SR)
* Mix Columns (MC)

Các phép biến đổi Subsitute Bytes, Shift Rows và Mix Columns có phép biến đổi ngược là Inverse Substitute Bytes, Inverse Shift Rows và Inverse Mix Columns. Riêng phép biến đổi Add Round Key chỉ là phép xor nên inverse cũng là chính nó.

Ta xét phép biến đổi trên key 128 bit (AES hỗ trợ 3 kích thước key là 128, 192 và 256 bit).

* Kích thước key ban đầu là 128 bit (16 bytes) và tương ứng là 10 vòng biến đổi.
* AES dùng hàm **Expand Key** để mở rộng khóa thành 44 word 32 bit, chia thành 11 cụm khóa con. Nghĩa là mỗi 4 word 32 bit sẽ làm tham số cho 1 thao tác Add Round Key do có 10 vòng biến đổi.
* Mỗi block bản rõ 16 bytes $$p_0 p_1 \cdots p_{15}$$ được tổ chức dưới dạng một ma trận $$4 \times 4$$ (gọi là **state**) $$\begin{pmatrix}p_0 & p_1 & p_2 & p_3 \\ p_4 & p_5 & p_6 & p_7 \\ p_8 & p_9 & p_{10} & p_{11} \\ p_{12} & p_{13} & p_{14} & p_{15}\end{pmatrix} \rightarrow \begin{pmatrix}s_{00} & s_{01} & s_{02} & s_{03} \\ s_{10} & s_{11} & s_{12} & s_{13} \\ s_{20} & s_{21} & s_{22} & s_{23} \\ s_{30} & s_{31} & s_{32} & s_{33}\end{pmatrix}$$
* Các phép biến đổi Add Round Key, Subtitute Bytes, Shift Rows và Mix Columns được thực hiện trên ma trận $$4 \times 4$$ này.
* Các phép tính số học trong AES được thực hiện trong trường Galois $$GF(2^8)$$ với đa thức tối giản là $$m(x) = x^8 + x^4 + x^3 + x + 1$$.
