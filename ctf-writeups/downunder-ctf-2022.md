# DownUnder CTF 2022

### 1.  Baby ARX

Bài này thuộc dạng stream cipher với việc 2 thằng kề nhau sẽ đưa ra 1 ciphertext.

```python
class baby_arx():
    def __init__(self, key):
        assert len(key) == 64
        self.state = list(key)

    def b(self):
        b1 = self.state[0]
        b2 = self.state[1]
        b1 = (b1 ^ ((b1 << 1) | (b1 & 1))) & 0xff
        b2 = (b2 ^ ((b2 >> 5) | (b2 << 3))) & 0xff
        b = (b1 + b2) % 256
        self.state = self.state[1:] + [b]
        return b

    def stream(self, n):
        return bytes([self.b() for _ in range(n)])


FLAG = open('./flag.txt', 'rb').read().strip()
cipher = baby_arx(FLAG)
out = cipher.stream(64).hex()
print(out)

# cb57ba706aae5f275d6d8941b7c7706fe261b7c74d3384390b691c3d982941ac4931c6a4394a1a7b7a336bc3662fd0edab3ff8b31b96d112a026f93fff07e61b
```

Ở đây ta thấy rằng, với $$p_i$$​ và $$p_{i+1}$$​ là 2 ký tự của plaintext sẽ cho ra ký tự thứ $$c_i$$​ của ciphertext.

Như vậy mình đã biết 1 đoạn plaintext ban đầu là **DUCTF** rồi nên phần còn lại là bruteforce từng ký tự và so sánh với ciphertext để ra được ký tự ban đầu.

```python

ct = bytes.fromhex(ct)

def b(x, y):
    x = (x ^ ((x << 1) | (x & 1))) & 0xff
    y = (y ^ ((y >> 5) | (y << 3))) & 0xff
    z = (x + y) % 256
    return z

pt = b'DUCTF{'
pt = list(pt)
ct = list(ct)
for i in range(len(pt), 64):
    for j in range(256):
        if b(pt[-1], j) == ct[i-1]:
            pt.append(j)
            break

print(bytes(pt))
```

### 2. OFB

Một bài block cipher gây rối loạn tiền đình :))))

```python
#!/usr/bin/env python3

from os import urandom, path
from Crypto.Cipher import AES


FLAG = open(path.join(path.dirname(__file__), 'flag.txt'), 'r').read().strip()
MESSAGE = f'Decrypt this... {urandom(300).hex()} {FLAG}'


def main():
    key = urandom(16)
    for _ in range(2):
        iv = bytes.fromhex(input('iv: '))
        aes = AES.new(key, iv=iv, mode=AES.MODE_OFB)
        ct = aes.encrypt(MESSAGE.encode())
        print(ct.hex())


if __name__ == '__main__':
    main()

```

Ở đây mỗi lần netcat lên server sẽ random 300 bytes và nhét vào giữa đoạn **Decrypt this...** (có dấu cách ở cuối nữa nha!!!!) và FLAG. Thêm nữa mỗi lần netcat lên sẽ random 1 key AES nên chúng ta sẽ chỉ attack trong một session netcat.

Mình được phép kiểm soát 2 IV cho 2 lần encrypt. Sau mỗi lần encrypt mình sẽ được nhận ciphertext. Do đó mình đoán rằng IV thứ 2 sẽ có liên quan gì đó đến IV đầu và ciphertext 1.

Trời không phụ lòng người :)))) Có công đoán mò có ngày làm nên :)))) Mình đã guessing được IV2 để có thể decrypt :))

<figure><img src="../.gitbook/assets/ofb.png" alt=""><figcaption><p>Hình 1. Sơ đồ cho 2 lần encrypt (lấy 2 block làm ví dụ)</p></figcaption></figure>

Cách giải bài này nằm ở 2 dấu chấm đỏ lòm mà mình vẽ :))))

Trong mode OFB, $$C_i = P_i \oplus O_i$$ với $$O_i$$​ là encrypt AES của $$O_{i-1}$$​. Như vậy nếu mình chọn $$IV2$$​ sao cho sau khi encrypt thì nó bằng đúng $$O_2$$​ ở lần encrypt đầu, thì tất cả các $$O'_i$$​ sau đó luôn giống với $$O_i$$​ sau một đơn vị. Tức là $$O'_i = O_{i+1}$$, $$i=1,2,\cdots$$

Trong OFB thì $$C_i = P_i \oplus O_i$$ và $$C'_i = P'_i\oplus O'_i$$. Do $$O'_i=O_{i+1}$$​ theo cách chọn $$IV2$$​ của mình nên mình sẽ có $$C_{i+1} \oplus P_{i+1} = C'_i \oplus P'_i$$ hay $$P_{i+1} = C_{i+1} \oplus C'_i \oplus P_i$$. Mà $$P_1$$​ mình có rồi :)))) nên mình sẽ suy ra được tất cả $$P_i$$​ còn lại với $$i=2, 3, \cdots$$​

Flag mình tìm được:

```python
b'Decrypt this... 65926f16baacedfc716e2046d55f56c449bf0d66e6344866a4a34c3879e687c3bc9ca79e6f74a2152def17d99043e4e7035b3af1379f57a737ea8d4c8557b31676cda81a7ed27b3333a7e63d7397b567485a0d9108eb2adfdee1c6eca22e9fda829f2cad61cbb20a4022918498496ee0185af3410a64987b5684aa03dc10b46d30aba53dcd64d1984956af0bb745db6f4692f997561c9a24afefdff9d5359744f8e984ffaaad38477fc0d015f699b31403494dde2ad436d4967fe98facdc70c705391f92ca0ed69170cdb2c6d85971e1450a41a7d8bf18eb82adb48967cf6d91156a9780fe4d6a0dfe492a5e5df3ba97a2028fdee1458cdfc00ecf008bb522b593b875127baeb1c6368f3d06fb8e59b01868043691b13a76edbdbcb77a86e26348038e92ea45e3963b634f51 DUCTF{0fb_mu5t_4ctu4lly_st4nd_f0r_0bvi0usly_f4ul7y_bl0ck_c1ph3r_m0d3_0f_0p3ra710n_7b9cb403e8332c980456b17a00abd51049cb8207581c274fcb233f3a43df4a}'
```

### 3. CRT

Một bài discrete logarithm trên modulo đa thức.

```python
p = 55899879511190230528616866117179357211
V = GF(p)^3
R.<x> = PolynomialRing(GF(p))
f = x^3 + 36174005300402816514311230770140802253*x^2 + 35632245244482815363927956306821829684*x + 10704085182912790916669912997954900147
Q = R.quotient(f)

def V_pow(A, n):
    return V([a^n for a in list(A)])

n, m = randint(1, p), randint(1, p)
A = Q.random_element()
B = Q.random_element()
C = A^n * B^m

print(' '.join(map(str, list(A))))
print(' '.join(map(str, list(B))))
print(' '.join(map(str, list(C))))

phi_A = V(list(map(int, input().split())))
phi_B = V(list(map(int, input().split())))
phi_C = V(list(map(int, input().split())))

check_phi_C = V_pow(phi_A, n).pairwise_product(V_pow(phi_B, m))

if phi_C == check_phi_C:
    print(open('./flag.txt', 'r').read().strip())

# DUCTF{CRT_e4sy_as_0ne_tw0_thr3e}
```

Ở đây đề cho chúng ta 2 đa thức được random là $$A$$​ và $$B$$​ (cả 2 đều nằm trong modulo $$f(x)$$​ trên $$\mathbb{Z}_p[x]$$​. Với 2 số random $$n$$​ và $$m$$​ bị giấu, đề cho mình đa thức $$C = A^n \cdot B^m$$.

Nhiệm vụ của mình phải tìm 3 vector trong $$GF(p)$$​ là $$\varphi_A$$​, $$\varphi_B$$ và $$\varphi_C$$​ sao cho tích có hướng của $$\varphi^n_A$$​ và $$\varphi^m_B$$​ bằng đúng $$\varphi_C$$​. Ở đây $$\varphi^n_A$$​ nghĩa là mỗi phần tử của $$\varphi_A$$​ được mũ $$n \pmod p$$​, $$\varphi_A = (x_A, y_A, z_A)$$ thì $$\varphi_A^n = (x^n_A \bmod p, y^n_A \bmod p, z^n_A \bmod p)$$.

Như vậy mình cần giải bài toán discrete logarithm cho polynomial ring. Phần khó của bài này là làm sao tìm được order của mỗi đa thức. Mình thấy rằng $$f(x)$$​ có thể factor thành tích của 3 đa thức bậc 1. Như vậy việc giải bài toán trên modulo $$f(x)$$​ trở thành giải bài toán trên từng đa thức bậc 1 rồi CRT chúng lại với nhau.

Nhưng mình không biết cách tìm order của mỗi đa thức .........

Chán thật, mình chọn $$\varphi_A = \varphi_B = \varphi_C = (0, 0, 0)$$ và nó luôn đúng chả quan tâm $$n, m$$ chi cả :))))))

Unintended solution :))))))

Cám ơn mọi người đã đọc writeup của mình. Hẹn gặp lại :joy:
