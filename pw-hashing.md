# Password hashing
## Good to know...
## This is a learning note from cs253 of Udacity
Python has an awesome library called hashlib, which contains
a bunch of existing hashing algorithms, like md5, sha256, etc.
This note is about hashing with salts.

### First thing first, what's a hashing algorithm?
A hashing algorithm takes a string (let's just consider string)
as input and returns a longer, harder to 'understand' string as
the secret version of the input string.
For example, consider a hashing algorithm H(x):

```
H('hello') = '5d41402abc4b2a76b9719d911017c592'
```

Now, given the same string as input, H(x) will generate the same
output. One example can be:

```python
import hashlib


def str_hash(s):
    # s: string to hashed
    # h: hashed string
    # returns "s,h"
    return "{},{}".format(s, hashlib.md5(s).hexdigest())


def str_verify(sh):
    # sh: hashed string "s,h" where s is the original string and
    # h is the hashed string
    s = sh.split(",")[0]
    return str_hash(s) == sh

```

