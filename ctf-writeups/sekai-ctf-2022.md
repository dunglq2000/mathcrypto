# Sekai CTF 2022

Mình làm 1 bài rồi đứng hình :))

## FalLProoF

```python
import hashlib
from os import urandom
from flag import FLAG


def gen_pubkey(secret: bytes, hasher=hashlib.sha512) -> list:
    def hash(m): return hasher(m).digest()
    state = hash(secret)
    pubkey = []
    for _ in range(len(hash(b'0')) * 4):
        pubkey.append(int.from_bytes(state, 'big'))
        state = hash(state)
    return pubkey


def happiness(x: int) -> int:
    return x - sum((x >> i) for i in range(1, x.bit_length()))


def encode_message(message: bytes, segment_len: int) -> list:
    message += bytes(segment_len - len(message) % (segment_len))
    encoded = []
    for i in range(0, len(message), segment_len):
        block = message[i:i + segment_len]
        encoded.append(int.from_bytes(block, 'big'))
    return encoded


def encrypt(pubkey: list, message: bytes) -> list:
    encrypted_blocks = []
    for block_int in encode_message(message, len(pubkey) // 4):
        encrypted_blocks.append([happiness(i & block_int) for i in pubkey])
    return encrypted_blocks


secret = urandom(16)
A = gen_pubkey(secret, hashlib.sha256)
enc = encrypt(A, FLAG)
print(secret.hex())
print(enc)

```

Ở bài này hệ mật mã tạo một public key từ một secret và một hàm hash.

### Tạo public key

Để tạo public key cần truyền vào một chuỗi byte secret và hàm hash. Chúng ta đã biết hàm hash luôn cho output có độ dài cố định không liên quan độ dài input.

Mình gọi hàm hash là $$H(x)$$​ cho input $$x$$​ và độ dài (cố định) của hàm hash là $$L$$. Mình ký hiệu việc thực hiện hash $$k$$​ lần là $$H^{(k)}(x)$$​. Tức là $$H^{(k)}(x) = H(H(\cdots (H(x))\cdots))$$ ($$k$$​ lần). Như vậy public key tương ứng với secret $$s$$​ đầu vào là $$[H^{(1)}(s),\, H^{(2)}(s),\, \cdots,\, H^{(4*L)}(s)]$$.

Prototype của hàm tạo public key dùng sha512 nhưng ở chương trình chính dùng sha256. Do đó $$L = 32$$​ bytes và độ dài public key là 128.

### Encode message

Bước vào hàm encrypt, message ban đầu sẽ được pad thành bội của 32 (theo độ dài public key chia 4 - độ dài hàm hash) và được chia thành từng chunk 32 bytes.

### Happiness

Hàm **happiness** có một tính chất thú vị.

Giả sử mình có đầu vào là $$x=x_n 2^n + x_{n-1} 2^{n-1} + \cdots + x_1 2 + x_0$$.

Khi đó:

* $$x \gg 1 = x_n 2^{n-1} + x_{n-1} 2^{n-2} + \cdots + x_2 2 + x_1$$​
* $$x \gg 2 = x_n 2^{n-2} + x_{n-1} 2^{n-3} + \cdots + x_3 2 + x_2$$​
* $$\cdots$$​
* $$x \gg n = x_n$$

Suy ra $$\begin{align*} & x - (x \gg 1 + x \gg 2 + \cdots x \gg n) \\ = & x_n 2^n + x_{n-1} 2^{n-1} + \cdots + x_1 2 + x_0 \\ - & [x_n (2^{n-1} + 2^{n-2} + \cdots + 1) + x_{n-1} (2^{n-2} + \cdots + 1) + \cdots + x_1] \\ = & x_n \Big(2^n - \frac{2^n - 1}{2 - 1}\Big) + x_{n-1} \Big(2^{n-1} - \frac{2^{n-1} - 1}{2-1} \Big) + \cdots + x_1 (2 - 2 + 1) + x_0 \\  = & x_n + x_{n-1} + \cdots + x_1 + x_0 \end{align*}$$

Tóm lại hàm **happiness** tính tổng các bit của $$x$$​ :))))

### Encrypt

Giả sử mình gọi chunk đầu là $$m$$​. Do $$m$$​ có 32 bytes, tương ứng 128 bit, nên mình viết dưới dạng nhị phân là $$m = m_{255} 2^{255} + m_{254} 2^{254} + \cdots + m_1 2 + m_0$$, $$m_i \in \{0, 1\}$$​.

Mình tiếp tục ký hiệu public key thứ $$j$$ là $$p_j$$​, $$j = \overline{0, 127}$$. Và mình cũng viết dưới dạng nhị phân $$p_j = p_{j, 255} 2^{255} + p_{j, 254} 2^{254} + \cdots + p_{j, 1} 2 + p_{j, 0}$$.

Do đó phép AND cho kết quả $$(m_{255} \cdot p_{j, 255}) \cdot 2^{255} + (m_{254} \cdot p_{j, 254}) \cdot 2^{254} + \cdots + (m_1 \cdot p_{j, 1}) \cdot 2 + (m_0 \cdot p_{j, 0})$$

Qua hàm **happiness** chính là tổng $$m_{255} \cdot p_{j, 255} + m_{254} \cdot p_{j, 254} + \cdots + m_1 \cdot p_{j, 1} + m_0 \cdot p_{j,0}$$

Do đó với 128 public key mình có thể viết dưới dạng ma trận như sau

$$\begin{pmatrix} 	p_{0, 255} & p_{0, 254} & \cdots & p_{0, 1} & p_{0, 0} \\ 	p_{1, 255} & p_{1, 254} & \cdots & p_{1, 1} & p_{1, 0} \\ 	\cdots & \cdots & \cdots & \cdots & \cdots \\ 	p_{126, 255} & p_{126, 254} & \cdots & p_{126, 1} & p_{126, 0} \\ 	p_{127, 255} & p_{127, 254} & \cdots & p_{127, 1} & p_{127, 0}  \end{pmatrix} \cdot \begin{pmatrix} m_{255} \\ m_{254} \\ \cdots \\ m_1 \\ m_0 \end{pmatrix} =  \begin{pmatrix} c_{0} \\ c_{1} \\ \cdots \\ c_{126} \\ c_{127} \end{pmatrix}$$

Vấn đề ở đây là ma trận $$P$$​ không phải ma trận vuông. Do đó mình không thể tính nghịch đảo được :((

Để ý rằng $$m$$​ luôn không đổi mỗi lần netcat nên mình chỉ cần request thêm 1 lần nữa và có thêm 128 public key nữa. Khi đó ghép các public key đó nối tiếp xuống dưới ma trận $$P$$​ cũng như ghép thêm các ciphertext mới xuống dưới cột $$c$$​ thì mình đã đủ ma trận vuông để giải.

```python
import hashlib
from sage.all import *

def gen_pubkey(secret: bytes, hasher=hashlib.sha512) -> list:
    def hash(m): return hasher(m).digest()
    state = hash(secret)
    pubkey = []
    for _ in range(len(hash(b'0')) * 4):
        pubkey.append(int.from_bytes(state, 'big'))
        state = hash(state)
    return pubkey


def happiness(x: int) -> int:
    return x - sum((x >> i) for i in range(1, x.bit_length()))


def encode_message(message: bytes, segment_len: int) -> list:
    message += bytes(segment_len - len(message) % (segment_len))
    encoded = []
    for i in range(0, len(message), segment_len):
        block = message[i:i + segment_len]
        encoded.append(int.from_bytes(block, 'big'))
    return encoded


def encrypt(pubkey: list, message: bytes) -> list:
    encrypted_blocks = []
    for block_int in encode_message(message, len(pubkey) // 4):
        encrypted_blocks.append([happiness(i & block_int) for i in pubkey])
    return encrypted_blocks

secret1 = bytes.fromhex("2329d5d8515229084589a6570919558f")
secret2 = bytes.fromhex("5a57b559987fb0f351f73647228e74fb")
enc2 = [[83, 67, 72, 64, 79, 69, 69, 76, 67, 60, 89, 60, 69, 74, 57, 77, 65, 77, 57, 67, 69, 61, 73, 64, 70, 73, 76, 51, 72, 74, 69, 68, 65, 69, 74, 70, 78, 56, 79, 57, 79, 72, 66, 81, 74, 78, 71, 68, 80, 58, 72, 79, 76, 78, 70, 76, 66, 66, 73, 70, 67, 62, 75, 77, 57, 70, 63, 66, 59, 68, 69, 70, 62, 72, 69, 76, 56, 67, 73, 66, 66, 76, 73, 62, 71, 68, 82, 75, 70, 75, 64, 67, 68, 63, 72, 71, 70, 60, 74, 72, 61, 75, 69, 71, 62, 74, 70, 71, 70, 82, 61, 75, 72, 62, 80, 67, 72, 63, 67, 71, 67, 68, 65, 72, 70, 68, 77, 64], [73, 68, 66, 74, 76, 72, 66, 71, 68, 57, 75, 59, 66, 68, 63, 73, 60, 62, 62, 65, 72, 57, 72, 63, 75, 71, 71, 54, 64, 73, 67, 65, 60, 69, 72, 70, 79, 62, 63, 64, 73, 63, 63, 80, 76, 78, 74, 65, 73, 63, 79, 81, 74, 76, 62, 73, 73, 64, 62, 74, 68, 55, 78, 63, 65, 65, 63, 64, 61, 73, 73, 65, 67, 67, 69, 69, 61, 66, 68, 66, 70, 66, 68, 57, 71, 64, 79, 71, 62, 77, 63, 61, 67, 62, 69, 61, 74, 57, 68, 63, 69, 76, 67, 74, 54, 73, 70, 65, 71, 77, 58, 76, 62, 69, 73, 58, 67, 65, 64, 65, 70, 73, 67, 72, 66, 59, 67, 73], [34, 35, 27, 29, 30, 34, 27, 32, 34, 30, 36, 34, 27, 30, 23, 27, 29, 32, 27, 28, 33, 21, 35, 24, 26, 36, 34, 24, 23, 27, 32, 37, 31, 27, 33, 31, 25, 30, 28, 26, 39, 29, 30, 30, 40, 35, 29, 31, 28, 27, 33, 40, 25, 33, 30, 34, 24, 26, 28, 30, 25, 31, 35, 32, 23, 33, 25, 32, 26, 32, 36, 28, 28, 31, 27, 29, 27, 35, 29, 31, 30, 26, 25, 29, 30, 25, 39, 28, 31, 28, 24, 33, 31, 32, 29, 22, 34, 23, 28, 31, 31, 33, 33, 33, 28, 32, 31, 32, 38, 33, 25, 31, 34, 28, 32, 27, 31, 30, 32, 33, 27, 25, 32, 37, 32, 26, 38, 27]]
enc1 = [[63, 67, 73, 73, 63, 62, 67, 72, 75, 73, 71, 75, 67, 65, 71, 68, 84, 67, 67, 69, 67, 65, 78, 71, 68, 74, 67, 69, 74, 59, 71, 70, 66, 73, 75, 72, 76, 61, 60, 67, 70, 70, 73, 63, 62, 75, 74, 77, 72, 56, 72, 77, 68, 77, 74, 79, 73, 77, 72, 63, 67, 77, 72, 82, 78, 69, 60, 74, 61, 71, 57, 65, 64, 77, 69, 60, 69, 61, 75, 61, 65, 71, 75, 70, 77, 69, 66, 74, 70, 78, 62, 73, 67, 72, 75, 78, 73, 70, 62, 72, 67, 61, 63, 69, 83, 75, 67, 84, 62, 70, 72, 67, 65, 66, 65, 73, 80, 69, 67, 71, 67, 65, 69, 79, 69, 59, 70, 71], [54, 70, 68, 69, 62, 65, 60, 75, 82, 73, 68, 73, 65, 60, 73, 71, 71, 71, 66, 69, 66, 66, 72, 67, 63, 80, 61, 67, 71, 65, 70, 73, 64, 68, 72, 73, 75, 60, 64, 70, 71, 70, 72, 61, 64, 64, 75, 69, 72, 63, 67, 72, 64, 71, 78, 74, 65, 71, 72, 61, 75, 71, 69, 77, 79, 69, 55, 63, 58, 63, 67, 73, 70, 72, 63, 59, 66, 63, 78, 63, 62, 67, 80, 67, 75, 70, 70, 71, 73, 71, 65, 72, 67, 58, 77, 69, 64, 62, 61, 70, 66, 52, 57, 68, 85, 73, 72, 75, 63, 69, 69, 70, 59, 76, 62, 64, 80, 64, 68, 77, 65, 50, 69, 76, 79, 52, 71, 73], [25, 32, 34, 38, 28, 33, 20, 35, 38, 27, 25, 32, 26, 29, 26, 28, 29, 31, 30, 28, 32, 29, 37, 31, 29, 39, 27, 28, 28, 24, 34, 37, 25, 35, 28, 37, 39, 24, 28, 26, 33, 26, 33, 21, 28, 31, 29, 28, 24, 22, 32, 32, 31, 32, 36, 32, 24, 34, 32, 28, 32, 38, 34, 31, 35, 28, 25, 29, 27, 26, 35, 28, 32, 31, 30, 23, 28, 21, 32, 26, 30, 28, 28, 28, 34, 23, 23, 29, 35, 29, 32, 29, 36, 32, 31, 32, 25, 28, 26, 30, 27, 23, 23, 32, 36, 30, 24, 34, 25, 30, 29, 30, 24, 31, 27, 33, 28, 25, 27, 28, 30, 21, 28, 24, 31, 20, 33, 32]]

pubkey1 = gen_pubkey(secret1, hashlib.sha256)
pubkey2 = gen_pubkey(secret2, hashlib.sha256)
mat = []

# print(len(pubkey), pubkey[0].bit_length())
for pub in pubkey1:
    m = list(map(int, bin(pub)[2:].zfill(256)))
    mat.append(m)
for pub in pubkey2:
    m = list(map(int, bin(pub)[2:].zfill(256)))
    mat.append(m)
    
F = ZZ
mat = matrix(F, mat)
flag = b""
for i in range(3):
    msg = mat.inverse() * vector(F, enc1[i] + enc2[i])
    msg = ''.join(list(map(str, msg)))
    flag += int.to_bytes(int(msg, 2), 32, 'big')
print(flag)
```

```
b'SEKAI{w3ll_1_gu355_y0u_c4n_4lw4y5_4sk_f0r_m0r3_3qu4t10n5_wh3n_n0_0n3s_l00k1ng}\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00'
```

Cám ơn các bạn đã đọc writeup siêu dài cho một bài ............ không dài lắm :'(
