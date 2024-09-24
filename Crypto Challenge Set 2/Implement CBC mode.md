<h1><b>Implement CBC mode</h1></b>
<pre>
<a href='https://cryptopals.com/static/challenge-data/10.txt'>The file here</a> is intelligible (somewhat) when CBC decrypted against "YELLOW SUBMARINE" with an IV of all ASCII 0 (\x00\x00\x00 &c)
<b>
Don't cheat.
Do not use OpenSSL's CBC code to do CBC mode, even to verify your results. What's the point of even doing this stuff if you aren't going to learn from it?</b>
</pre>
</b><h3>Solution</h3></b>

<p>Diketahui bahwa AES mode CBC merupakan salah satu operasi dari AES, selain ECB yang sebelumnya kita bahas. Pada AES mode CBC memiliki tingkat keamanan yang lebih dibandingkan 
mode ECB karena pada operasi Encryption CBC tidak akan membentuk pola plaintext yang terjadi pada ECB, ini dikarenakan pada CBC memiliki IV atau Initial Vector untuk setiap proses block encryption seperti pada gambar dibawah ini</p>
<p align=center>
  <img src='https://github.com/enomarozi/Writeup-CTF_Online/blob/master/BackdoorCTF/Images/1920px-CBC_encryption.svg.png' width=600>
</p>
<p>Proses pertama melakukan operasi XOR antara block pertama plaintext dengan IV(Initial Vector) dan dilanjutkan proses encryption dengan Key, yang kemudian hasil ciphertext akan menjadi 
IV(Initial Vector) untuk block plaintext selanjutnya dan begitu seterusnya hingga seluruh pesan ter-encrytion</p>
<p>Dan untuk proses Decryption</p>
<p align=center>
  <img src='https://github.com/enomarozi/Writeup-CTF_Online/blob/master/BackdoorCTF/Images/600px-CBC_decryption.svg.png' width=600>
</p>
<p>Prosesnya kebalikan dari encrytion, yaitu block pertama ciphertext akan di decrypt dengan Key dan kemudian hasilnya di-XOR dengan IV(Initial Vector) yang akan mendapatkan plaintext block pertama, 
tetapi ciphertext block pertama juga menjadi IV(Initial Vector) untuk memperoleh plaintext block ke-2 dari hasil operasi XOR, dan begitu seterusnya</p>
<p>Dan untuk soal kita diminta untuk mendecrypt ciphertext pada file dengan key "YELLOW SUBMARINE" dan IV(initial vector) "0000000000000000"</p>

```python
import base64
from Crypto.Cipher import AES

file = open("10.txt","rb").read()
decode = base64.b64decode(file)
IV = ("0"*16).encode('utf8')
key = "YELLOW SUBMARINE".encode('utf8')
AES_Decryption = AES.new(key, AES.MODE_CBC, IV)
decrypt = AES_Decryption.decrypt(decode).decode('ascii')
print(decrypt)
```
<p>Dari program diatas kita sudah mendapatkan plaintext dari ciphertext, tetapi kita tidak boleh menggunakan cheat, yang artinya cara simple seperti program diatas</p>
<p>Dan disini kita akan mencoba mengikuti proses decryption yang sudah saya jelaskan diatas, dengan bantuan looping program untuk setiap 16 bytes block chipertext, seperti pada program dibawah</p>

```python
import base64
from Crypto.Cipher import AES

file = open("10.txt").read()
decode = base64.b64decode(file)
hexa = ''.join([hex(i)[2:].rjust(2,'0') for i in decode])
result = [hexa[:i][-32:] for i in range(32,len(hexa)+32,32)]
IV = b"0000000000000000"
key = b"YELLOW SUBMARINE"
for i in range(len(result)):
    AES_Decryption = AES.new(key,AES.MODE_CBC,IV)
    decrypt = AES_Decryption.decrypt(bytes.fromhex(result[i]))
    IV = bytes.fromhex(result[i])
    print(decrypt.decode('ascii')) 
```
<p>Dan kita mendapatkan padding sepanjang 4 bytes diakhir plaintext</p>
</b><h3>Result</h3></b>
<pre>
y\x17]\x10RQS[\x10Q^T\x10y\x17]
 ringin' the bel
l \nA rockin' on 
the mike while t
he fly girls yel
l \nIn ecstasy in
 the back of me 
\nWell that's my 
DJ Deshay cuttin
' all them Z's \n
Hittin' hard and
 the girlies goi
n' crazy \nVanill
a's on the mike,
 man I'm not laz
y. \n\nI'm lettin'
 my drug kick in
 \nIt controls my
 mouth and I beg
in \nTo just let 
it flow, let my 
concepts go \nMy 
posse's to the s
ide yellin', Go 
Vanilla Go! \n\nSm
ooth 'cause that
's the way I wil
l be \nAnd if you
 don't give a da
mn, then \nWhy yo
u starin' at me 
\nSo get off 'cau
se I control the
 stage \nThere's 
no dissin' allow
ed \nI'm in my ow
n phase \nThe gir
lies sa y they l
ove me and that 
is ok \nAnd I can
 dance better th
an any kid n' pl
ay \n\nStage 2 -- 
Yea the one ya' 
wanna listen to 
\nIt's off my hea
d so let the bea
t play through \n
So I can funk it
 up and make it 
sound good \n1-2-
3 Yo -- Knock on
 some wood \nFor 
good luck, I lik
e my rhymes atro
cious \nSupercala
fragilisticexpia
lidocious \nI'm a
n effect and tha
t you can bet \nI
 can take a fly 
girl and make he
r wet. \n\nI'm lik
e Samson -- Sams
on to Delilah \nT
here's no denyin
', You can try t
o hang \nBut you'
ll keep tryin' t
o get my style \n
Over and over, p
ractice makes pe
rfect \nBut not i
f you're a loafe
r. \n\nYou'll get 
nowhere, no plac
e, no time, no g
irls \nSoon -- Oh
 my God, homebod
y, you probably 
eat \nSpaghetti w
ith a spoon! Com
e on and say it!
 \n\nVIP. Vanilla 
Ice yep, yep, I'
m comin' hard li
ke a rhino \nInto
xicating so you 
stagger like a w
ino \nSo punks st
op trying and gi
rl stop cryin' \n
Vanilla Ice is s
ellin' and you p
eople are buyin'
 \n'Cause why the
 freaks are jock
in' like Crazy G
lue \nMovin' and 
groovin' trying 
to sing along \nA
ll through the g
hetto groovin' t
his here song \nN
ow you're amazed
 by the VIP poss
e. \n\nSteppin' so
 hard like a Ger
man Nazi \nStartl
ed by the bases 
hittin' ground \n
There's no tripp
in' on mine, I'm
 just gettin' do
wn \nSparkamatic,
 I'm hangin' tig
ht like a fanati
c \nYou trapped m
e once and I tho
ught that \nYou m
ight have it \nSo
 step down and l
end me your ear 
\n'89 in my time!
 You, '90 is my 
year. \n\nYou're w
eakenin' fast, Y
O! and I can tel
l it \nYour body'
s gettin' hot, s
o, so I can smel
l it \nSo don't b
e mad and don't 
be sad \n'Cause t
he lyrics belong
 to ICE, You can
 call me Dad \nYo
u're pitchin' a 
fit, so step bac
k and endure \nLe
t the witch doct
or, Ice, do the 
dance to cure \nS
o come up close 
and don't be squ
are \nYou wanna b
attle me -- Anyt
ime, anywhere \n\n
You thought that
 I was weak, Boy
, you're dead wr
ong \nSo come on,
 everybody and s
ing this song \n\n
Say -- Play that
 funky music Say
, go white boy, 
go white boy go 
\nplay that funky
 music Go white 
boy, go white bo
y, go \nLay down 
and boogie and p
lay that funky m
usic till you di
e. \n\nPlay that f
unky music Come 
on, Come on, let
 me hear \nPlay t
hat funky music 
white boy you sa
y it, say it \nPl
ay that funky mu
sic A little lou
der now \nPlay th
at funky music, 
white boy Come o
n, Come on, Come
 on \nPlay that f
unky music \n\x04\x04\x04\x04
</pre>
