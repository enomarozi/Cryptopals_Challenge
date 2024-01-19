<h1><b>Convert hex to base64</h1></b>
<pre>
The string:

49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d
</pre>
</b><h3>Solution</h3></b>
<p>Convert hexa to ascii dan encode ke base64</p>

```python
ascii_base64 = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"

hexa = '49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d'
result_step1 = ''.join([bin(int(hexa[:i][-2:],16))[2:].rjust(8,'0') for i in range(2,len(hexa)+2,2)])
result_step2 = ''.join([ascii_base64[int(result_step1[:i][-6:].rjust(8,'0'),2)] for i in range(6,len(result_step1)+6,6)])
data = ''.join([chr(int(hexa[:i][-2:],16)) for i in range(2,len(hexa)+2,2)])
print("Result Base64 :",result_step2)
print("Result Decode :",data)
```
<p>Output</p>
<pre>
  Result Base64 : SSdtIGtpbGxpbmcgeW91ciBicmFpbiBsaWtlIGEgcG9pc29ub3VzIG11c2hyb29t
  Result Decode : I'm killing your brain like a poisonous mushroom
</pre>
</b><h3>Result</h3></b>
<pre>
SSdtIGtpbGxpbmcgeW91ciBicmFpbiBsaWtlIGEgcG9pc29ub3VzIG11c2hyb29t
</pre>
