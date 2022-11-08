# AES

AES là block cipher (mã hóa khối) có độ an toàn cao nhất hiện nay.

Một block của AES gồm 16 bytes, trong khi độ dài key cho phép 16, 24 hoặc 32 bytes.

AES thực hiện 4 động tác sau để biến đổi plaintext và key tạo thành ciphertext:

1. AddRoundKey
2. SubBytes
3. ShiftRows
4. MixColumn

4 động tác trên được thực hiện theo số lần tùy theo độ dài key. Do đó chúng ta cần một hàm dựa trên độ dài key mà tạo ra các key con dành cho việc mã hóa ở mỗi lần. Hàm này là ExpandKey.
