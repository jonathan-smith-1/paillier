Pure Python Paillier Homomorphic Cryptosystem
=============================================

This is a fork of [mikeivanov][1]'s pure Python implementation of the 
[Paillier Homomorphic Cryptosystem][2], modified to run on Python3.

Homomorphic Cryptosystems
-------------------------

The idea of homomorphic computation is to encrypt some numbers into 
*cyphertexts*, perform algebraic operations like "add" and "multiply" on
the cyphertexts, and then decrypt the result.  The result is exactly the
same as if corresponding "+" and "*" operations were applied to the
original numbers.

In other words, a homomorphic cryptosystem enables cryptographically
secure computations in an untrusted environment.

This is important because it allows models to be trained on *encrypted* data 
(e.g. preserving patient privacy in healthcare applications).

Paillier cryptosystem
---------------------

The Paillier cryptosystem is a probabilistic asymmetric algorithm for
public key cryptography. It is known as partially
homomorphic as it can only add encrypted numbers or multiply an
encrypted number by an unencrypted multiplier.

Implementation
--------------

This pure Python implementation exploits the `int` type in Python 3 with
its arbitrary precision arithmetic. The generated public key is serializable, 
so it can be pickled along with the encrypted numbers and sent to a
remote server for computation.

According to [mikeivanov][1]'s repository, the code is loosely based on 
[Thep][3] and a few ActiveState recipes.

Please note that this implementation's primary purpose is education;
it is **not suitable for production use** as it is.

Installation and Tests
----------------------

The paillier.py module has no external dependencies besides the included
primes.py. Simply run demo.py to see it in action.

    $ git clone https://github.com/jonathan-smith-1/paillier
    $ cd paillier
    $ pip install .
    $ python demo.py
    ...............
    Generating keypair...
    x = 3
    Encrypting x...
    cx = 14788818202106802157979663709685399775685304772689176951138395154...
    y = 5
    Encrypting y...
    cy = 15845129408592377991051835070770332917255019576438102739007785409...
    Computing cx + cy...
    cz = 35054170028941356642770510397991701544909261570444245993603636388...
    Decrypting cz...
    z = 8
    Computing decrypt((cz + 2) * 3) ...
    result = 30

To run unit tests please install [Nose][4]:

    $ pip install -r requirements_dev.txt
    $ nosetests
    ...............
    Ran 816 tests in 7.715s
    OK

Usage
-----

    $ python
    Python 3.6.5 (v3.6.5:f59c0932b4, Mar 28 2018, 03:03:55) 
    Type "help", "copyright", "credits" or "license" for more information.
    
    >>> from paillier.paillier import *

    >>> priv, pub = generate_keypair(128)

    >>> x = encrypt(pub, 2)

    >>> y = encrypt(pub, 3)

    >>> x, y
    (58270969461107207535519595770..., 84176641665375048505734864...)

    >>> z = e_add(pub, x, y)

    >>> z
    543656852031605188344427268...

    >>> decrypt(priv, pub, z)
    5


License and Copyright
---------------------
LGPL v3, see [LICENSE][5]

(C) 2011 Mike Ivanov


[1]: https://github.com/mikeivanov/paillier
[2]: https://en.wikipedia.org/wiki/Paillier_cryptosystem
[3]: http://code.google.com/p/thep/
[4]: http://readthedocs.org/docs/nose/en/latest/index.html
[5]: https://github.com/mikeivanov/paillier/blob/master/LICENSE

