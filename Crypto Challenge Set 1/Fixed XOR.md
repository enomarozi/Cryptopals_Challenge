<h1><b>Fixed XOR</h1></b>
<pre>
Hexa_1 = 1c0111001f010100061a024b53535009181c
Hexa_2 = 686974207468652062756c6c277320657965
</pre>
</b><h3>Solution</h3></b>
<p>Lakukan operasi XOR terhadap kedua nilai Hexadesimal, yang operasi XOR dilakukan per 1 bytes Hexadesimal yang secara berurut hingga 1 bytes Hexadesimal terakhir</p>

```python
result_hex = ''
result_txt = ''
def split_bytes(text):
    data = [text[:i][-2:] for i in range(2,len(text)+2,2)]
    return data

str_ = split_bytes("1c0111001f010100061a024b53535009181c")
xor_ = split_bytes("686974207468652062756c6c277320657965")
for i,j in zip(str_,xor_):
    result_hex += hex(int(i,16)^int(j,16))[2:].rjust(2,'0')
    result_txt += chr(int(i,16)^int(j,16))
    
print("Result Hexa : ",result_hex)
print("Result Text : ",result_txt)

```
<p>Output</p>
<pre>
Result Hexa :  746865206b696420646f6e277420706c6179
Result Text :  the kid don't play
</pre>
</b><h3>Result</h3></b>
<pre>
746865206b696420646f6e277420706c6179
</pre>
