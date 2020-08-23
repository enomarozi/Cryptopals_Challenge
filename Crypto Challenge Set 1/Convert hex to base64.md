<h1><b>Convert hex to base64</h1></b>
<pre>
The string:

49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d
</pre>
</b><h3>Solution</h3></b>
<p>Convert hexa to ascii dan encode ke base64</p>

```python
import base64

hexa = "49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d"
raw_bytes = base64.b64encode(bytes.fromhex(hexa))
print(str(raw_bytes)[2:-1])
```
</b><h3>Result</h3></b>
<pre>
SSdtIGtpbGxpbmcgeW91ciBicmFpbiBsaWtlIGEgcG9pc29ub3VzIG11c2hyb29t
</pre>
