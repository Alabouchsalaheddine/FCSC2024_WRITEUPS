# Layer Cake 1/3

## Challenge Overview
- **Points:** 20
- **Original French description:** J'ai chiffré le flag avec le cryptosystème à clé publique bien connu RSA.
- **Translated Description :** I encrypted the flag using the well-known RSA public-key cryptosystem.


## Solution

- **Requirements:** 
```bash
pip install pycryptodome
```
- **Code :** 

```python
import json
from Crypto.Util.number import long_to_bytes
from Crypto.Util.number import getPrime, bytes_to_long
from Crypto.Util.number import inverse


def calculate_private_exponent(p, q, e):
    phi = (p - 1) * (q - 1)
    d = inverse(e, phi)
    return d

# Read the ciphertext and public key from the JSON
with open("output.txt") as f:
    data = json.load(f)
e = data["e"]
n = data["n"]
c = data["c"]

# Example values (replace with your actual prime factors and public exponent)
p = getPrime(1024)
q = getPrime(1024)

# Calculate private exponent
d = calculate_private_exponent(p, q, e)

# Define the private key components
d = 65537  # Example private exponent

# Decrypt the ciphertext
m = pow(c, d, n)

# Convert the plaintext to bytes
message_bytes = long_to_bytes(m)
print(message_bytes)
# Decode bytes to string using UTF-8 encoding
message_string = message_bytes.decode('utf-8')

# Output the decrypted message
print("Decrypted Message:", message_string)
  
```

- **Flag:** 
FCSC{7264bd2db7fae77e0c4e2445e45ed89fbe98f7c1bc8e7796111e32654f1ad1f0}
