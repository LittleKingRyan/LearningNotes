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
The characteristics of a hashing algorithm are:
1. difficult to generate a specific output string
2. infeasible to find input string for a given output string
3. can't modify input string without modifying output string

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

s = "hello"
sh = str_hash(s) # sh: 'hello,5d41402abc4b2a76b9719d911017c592'
print str_verify('hello,5d41402abc4b2a76b9719d911017c591') # False
```

### Hashing with salts
Now, being able to hash a string into another string is nice,
however if the hashing algorithm used is figured out by someone else,
it would be insecure.

To improve the above algorithm, we now add a salt as a part of the
hashing process. Basically, a salt is a fixed length of randomly
generated string that is to be concatenated with the string that we
want to hash as a way to the output string even harder to decode.

Consider the following code
```python
import random
import string
import hashlib


def make_salt():
    # return a randomly generated string with length 5
    return ''.join(random.choice(string.letters) for x in range(5))


def make_pw_hash(name, pw, salt=None):
    # if salt is not given, then generate salt and use the generated
    # salt to create a hashed string
    if not salt:
        salt = make_salt()
    h = hashlib.sha256(name + pw + salt).hexdigest()
    return "%s,%s" % (h, salt)


def valid_pw(name, pw, h):
    try:
        salt = h.split(',')[1]
        return h == make_pw_hash(name, pw, salt)
    except IndexError:
        return False
```
