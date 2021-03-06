Test vectors
============

Testing the correctness of the primitives implemented in each ``cryptography``
backend requires trusted test vectors. Where possible these vectors are
obtained from official sources such as `NIST`_ or `IETF`_ RFCs. When this is
not possible ``cryptography`` has chosen to create a set of custom vectors
using an official vector file as input to verify consistency between
implemented backends.

Vectors are kept in the `cryptography_vectors` package rather than within our
main test suite.

Sources
-------

Asymmetric ciphers
~~~~~~~~~~~~~~~~~~

* RSA PKCS #1 from the RSA FTP site (ftp://ftp.rsasecurity.com/pub/pkcs/pkcs-1/
  and ftp://ftp.rsa.com/pub/rsalabs/tmp/).
* RSA FIPS 186-2 and PKCS1 v1.5 vulnerability test vectors from `NIST CAVP`_.
* FIPS 186-2 and FIPS 186-3 DSA test vectors from `NIST CAVP`_.
* FIPS 186-2 and FIPS 186-3 ECDSA test vectors from `NIST CAVP`_.
* DH and ECDH test vectors from `NIST CAVP`_.
* Ed25519 test vectors from the `Ed25519 website_`.
* OpenSSL PEM RSA serialization vectors from the `OpenSSL example key`_ and
  `GnuTLS key parsing tests`_.
* OpenSSL PEM DSA serialization vectors from the `GnuTLS example keys`_.
* PKCS #8 PEM serialization vectors from

  * GnuTLS: `enc-rsa-pkcs8.pem`_, `enc2-rsa-pkcs8.pem`_,
    `unenc-rsa-pkcs8.pem`_, `pkcs12_s2k_pem.c`_. The contents of
    `enc2-rsa-pkcs8.pem`_ was re-encrypted using a stronger PKCS#8 cipher.
  * `Botan's ECC private keys`_.

Custom Asymmetric Vectors
~~~~~~~~~~~~~~~~~~~~~~~~~

* ``asymmetric/PEM_Serialization/ec_private_key.pem`` and
  ``asymmetric/DER_Serialization/ec_private_key.der`` - Contains an Elliptic
  Curve key generated by OpenSSL from the curve ``secp256r1``.
* ``asymmetric/PEM_Serialization/ec_private_key_encrypted.pem`` and
  ``asymmetric/DER_Serialization/ec_private_key_encrypted.der``- Contains the
  same Elliptic Curve key as ``ec_private_key.pem``, except that it is
  encrypted with AES-128 with the password "123456".
* ``asymmetric/PEM_Serialization/ec_public_key.pem`` and
  ``asymmetric/DER_Serialization/ec_public_key.der``- Contains the public key
  corresponding to ``ec_private_key.pem``, generated using OpenSSL.
* ``asymmetric/PEM_Serialization/rsa_private_key.pem`` - Contains an RSA 2048
  bit key generated using OpenSSL, protected by the secret "123456" with DES3
  encryption.
* ``asymmetric/PEM_Serialization/rsa_public_key.pem`` and
  ``asymmetric/DER_Serialization/rsa_public_key.der``- Contains an RSA 2048
  bit public generated using OpenSSL from ``rsa_private_key.pem``.
* ``asymmetric/PEM_Serialization/dsaparam.pem`` - Contains 2048-bit DSA
  parameters generated using OpenSSL; contains no keys.
* ``asymmetric/PEM_Serialization/dsa_private_key.pem`` - Contains a DSA 2048
  bit key generated using OpenSSL from the parameters in ``dsaparam.pem``,
  protected by the secret "123456" with DES3 encryption.
* ``asymmetric/PEM_Serialization/dsa_public_key.pem`` and
  ``asymmetric/DER_Serialization/dsa_public_key.der`` - Contains a DSA 2048 bit
  key generated using OpenSSL from ``dsa_private_key.pem``.
* ``asymmetric/PKCS8/unenc-dsa-pkcs8.pem`` and
  ``asymmetric/DER_Serialization/unenc-dsa-pkcs8.der`` - Contains a DSA 1024
  bit key generated using OpenSSL.
* ``asymmetric/PKCS8/unenc-dsa-pkcs8.pub.pem`` and
  ``asymmetric/DER_Serialization/unenc-dsa-pkcs8.pub.der`` - Contains a DSA
  2048 bit public key generated using OpenSSL from ``unenc-dsa-pkcs8.pem``.
* DER conversions of the `GnuTLS example keys`_ for DSA as well as the
  `OpenSSL example key`_ for RSA.
* DER conversions of `enc-rsa-pkcs8.pem`_, `enc2-rsa-pkcs8.pem`_, and
  `unenc-rsa-pkcs8.pem`_.


X.509
~~~~~

* PKITS test suite from `NIST PKI Testing`_.
* ``v1_cert.pem`` from the OpenSSL source tree (`testx509.pem`_).
* ``ecdsa_root.pem`` - `DigiCert Global Root G3`_, a ``secp384r1`` ECDSA root
  certificate.

Custom X.509 Vectors
~~~~~~~~~~~~~~~~~~~~

* ``invalid_version.pem`` - Contains an RSA 2048 bit certificate with the
  X.509 version field set to ``0x7``.
* ``post2000utctime.pem`` - Contains an RSA 2048 bit certificate with the
  ``notBefore`` and ``notAfter`` fields encoded as post-2000 ``UTCTime``.
* ``dsa_selfsigned_ca.pem`` - Contains a DSA self-signed CA certificate
  generated using OpenSSL.
* ``ec_no_named_curve.pem`` - Contains an ECDSA certificate that does not have
  an embedded OID defining the curve.
* ``all_supported_names.pem`` - An RSA 2048 bit certificate generated using
  OpenSSL that contains a subject and issuer that have two of each supported
  attribute type from :rfc:`5280`.
* ``unsupported_subject_name.pem`` - An RSA 2048 bit self-signed CA certificate
  generated using OpenSSL that contains the unsupported "initials" name.
* ``utf8_common_name.pem`` - An RSA 2048 bit self-signed CA certificate
  generated using OpenSSL that contains a UTF8String common name with the value
  "We heart UTF8!™".

Hashes
~~~~~~

* MD5 from :rfc:`1321`.
* RIPEMD160 from the `RIPEMD website`_.
* SHA1 from `NIST CAVP`_.
* SHA2 (224, 256, 384, 512) from `NIST CAVP`_.
* Whirlpool from the `Whirlpool website`_.

HMAC
~~~~

* HMAC-MD5 from :rfc:`2202`.
* HMAC-SHA1 from :rfc:`2202`.
* HMAC-RIPEMD160 from :rfc:`2286`.
* HMAC-SHA2 (224, 256, 384, 512) from :rfc:`4231`.

Key derivation functions
~~~~~~~~~~~~~~~~~~~~~~~~

* HKDF (SHA1, SHA256) from :rfc:`5869`.
* PBKDF2 (HMAC-SHA1) from :rfc:`6070`.
* scrypt from the `draft RFC`_.

Recipes
~~~~~~~

* Fernet from its `specification repository`_.

Symmetric ciphers
~~~~~~~~~~~~~~~~~

* AES (CBC, CFB, ECB, GCM, OFB) from `NIST CAVP`_.
* AES CTR from :rfc:`3686`.
* 3DES (CBC, CFB, ECB, OFB) from `NIST CAVP`_.
* ARC4 from :rfc:`6229`.
* Blowfish (CBC, CFB, ECB, OFB) from `Bruce Schneier's vectors`_.
* Camellia (ECB) from NTT's `Camellia page`_ as linked by `CRYPTREC`_.
* Camellia (CBC, CFB, OFB) from `OpenSSL's test vectors`_.
* CAST5 (ECB) from :rfc:`2144`.
* CAST5 (CBC, CFB, OFB) generated by this project.
  See: :doc:`/development/custom-vectors/cast5`
* IDEA (ECB) from the `NESSIE IDEA vectors`_ created by `NESSIE`_.
* IDEA (CBC, CFB, OFB) generated by this project.
  See: :doc:`/development/custom-vectors/idea`
* SEED (ECB) from :rfc:`4269`.
* SEED (CBC) from :rfc:`4196`.
* SEED (CFB, OFB) generated by this project.
  See: :doc:`/development/custom-vectors/seed`

Two factor authentication
~~~~~~~~~~~~~~~~~~~~~~~~~

* HOTP from :rfc:`4226`
* TOTP from :rfc:`6238` (Note that an `errata`_ for the test vectors in RFC
  6238 exists)

CMAC
~~~~

* AES-128, AES-192, AES-256, 3DES from `NIST SP-800-38B`_

Creating test vectors
---------------------

When official vectors are unavailable ``cryptography`` may choose to build
its own using existing vectors as source material.

Custom Symmetric Vectors
~~~~~~~~~~~~~~~~~~~~~~~~

.. toctree::
    :maxdepth: 1

    custom-vectors/cast5
    custom-vectors/idea
    custom-vectors/seed

If official test vectors appear in the future the custom generated vectors
should be discarded.

Any vectors generated by this method must also be prefixed with the following
header format (substituting the correct information):

.. code-block:: python

    # CAST5 CBC vectors built for https://github.com/pyca/cryptography
    # Derived from the AESVS MMT test data for CBC
    # Verified against the CommonCrypto and Go crypto packages
    # Key Length : 128

.. _`NIST`: http://www.nist.gov/
.. _`IETF`: https://www.ietf.org/
.. _`NIST CAVP`: http://csrc.nist.gov/groups/STM/cavp/
.. _`Bruce Schneier's vectors`: https://www.schneier.com/code/vectors.txt
.. _`Camellia page`: http://info.isl.ntt.co.jp/crypt/eng/camellia/
.. _`CRYPTREC`: http://www.cryptrec.go.jp
.. _`OpenSSL's test vectors`: https://github.com/openssl/openssl/blob/97cf1f6c2854a3a955fd7dd3a1f113deba00c9ef/crypto/evp/evptests.txt#L232
.. _`RIPEMD website`: http://homes.esat.kuleuven.be/~bosselae/ripemd160.html
.. _`Whirlpool website`: http://www.larc.usp.br/~pbarreto/WhirlpoolPage.html
.. _`draft RFC`: https://tools.ietf.org/html/draft-josefsson-scrypt-kdf-01
.. _`Specification repository`: https://github.com/fernet/spec
.. _`errata`: http://www.rfc-editor.org/errata_search.php?rfc=6238
.. _`OpenSSL example key`: http://git.openssl.org/gitweb/?p=openssl.git;a=blob;f=test/testrsa.pem;h=aad21067a8f7cb93a52a511eb9162fd83be39135;hb=66e8211c0b1347970096e04b18aa52567c325200
.. _`GnuTLS key parsing tests`: https://gitorious.org/gnutls/gnutls/commit/f16ef39ef0303b02d7fa590a37820440c466ce8d
.. _`enc-rsa-pkcs8.pem`: https://gitorious.org/gnutls/gnutls/source/f8d943b38bf74eaaa11d396112daf43cb8aa82ae:tests/pkcs8-decode/encpkcs8.pem
.. _`enc2-rsa-pkcs8.pem`: https://gitorious.org/gnutls/gnutls/source/f8d943b38bf74eaaa11d396112daf43cb8aa82ae:tests/pkcs8-decode/enc2pkcs8.pem
.. _`unenc-rsa-pkcs8.pem`: https://gitorious.org/gnutls/gnutls/source/f8d943b38bf74eaaa11d396112daf43cb8aa82ae:tests/pkcs8-decode/unencpkcs8.pem
.. _`pkcs12_s2k_pem.c`: https://gitorious.org/gnutls/gnutls/source/f8d943b38bf74eaaa11d396112daf43cb8aa82ae:tests/pkcs12_s2k_pem.c
.. _`Botan's ECC private keys`: https://github.com/randombit/botan/tree/4917f26a2b154e841cd27c1bcecdd41d2bdeb6ce/src/tests/data/ecc
.. _`GnuTLS example keys`: https://gitorious.org/gnutls/gnutls/commit/ad2061deafdd7db78fd405f9d143b0a7c579da7b
.. _`NESSIE IDEA vectors`: https://www.cosic.esat.kuleuven.be/nessie/testvectors/bc/idea/Idea-128-64.verified.test-vectors
.. _`NESSIE`: https://en.wikipedia.org/wiki/NESSIE
.. _`Ed25519 website`: http://ed25519.cr.yp.to/software.html
.. _`NIST SP-800-38B`: http://csrc.nist.gov/publications/nistpubs/800-38B/Updated_CMAC_Examples.pdf
.. _`NIST PKI Testing`: http://csrc.nist.gov/groups/ST/crypto_apps_infra/pki/pkitesting.html
.. _`testx509.pem`: https://github.com/openssl/openssl/blob/master/test/testx509.pem
.. _`DigiCert Global Root G3`: http://cacerts.digicert.com/DigiCertGlobalRootG3.crt
