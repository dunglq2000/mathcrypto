# Crypto CTF 2021

Chào mọi người, lại một mùa Crypto CTF nữa đã qua và lần này mình có khá khẩm hơn năm ngoái một chút, và sau đây là writeup các challenge mình đã làm được

### Farm

```python
#!/usr/bin/env sage

from sage.all import *
import string, base64, math
from flag import flag

ALPHABET = string.printable[:62] + '\\='

F = list(GF(64))

def keygen(l):
	key = [F[randint(1, 63)] for _ in range(l)] 
	key = math.prod(key) # Optimization the key length :D
	return key

def maptofarm(c):
	assert c in ALPHABET
	return F[ALPHABET.index(c)]

def encrypt(msg, key):
	m64 = base64.b64encode(msg)
	enc, pkey = '', key**5 + key**3 + key**2 + 1
	for m in m64:
		enc += ALPHABET[F.index(pkey * maptofarm(chr(m)))]
	return enc

# KEEP IT SECRET 
key = keygen(14) # I think 64**14 > 2**64 is not brute-forcible :P

enc = encrypt(flag, key)
print(f'enc = {enc}')
```

Đề bài cho mình **F** tạo các đa thức trên GF(2^6), **maptofarm** để lấy đa thức tương ứng với chỉ số của ký tự trong alphabet, và **encrypt** để mã hóa chuỗi base64, bằng cách là ký tự base64 **m** sẽ thành **ALPHABET\[F.index(pkey \* maptofarm(chr(m)))]**

Ok, vì **key** chỉ nằm trong GF(2^6), mình chỉ việc bruteforce thôi (nằm trong GF(2^6) nên độ dài là 14 hay bao nhiêu cũng không quan trọng). Làm ngược lại quá trình mã hóa mình có flag.

Flag: _CCTF{EnCrYp7I0n\_4nD\_5u8STitUtIn9\_iN\_Fi3Ld!}_

### KeyBase

```python
#!/usr/bin/env python3

from Crypto.Util import number
from Crypto.Cipher import AES
import os, sys, random
from flag import flag

def keygen():
	iv, key = [os.urandom(16) for _ in '01']
	return iv, key

def encrypt(msg, iv, key):
	aes = AES.new(key, AES.MODE_CBC, iv)
	return aes.encrypt(msg)

def decrypt(enc, iv, key):
	aes = AES.new(key, AES.MODE_CBC, iv)
	return aes.decrypt(enc)

def die(*args):
	pr(*args)
	quit()

def pr(*args):
	s = " ".join(map(str, args))
	sys.stdout.write(s + "\n")
	sys.stdout.flush()

def sc():
	return sys.stdin.readline().strip()

def main():
	border = "+"
	pr(border*72)
	pr(border, " hi all, welcome to the simple KEYBASE cryptography task, try to    ", border)
	pr(border, " decrypt the encrypted message and get the flag as a nice prize!    ", border)
	pr(border*72)

	iv, key = keygen()
	flag_enc = encrypt(flag, iv, key).hex()

	while True:
		pr("| Options: \n|\t[G]et the encrypted flag \n|\t[T]est the encryption \n|\t[Q]uit")
		ans = sc().lower()
		if ans == 'g':
			pr("| encrypt(flag) =", flag_enc)
		elif ans == 't':
			pr("| Please send your 32 bytes message to encrypt: ")
			msg_inp = sc()
			if len(msg_inp) == 32:
				enc = encrypt(msg_inp, iv, key).hex()
				r = random.randint(0, 4)
				s = 4 - r
				mask_key = key[:-2].hex() + '*' * 4
				mask_enc = enc[:r] + '*' * 28 + enc[32-s:]
				pr("| enc =", mask_enc)
				pr("| key =", mask_key)
			else:
				die("| SEND 32 BYTES MESSAGE :X")
		elif ans == 'q':
			die("Quitting ...")
		else:
			die("Bye ...")

if __name__ == '__main__':
	main()
```

Bài này cho mình 1 hệ thống sử dụng AES mode CBC (key và iv giống nhau suốt 1 phiên kết nối) để làm 2 việc:

* Đưa flag đã bị mã hóa
* Mã hóa 1 đoạn input 32 byte bất kì và trả lại key (dạng hex) với 2 byte cuối bị ẩn, và ciphertext với 14 byte ở giữa bị ẩn

Do mode CBC có tính chất $$C_{i+1} = E_k(C_i \oplus P_{i+1})$$, với $$P_0 = iv$$. Do đó nếu mình chọn $$P$$ và $$P'$$ là 2 plaintext có 16 byte đầu giống nhau còn 16 byte cuối khác nhau thì mình có $$C_1=C_1'=E_k(iv \oplus P_1)$$ còn $$C_2=E_k(C_1 \oplus P_2)$$ và $$C_2'=E_k(C_1' \oplus P_2')$$

Từ đây mình có $$C_1 \oplus P_2 \oplus C_1' \oplus P_2' = D_k(C_2) \oplus D_k(C_2')$$. Mà $$C_1 = C_1'$$ rồi nên mình cần lấy ciphertext nào mà 16 byte cuối không bị ẩn đi để có thể bruteforce 2 byte cuối của key và decrypt, tức là mình phải có $$P_2 \oplus P_2' = D_k(C_2) \oplus D_k(C_2')$$

Bây giờ tìm iv, mình chỉ cần đưa lên server 32 byte 0 là xong và cũng tương tự trên, chỉ lấy ciphertext nào mà 16 byte cuối không bị ẩn. Vì $$C_2 = E_k(C_1) = E_k(E_k(iv))$$ (do xor với dãy toàn 0). Decrypt mình có lại iv.

Giờ thì giải mã flag thôi

Flag: _CCTF{h0W\_R3cOVER\_7He\_5eCrET\_1V?}_

### Rima

```python
#!/usr/bin/env python

from Crypto.Util.number import *
from flag import FLAG

def nextPrime(n):
    while True:
        n += (n % 2) + 1
        if isPrime(n):
            return n

f = [int(x) for x in bin(int(FLAG.hex(), 16))[2:]]

f.insert(0, 0)
for i in range(len(f)-1): f[i] += f[i+1]

a = nextPrime(len(f))
b = nextPrime(a)

g, h = [[_ for i in range(x) for _ in f] for x in [a, b]]

c = nextPrime(len(f) >> 2)

for _ in [g, h]:
    for __ in range(c): _.insert(0, 0)
    for i in range(len(_) -  c): _[i] += _[i+c]

g, h = [int(''.join([str(_) for _ in __]), 5) for __ in [g, h]]

for _ in [g, h]:
    if _ == g:
        fname = 'g'
    else:
        fname = 'h'
    of = open(f'{fname}.enc', 'wb')
    of.write(long_to_bytes(_))
    of.close()
```

Bài này không dùng biến chữ để chạy loop và dùng dấu gạch dưới của python nên lúc đầu mình thấy hơi rắc rối.

Đầu tiên flag được chuyển sang dạng nhị phân và thêm 1 bit "0" ở đầu được dãy $$f$$. Kế tiếp với mỗi $$i=0 \cdots len(f)-2$$ thì $$f_i += f_{i+1}$$.

Kế tiếp 2 số $$a$$ và $$b$$ được tạo là 2 số nguyên tố kế tiếp tính từ $$len(f)$$ là độ dài $$f$$. $$g$$ và $$h$$ là 2 list tạo ra từ việc lặp $$f$$ $$a$$ và $$b$$ lần. Như vậy độ dài của $$g$$ là $$a \cdot len(f)$$ và độ dài của $$h$$ là $$b \cdot len(f)$$

Kế tiếp $$c$$ là số nguyên tố kế tiếp tính từ $$len(f) >> 2$$. Thêm $$c$$ bit "0" vào đầu $$g$$ và thực hiện $$g_i += g_{i+c}$$ với $$i=0 \cdots len(f)-c-1$$. Làm tương tự với $$h$$

Cuối cùng là chuyển $$g$$ và $$h$$ sang số int base 5 và viết lên file dưới dạng byte. Nên đầu tiên mình sẽ làm ngược lại và tìm được $$g$$ và $$h$$, sau đó mình bruteforce $$len(f)$$ để tìm $$a$$, $$b$$ và $$c$$ và xem thử bộ nào thỏa $$a \cdot len(f) + c = len(g)$$ và $$b \cdot len(f) + c = len(h)$$.

Sau đó là làm ngược lại quá trình, với $$i=len(f)-c-1 \cdots 0$$ thì $$g_i -= g_{i+c}$$. Tương tự với $$h$$. Có thể kiểm chứng cách đúng nếu đầu $$g$$ có đúng $$c$$ số 0 :))

Giờ thì, lấy $$len(f)$$ số đầu của $$g$$ và tiếp tục làm ngược lại sẽ ra các bit của flag.

Flag: _CCTF{\_how\_finD\_7h1s\_1z\_s3cr3T?!}_

### Maid

```python
#!/usr/bin/python3

from Crypto.Util.number import *
from gmpy2 import *
from secret import *
from flag import flag

global nbit
nbit = 1024

def keygen(nbit):
	while True:
		p, q = [getStrongPrime(nbit) for _ in '01']
		if p % 4 == q % 4 == 3:
			return (p**2)*q, p

def encrypt(m, pubkey):
	if GCD(m, pubkey) != 1 or m >= 2**(2*nbit - 2):
		return None
	return pow(m, 2, pubkey)

def flag_encrypt(flag, p, q):
	m = bytes_to_long(flag)
	assert m < p * q
	return pow(m, 65537, p * q)

def die(*args):
	pr(*args)
	quit()

def pr(*args):
	s = " ".join(map(str, args))
	sys.stdout.write(s + "\n")
	sys.stdout.flush()

def sc():
	return sys.stdin.readline().strip()

def main():
	border = "+"
	pr(border*72)
	pr(border, "  hi all, welcome to Rooney Oracle, you can encrypt and decrypt any ", border)
	pr(border, "  message in this oracle, but the flag is still encrypted, Rooney   ", border)
	pr(border, "  asked me to find the encrypted flag, I'm trying now, please help! ", border)
	pr(border*72)

	pubkey, privkey = keygen(nbit)
	p, q = privkey, pubkey // (privkey ** 2)

	while True:
		pr("| Options: \n|\t[E]ncrypt message \n|\t[D]ecrypt ciphertext \n|\t[S]how encrypted flag \n|\t[Q]uit")
		ans = sc().lower()
		if ans == 'e':
			pr("| Send the message to encrypt: ")
			msg = sc()
			try:
				msg = int(msg)
			except:
				die("| your message is not integer!!")
			pr(f"| encrypt(msg, pubkey) = {encrypt(msg, pubkey)} ")
		elif ans == 'd':
			pr("| Send the ciphertext to decrypt: ")
			enc = sc()
			try:
				enc = int(enc)
			except:
				die("| your message is not integer!!")
			pr(f"| decrypt(enc, privkey) = {decrypt(enc, privkey)} ")
		elif ans == 's': 
			pr(f'| enc = {flag_encrypt(flag, p, q)}')
		elif ans == 'q':
			die("Quitting ...")
		else:
			die("Bye ...")

if __name__ == '__main__':
	main()
```

Ở bài này server cung cấp cho mình các chứng năng sau:

* Encrypt 1 số bất kì không vượt quá $$2^{2048 - 2}$$ bit
* Decrypt 1 số bất kì (hàm decrypt bị giấu đi)
* Lấy flag bị mã hóa

Key là 1 cặp khóa công khai-bí mật $$(pubkey, privkey)$$, trong đó $$pubkey = p^2q$$ còn $$privkey = p^2$$, với $$p$$ và $$q$$ là 2 số nguyên tố 1024 bit và đồng dư 3 modulo 4. Hàm **encrypt** thực hiện mã hóa số $$m$$ bằng cách trả về $$m^2 \pmod{pubkey}$$. Còn hàm **decrypt** thực hiện giải mã chỉ cần $$privkey$$.

Kì cục ..............

Thế quái nào ..............

Mà **encrypt** cần cả $$p$$ và $$q$$ còn **decrypt** chỉ cần $$p$$?

Thật ra là vì nếu $$c \equiv m^2 \pmod{pubkey}$$ thì $$c \equiv m^2 \pmod{p^2}$$, như vậy giải thích cho việc $$m$$ không được vượt quá 2048-2 bit và việc giải mã chỉ cần $$p$$. Như vậy cách attack của mình như sau:

* Chọn ngẫu nhiên các ciphertext, gửi lên để server decrypt và nhận lại các plaintext tương ứng. Ta biết rằng $$c \equiv m^2 \pmod{p^2}$$ nên $$p^2 = \gcd(m_1^2 - c_1, m_2^2 - c_2)$$, từ đó lấy căn bậc 2 là có $$p$$.
* Tiếp theo, chọn ngẫu nhiên các plaintext, gửi lên server encrypt và nhận lại ciphertext tươngg ứng. Do $$c \equiv m^2 \pmod{pubkey} \equiv m^2 \pmod{p^2q}$$, khi đó $$p^2q = \gcd(m_1^2 - c_1, m_2^2 - c_2)$$. Việc này ngược lại quá trình trên vì như nãy mình đã nói, **encrypt** sử dụng $$p^2q$$ còn **decrypt** thì chỉ cần $$p^2$$.
* Và bây giờ $$p$$ và $$q$$ đã có đủ, ta decrypt và có flag thôi

Flag: _CCTF{\_\_\_Ra8!N\_H\_Cryp70\_5YsT3M\_\_\_}_

### Tuti

```python
#!/usr/bin/env python3

from Crypto.Util.number import *
from flag import flag

l = len(flag)
m_1, m_2 = flag[: l // 2], flag[l // 2:]

x, y = bytes_to_long(m_1), bytes_to_long(m_2)

k = '''
000bfdc32162934ad6a054b4b3db8578674e27a165113f8ed018cbe9112
4fbd63144ab6923d107eee2bc0712fcbdb50d96fdf04dd1ba1b69cb1efe
71af7ca08ddc7cc2d3dfb9080ae56861d952e8d5ec0ba0d3dfdf2d12764
'''.replace('\n', '')

assert((x**2 + 1)*(y**2 + 1) - 2*(x - y)*(x*y - 1) == 4*(int(k, 16) + x*y))
```

Ở đây $$x$$ và $$y$$ là nửa đầu và nửa sau của flag, $$k$$ là một số cho trước thỏa mãn $$(x^2+1)(y^2+1)-2(x-y)(xy-1) = 4(k+xy)$$. Biến đổi một tí mình có

$$x^2 y^2 + x^2 + y^2 + 1 - 2(x-y)xy+2(x-y)-4xy = 4k$$

$$\Leftrightarrow x^2 y^2 + (x^2 + y^2 + 1 + 2(x-y) - 2xy) - 2(x-y+1)xy = 4k$$

$$\Leftrightarrow x^2 y^2 + (x-y+1)^2 - 2(x-y+1)xy = 4k$$

$$\Leftrightarrow (xy - x + y - 1)^2 = 4k$$

Như vậy $$xy-x+y-1=\sqrt{4k}$$ mà $$xy-x+y-1=(x+1)(y-1)$$ nên mình chỉ cần factor số này là tìm được $$x$$ và $$y$$. Do có thể có nhiều cách chọn nên mình tìm cái "hợp lí" nhất

Flag: _CCTF{S1mPL3\_4Nd\_N!cE\_Diophantine\_EqUa7I0nS!}_

### Improve

```python
#!/usr/bin/env python3

from Crypto.Util.number import *
from gmpy2 import gcd
from random import randint
import sys, hashlib
from flag import flag

def lcm(a, b):
	return (a * b) // gcd(a,b)

def gen_params(nbit):
	p, q = [getPrime(nbit) for _ in range(2)]
	n, f, g = p * q, lcm(p-1, q-1), p + q
	e = pow(g, f, n**2)
	u = divmod(e-1, n)[0]
	v = inverse(u, n)
	params = int(n), int(f), int(v)
	return params

def improved(m, params):
	n, f, v = params
	if 1 < m < n**2 - 1:
		e = pow(m, f, n**2)
		u = divmod(e-1, n)[0]
		L = divmod(u*v, n)[1]
	H = hashlib.sha1(str(L).encode('utf-8')).hexdigest()
	return H

def die(*args):
	pr(*args)
	quit()

def pr(*args):
	s = " ".join(map(str, args))
	sys.stdout.write(s + "\n")
	sys.stdout.flush()

def sc():
	return sys.stdin.readline().strip()

def main():
	border = "+"
	pr(border*72)
	pr(border, " hi talented cryptographers! Your mission is to find hash collision ", border)
	pr(border, " in the given hash function based on famous cryptographic algorithm ", border)
	pr(border, " see the source code and get the flag! Its improved version :)      ", border)
	pr(border*72)

	nbit = 512
	params = gen_params(nbit)
	n = params[0]

	while True:
		pr("| Options: \n|\t[R]eport collision! \n|\t[T]ry hash \n|\t[G]et parameters \n|\t[Q]uit")
		ans = sc().lower()
		if ans == 'r':
			pr("| please send the messages split by comma: ")
			m = sc()
			try:
				m_1, m_2 = m.split(',')
				m_1, m_2 = int(m_1), int(m_2)
			except:
				die("| Sorry! your input is invalid, Bye!!")
				# fix the bug :P
			if m_1 % n != 0 and m_2 % n != 0 and m_1 != m_2 and 1 < m_1 < n**2-1 and 1 < m_2 < n**2-1 and improved(m_1, params) == improved(m_2, params):
				die(f"| Congrats! You find the collision!! the flag is: {flag}")
			else:
				die("| Sorry! your input is not correct!!")
		elif ans == 't':
			pr("| Please send your message to get the hash: ")
			m = sc()
			try:
				m = int(m)
				pr(f"improved(m) = {improved(m, params)}")
			except:
				die("| Sorry! your input is invalid, Bye!!") 
		elif ans == 'g':
			pr('| Parameters =', params)
		elif ans == 'q':
			die("Quitting ...")
		else:
			die("Bye ...")

if __name__ == '__main__':
	main()
```

Ở bài này khá có khá nhiều thứ linh tinh nhưng chung quy lại là mình cần nhập vào 2 số khác nhau $$m_1$$ và $$m_2$$ khác $$n$$ sao cho kết quả hàm **improve** với 2 số này là giống nhau.

Các tham số sẽ là $$n$$ làm chặn trên cho 2 số nhập vào (không vượt quá $$n^2$$, và $$f$$ có tính chất quan trọng là luôn chẵn, đây là tiền đề để mình giải bài này.

Hàm **improve** mình để ý rằng $$L$$ được tạo ra sau vài biến đổi từ $$e=m^f \pmod{n^2}$$, mà mình cần 2 số $$m$$ cho cùng $$L$$, vậy chỉ cần cho ra cùng $$e$$ là xong. Mà như hồi nãy mình có đề cập là $$f$$ luôn chẵn, vậy chỉ cần chọn $$m$$ và $$n^2-m$$ là xong :))

Flag: _CCTF{Phillip\_N0W\_4\_pr0b4b1liStiC\_\_aSymM3Tr1C\_\_AlGOrithM!!}_

### Onlude

```python
#!/usr/bin/env sage

from sage.all import *
from flag import flag

global p, alphabet
p = 71
alphabet = '=0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ$!?_{}<>'

flag = flag.lstrip('CCTF{').rstrip('}')
assert len(flag) == 24

def cross(m):
	return alphabet.index(m)

def prepare(msg):
	A = zero_matrix(GF(p), 11, 11)
	for k in range(len(msg)):
		i, j = 5*k // 11, 5*k % 11
		A[i, j] = cross(msg[k])
	return A

def keygen():
	R = random_matrix(GF(p), 11, 11)
	while True:
		S = random_matrix(GF(p), 11, 11)
		if S.rank() == 11:
			_, L, U = S.LU()
			return R, L, U

def encrypt(A, key):
	R, L, U = key
	S = L * U
	X = A + R
	Y = S * X
	E = L.inverse() * Y
	return E

A = prepare(flag)
key = keygen()
R, L, U = key
S = L * U
E = encrypt(A, key)
print(f'E = \n{E}')
print(f'L * U * L = \n{L * U * L}')
print(f'L^(-1) * S^2 * L = \n{L.inverse() * S**2 * L}')
print(f'R^(-1) * S^8 = \n{R.inverse() * S**8}')
```

Bài này mình giải trước khi hết thời gian 1 tiếng và là bài cuối cùng mình giải được. Hàm **prepare** chuyển flag thành ma trận $$A$$, $$key$$ là bộ 3 ma trận $$R$$, $$L$$ và $$U$$. Ma trận $$S=L U$$

Việc mã hóa như sau:

* Với $$R$$, $$L$$ và $$U$$ như trên, $$S = LU$$
* $$X=A+R$$, $$Y=SX$$ và ciphertext là $$E=L^{-1}Y$$

Đề cho mình 4 ma trận:

* $$E$$ là ciphertext, với 1 chút biến đổi mình có $$E=U(A+R)$$
* Ma trận $$L U L$$
* Ma trận $$L^{-1} S^2 L = L^{-1} (LU)^2 L = L^{-1}LULUL=(UL)^2$$, mình đặt là $$T$$
* Ma trận $$R^{-1}S^8$$, mình đặt là $$W$$

Lấy $$LUL$$ nhân với $$T$$ mình có $$LUL \cdot (UL)^2 = L(UL)^3$$. Khi đó $$T^2 [L(UL)^3]^{-1} = (UL)^4 \cdot (UL)^{-3} \cdot L^{-1} = UL \cdot L^{-1} = U$$. Vậy là mình có $$U$$ rồi :))

Quay lại $$E=U(A+R)$$, khi đó $$R=U^{-1}E-A$$, nhân bên phải của 2 vế với $$W$$ thì $$R \cdot R^{-1} S^8 = (U^{-1} E - A) W = S^8 = (LU)^8$$

Quay lại 1 chút, $$(LUL) \cdot T^3 = (LUL) \cdot (L^{-1}S^6L) = (LU)^7 \cdot L$$, suy ra $$(LUL) \cdot T^3 \cdot U = (LU)^8$$

Từ đó mình dễ dàng tìm lại được $$A = U^{-1}E - (LU)^8 W^{-1}$$

Thực hiện tương tự hàm **prepare** mình có được flag

Flag: _CCTF{LU\_\_D3c0mpO517Ion\_\_4L90?}_

Writeup đến đây là hết, cám ơn các bạn đã đọc. Source code của mình ở [đây](https://github.com/dunglq2000/CTF/tree/master/CryptoCTF/2021)
