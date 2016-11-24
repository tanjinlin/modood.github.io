# crypto

```
crypto.constants
crypto.DEFAULT_ENCODING
crypto.fips

crypto.timingSafeEqual(a, b)
crypto.randomBytes(size[, callback])
crypto.setEngine(engine[, flags])
```

*   Encrypt and Decrypt

    ```
    crypto.privateEncrypt(private_key, buffer)
    crypto.privateDecrypt(private_key, buffer)

    crypto.publicEncrypt(public_key, buffer)
    crypto.publicDecrypt(public_key, buffer)
    ```

*   pdkdf2

    ```
    crypto.pbkdf2(password, salt, iterations, keylen, digest, callback)
    crypto.pbkdf2Sync(password, salt, iterations, keylen, digest)
    ```

*   Certificate

    ```
    crypto.Certificate()
    new crypto.Certificate()

    certificate.exportChallenge(spkac)
    certificate.exportPublicKey(spkac)
    certificate.verifySpkac(spkac)
    ```

*   Cipher and Decipher

    ```
    crypto.getCiphers()

    crypto.createCipher(algorithm, password)
    crypto.createCipheriv(algorithm, key, iv)

    cipher.setAAD(buffer)
    cipher.getAuthTag()
    cipher.setAutoPadding(auto_padding=true)
    cipher.update(data[, input_encoding][, output_encoding])
    cipher.final([output_encoding])
    ```
    ```
    crypto.createDecipher(algorithm, password)
    crypto.createDecipheriv(algorithm, key, iv)

    decipher.setAAD(buffer)
    decipher.setAuthTag(buffer)
    decipher.setAutoPadding(auto_padding=true)
    decipher.update(data[, input_encoding][, output_encoding])
    decipher.final([output_encoding])
    ```

*   DiffieHellman and ECDH(Elliptic Curve Diffie-Hellman)

    ```
    crypto.getDiffieHellman(group_name)
    crypto.createDiffieHellman(prime_length[, generator])
    crypto.createDiffieHellman(prime[, prime_encoding][, generator][, generator_encoding])

    diffieHellman.computeSecret(other_public_key[, input_encoding][, output_encoding])
    diffieHellman.generateKeys([encoding])
    diffieHellman.getGenerator([encoding])
    diffieHellman.getPrime([encoding])

    diffieHellman.getPrivateKey([encoding])
    diffieHellman.setPrivateKey(private_key[, encoding])
    diffieHellman.getPublicKey([encoding])
    diffieHellman.setPublicKey(public_key[, encoding])

    diffieHellman.verifyError
    ```
    ```
    crypto.getCurves()

    crypto.createECDH(curve_name)

    ecdh.computeSecret(other_public_key[, input_encoding][, output_encoding])
    ecdh.generateKeys([encoding[, format]])

    ecdh.getPublicKey([encoding[, format]])
    ecdh.setPublicKey(public_key[, encoding])
    ecdh.getPrivateKey([encoding])
    ecdh.setPrivateKey(private_key[, encoding])
    ```

*   Hash and Hmac

    ```
    crypto.getHashes()

    crypto.createHash(algorithm)

    hash.update(data[, input_encoding])
    hash.digest([encoding])
    ```
    ```
    crypto.createHmac(algorithm, key)

    hmac.update(data[, input_encoding])
    hmac.digest([encoding])
    ```

*   Sign and Verify

    ```
    crypto.createSign(algorithm)

    sign.sign(private_key[, output_format])
    sign.update(data[, input_encoding])
    ```
    ```
    crypto.createVerify(algorithm)

    verifier.update(data[, input_encoding])
    verifier.verify(object, signature[, signature_format])
    ```

