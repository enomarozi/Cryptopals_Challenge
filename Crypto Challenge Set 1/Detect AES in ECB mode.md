<h1><b>Detect AES in ECB mode</h1></b>
<pre>
<a href='https://cryptopals.com/static/challenge-data/8.txt'>In this file</a> are a bunch of hex-encoded ciphertexts.

One of them has been encrypted with ECB.

Detect it.

Remember that the problem with ECB is that it is stateless and deterministic; the same 16 byte plaintext block will always produce the same 16 byte ciphertext.
</pre>
</b><h3>Solution</h3></b>
<p>Berikut operasi dari ECB</p>
<p align='center'>
  <img src='https://github.com/enomarozi/Writeup-CTF_Online/blob/master/BackdoorCTF/Images/601px-ECB_encryption.svg.png'>
</p>
<p>ECB beroperasi dengan me-encrypt suatu block pesan yang dibagi per block, yaitu 1 block = 8,16 atau 32 character</p>
<p>Sudah terdapat pada <a href='https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation'>Wikipedia</a> bahwa mode ECB merupakan mode encryption yang lemah, karena kita dapat mengetahui pola dari encryption
Contohnya pada kedua gambar dibawah ini, yang me-encrypt setiap warna pada pixel yang dianggap berupa block dengan kunci tertentu</p>
<p align='center'>
  <img src='https://github.com/enomarozi/Writeup-CTF_Online/blob/master/BackdoorCTF/Images/plaintext_TUX.jpg'>
  <img src='https://github.com/enomarozi/Writeup-CTF_Online/blob/master/BackdoorCTF/Images/ciphertext_TUX.jpg'>
</p>
<p>Dan dapat dilihat hasil image chipertext masih menyerupai image plaintext dari polanya</p>
<p>Jadi, untuk soal diatas terdapat 204 ciphertext</p>

```console
root@Python:/home/venom/Downloads# wc -l 8.txt 
204 8.txt
root@Python:/home/venom/Downloads# 
```
</p>Dan kita akan memeriksa setiap 204 ciphertext yang salah satunya merupakan encrypted dari AES mode ECB, kita bisa membagi setiap hexa kedalam setiap block, 1 block terdapat 32 hexadesimal = 16 character</p>

```python
file = open("8.txt")
for i in file:
    i = i.strip()
    result = [i[:j][-32:] for j in range(32,len(i)+32,32)]
    ECB = len(result)-len(set(result))
    if ECB > 0:
        print("Encryption :",i)
        print("Semua Block :",result)
        print("Block yang sama :",set(result))

```
<p>Output Program</p>
<pre>
Encryption : d880619740a8a19b7840a8a31c810a3d08649af70dc06f4fd5d2d69c744cd283e2dd052f6b641dbf9d11b0348542bb5708649af70dc06f4fd5d2d69c744cd2839475c9dfdbc1d46597949d9c7e82bf5a08649af70dc06f4fd5d2d69c744cd28397a93eab8d6aecd566489154789a6b0308649af70dc06f4fd5d2d69c744cd283d403180c98c8f6db1f2a3f9c4040deb0ab51b29933f2c123c58386b06fba186a
Semua Block : ['d880619740a8a19b7840a8a31c810a3d', '08649af70dc06f4fd5d2d69c744cd283', 'e2dd052f6b641dbf9d11b0348542bb57', '08649af70dc06f4fd5d2d69c744cd283', '9475c9dfdbc1d46597949d9c7e82bf5a', '08649af70dc06f4fd5d2d69c744cd283', '97a93eab8d6aecd566489154789a6b03', '08649af70dc06f4fd5d2d69c744cd283', 'd403180c98c8f6db1f2a3f9c4040deb0', 'ab51b29933f2c123c58386b06fba186a']
Block yang sama : {'d880619740a8a19b7840a8a31c810a3d', '08649af70dc06f4fd5d2d69c744cd283', '97a93eab8d6aecd566489154789a6b03', 'e2dd052f6b641dbf9d11b0348542bb57', '9475c9dfdbc1d46597949d9c7e82bf5a', 'ab51b29933f2c123c58386b06fba186a', 'd403180c98c8f6db1f2a3f9c4040deb0'}
</pre>
<p>Dan didapatkan hasilnya yaitu pada encryption line 133, yaitu block 2,4,6 dan 8 merupakan block encryption yang sama</p>
</b><h3>Result</h3></b>
<pre>
d880619740a8a19b7840a8a31c810a3d08649af70dc06f4fd5d2d69c744cd283e2dd052f6b641dbf9d11b0348542bb5708649af70dc06f4fd5d2d69c744cd2839475c9dfdbc1d46597949d9c7e82bf5a08649af70dc06f4fd5d2d69c744cd28397a93eab8d6aecd566489154789a6b0308649af70dc06f4fd5d2d69c744cd283d403180c98c8f6db1f2a3f9c4040deb0ab51b29933f2c123c58386b06fba186a
</pre>
