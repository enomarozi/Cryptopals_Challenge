<h1><b>
Implement repeating-key XOR</h1></b>
<pre>
Here is the opening stanza of an important work of the English language:
<b>
Burning 'em, if you ain't quick and nimble
I go crazy when I hear a cymbal
</b>
Encrypt it, under the key "ICE", using repeating-key XOR.
</pre>
</b><h3>Solution</h3></b>
<p>Lakukan Operasi XOR dengan Key "ICE" berulang-ulang kali, hingga bytes text terakhir</p>

```python
text = '''Burning 'em, if you ain't quick and nimble
I go crazy when I hear a cymbal'''
key = "ICE"*len(text)
for i,j in zip(text,key):
    print(hex(ord(i)^ord(j))[2:].rjust(2,'0'),end='')  
```
</b><h3>Result</h3></b>
<pre>
0b3637272a2b2e63622c2e69692a23693a2a3c6324202d623d63343c2a26226324272765272
a282b2f20430a652e2c652a3124333a653e2b2027630c692b20283165286326302e27282f
</pre>
