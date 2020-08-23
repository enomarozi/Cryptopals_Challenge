<h1><b>Fixed XOR</h1></b>
<pre>
Hexa_1 = 1c0111001f010100061a024b53535009181c
Hexa_2 = 686974207468652062756c6c277320657965
</pre>
</b><h3>Solution</h3></b>
<p>Lakukan operasi XOR terhadap kedua nilai Hexadesimal</p>

```python
hexa1 = 0x1c0111001f010100061a024b53535009181c
hexa2 = 0x686974207468652062756c6c277320657965
result = hex(hexa1^hexa2)[2:]
print(result," --> ",str(bytes.fromhex(result))[2:-1])
```
<p>Output</p>
<pre>
746865206b696420646f6e277420706c6179  -->  the kid don't play
</pre>
</b><h3>Result</h3></b>
<pre>
746865206b696420646f6e277420706c6179
</pre>
