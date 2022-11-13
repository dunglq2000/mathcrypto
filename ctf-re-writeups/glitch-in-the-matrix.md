# Glitch in the matrix

```python
#!/usr/bin/env python3
from secret import SECRET_BASIS
from secrets import token_hex
import random
import os

assert len(SECRET_BASIS) == len(SECRET_BASIS[0]) == 128

def f(M: list[list[int]], C: list[int]) -> list[int]:
    v = [0] * len(M[0])
    for c, m in zip(C, M):
        if c:
            v = [x ^ y for x, y in zip(v, m)]
    return v

def random_bits(n: int) -> list[int]:
    return list(map(int, bin(random.getrandbits(n))[2:].rjust(n, "0")))

def encrypt(message: bytes) -> str:
    M = [b for c in message for b in map(int, "{:08b}".format(c))]
    ct = []
    for bit in M:
        C = random_bits(64)
        v = f(SECRET_BASIS[:64], C) if bit else f(SECRET_BASIS[64:], C)
        ct.extend(v)
    ct = "".join(map(str, ct))
    return bytes([int(ct[i:i+8], 2) for i in range(0, len(ct), 8)]).hex()

def decrypt(ciphertext: str) -> bytes:
    # TODO: implement this pls
    pass

def action_prompt() -> int:
    print('''============= MENU =============
    1. Have a guess
    2. Get ciphertext
    3. Change password
    4. Quit
================================\n''')
    try:
        option = int(input("Your option> "))
    except:
        return None
    return option

def chall():
    try:
        password = token_hex(8)
        while True:
            option = action_prompt()
            if option == 1:
                user_password = input("Input your password (hex): ")
                if user_password == password:
                    print(f"Is taking the red pill worth it? Here is the truth that you want: {os.environ['FLAG']}.")
                else:
                    print("Guess you can't escape the matrix after all.", password)
                break
            elif option == 2:
                print(f"Leaky ciphertext: {encrypt(bytes.fromhex(password))}")
            elif option == 3:
                print("Generating super secure password ...")
                password = token_hex(8)
            elif option == 4:
                print("Maybe the truth is not that important, huh?")
                break
            else:
                print("Invalid option.")
            print("\n")
    except:
        print("An error occured!")

chall()
```

Bài này mình re-writeup từ hint của của một idol :))))

Thử thách ở đây là cần đoán một token hex độ dài 64 bit với secret key là **SECRET\_BASIS**.

Gọi token hex có 64 bit là $$(m_1, m_2, \cdots, m_{64})$$. Với **SECRET\_BASIS** là ma trận trên $$GF(2)$$ $$128 \times 128$$, ta thực hiện encrypt như sau:

* Random một chuỗi 64 bit **C**
* Nếu $$m_i = 1$$ thì thực hiện **f(SECRET\_BASIS\[:64], C)**, nếu là 0 thì **f(SECRET\_BASIS\[64:], C)**
* Nghĩa là secret key được chia thành 2 nửa trái phải theo chiều dọc

Hàm $$f$$ thực hiện như sau:

* Với **C** là một chuỗi 64 bit. Đặt $$C = (c_1, c_2, \cdots, c_{64})$$.
* Nếu $$c_i = 1$$ thì dòng $$i$$ được xor vào kết quả
* Hay viết dưới dạng vector sẽ là $$c_1 \cdot (m_{1,1}, m_{1,2}, \cdots m_{1,128}) + \cdots + c_{64} \cdot (m_{64,1}, m_{64,2}, \cdots, m_{64,128})$$

Ý tưởng để làm bài này là mình lấy thật nhiều ciphertext tương ứng với 1 plaintext (password). Do từng bit của plaintext được mã hóa riêng nhau nên mình sẽ tìm mối liên hệ giữa 2 block mã hóa để xem chúng có cùng thuộc nửa trái (hoặc nửa phải) của secret key hay không.

Vì 64 bit plaintext được mã hóa thành $$64 \times 128$$ bit của ciphertext, mình chia mỗi ciphertext thành 64 block. Giả sử mình lấy $$n$$ ciphertext, mỗi ciphertext cũng được chia thành 64 block thì mình sẽ có 64 ma trận $$n \times 128$$.

Nếu 2 ma trận có chung base (cùng thuộc nửa trái hoặc nửa phải) thì hiệu của chúng sẽ có cùng rank với ma trận đầu. Do đó mình giả sử bit đầu là 0, vậy thì những block thứ 2 tới 64 (tương ứng bit thứ 2 tới 64) nếu có cùng rank thì sẽ mang bit 0, không thì mang bit 1. Do đó mình cần lấy $$n$$ ciphertext đủ lớn để block đầu có rank là 64 (max).

Lưu ý rằng do mình giả sử bit đầu là 0, nên nếu bit đầu của plaintext là 1 thì sẽ không ra. Do đó xác suất cách làm này là 1/2.

Source code ở [đây](https://github.com/dunglq2000/CTF/tree/master/ISITDTUCTF/2022/glitch\_in\_the\_matrix)
