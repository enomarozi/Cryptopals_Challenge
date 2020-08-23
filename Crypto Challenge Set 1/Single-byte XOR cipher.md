<h1><b>Single-byte XOR cipher</h1></b>
<pre>
The hex encoded string:
1b37373331363f78151b7f2b783431333d78397828372d363c78373e783a393b3736

... has been XOR'd against a single character. Find the key, decrypt the message.
</pre>
</b><h3>Solution</h3></b>
<p>Xor setiap bytes hexa dengan 1 character</p>

```python
def xoor(n):
    hexa = "1b 37 37 33 31 36 3f 78 15 1b 7f 2b 78 34 31 33 3d 78 39 78 28 37 2d 36 3c 78 37 3e 78 3a 39 3b 37 36".split(" ")
    result = ""
    for i in hexa:
        result += chr(int(i,16)^n)
    if "Cooking" in result:
        print(result,"And key is",chr(n))
for j in range(100):
    xoor(j)
```
<p>Output Program</p>
<pre>
Message is Cooking MC's like a pound of bacon 
And key is X
</pre>
</b><h3>Flag</h3></b>
<pre>
Cooking MC's like a pound of bacon 
</pre>
