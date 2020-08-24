<h1><b>Implement PKCS#7 padding</h1></b>
<pre>
<b>"YELLOW SUBMARINE"</b>
... padded to 20 bytes would be:
<b>"YELLOW SUBMARINE\x04\x04\x04\x04"</b>
</pre>
</b><h3>Solution</h3></b>
<p>Padding merupakan penambahan/penyempurnaan dari block cipher yang panjangan dari block terakhir tidak lengkap. Biasanya setiap block cipher terdiri dari 8 atau 16 character (tidak bisa kurang/lebih),
 dan apa yang terjadi jika pada block terakhir hanya terdapat 14 block? maka akan ada penambahan bytes atau dinamakan padding.</p>
<p>PKCS#7 merupakan implementasi padding pada block cipher yang mana setiap block encryptions tidak harus 8 atau 16 bytes, yang bisa kita set blocknya sesuai yang kita inginkan</p>
<p>Contohnya pada soal "YELLOW SUBMARINE" merupakan Fix block (16 bytes) jika tanpa menggunakan/implementasi PKCS#7, dan jika kita implementasikan PKCS#7 yaitu padding 20 bytes, 
maka akan menghasilkan (encryption to decryption) 
"YELLOW SUBMARINE\x04\x04\x04\x04" yang blocknya = 20 bytes</p>
<p>Penempatan block padding pada ciphertext atau plaintext, sebagai berikut</p>
<pre>
Jika 1 bytes padding -> \x01
Jika 2 bytes padding -> \x02\x02
Jika 3 bytes padding -> \x03\x03\x03
Jika 4 bytes padding -> \x04\x04\x04\x04
Jika 5 bytes padding -> \x05\x05\x05\x05\x05
.........................................etc
</pre>
<p>Berikut contoh program PKCS#7 python</p>

```python
from Crypto.Util.Padding import pad

block_size = 20
data = b'YELLOW SUBMARINE'
result = pad(data,block_size)
print(str(result)[2:-1]) #YELLOW SUBMARINE\x04\x04\x04\x04
```
<p>Atau Cara manual</p>

```python
text = "Eno Marozi"
block = 13
padding = block - len(text)
for i in range(padding):
    text += "\\x0"+str(padding)
print(text) #Eno Marozi\x03\x03\x03
```
</b><h3>Result</h3></b>
<pre>
YELLOW SUBMARINE\x04\x04\x04\x04
</pre>
