<h1><b>Detect single-character XOR</h1></b>
<pre>
One of the 60-character strings in this <a href='https://cryptopals.com/static/challenge-data/4.txt'>file</a> has been encrypted by single-character XOR.
Find it.
</pre>
</b><h3>Solution</h3></b>

```console
root@Python:/home/venom/Downloads# wc -l 4.txt 
326 4.txt
```
<p>Terdapat 326 chipertext, kita diminta untuk mendapatkan plaintext dari semua kemungkinan kunci yaitu character 1 s/d 60. 
Yang nantinya kita akan mendapatkan 326 * 60 yaitu 19560 kemungkinan plaintext</p>

```python
def xoor(n):
    listing = [i for i in range(33,65)]
    file = open("4.txt")
    for i in file:
        i = i.strip('\n')
        result = ""
        for j in bytes.fromhex(i):
            compute = j^n
            if compute > 31 and compute < 127:
                if compute not in listing:
                    result += chr(compute)
        if len(result) >= 28:
            print("Hexa encode -->",i,"\nKey -->",n,"\nPlaintext -->",result)
        
for j in range(61):
    xoor(j)
```
<p>Output Program</p>
<pre>
Hexa encode --> 7b5a4215415d544115415d5015455447414c155c46155f4058455c5b523f 
Key --> 53 
Plaintext --> Now that the party is jumping
</pre>
</b><h3>Result</h3></b>
<pre>
Now that the party is jumping
</pre>
