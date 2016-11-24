# assert

*   true or false

    ```
    assert(value[, message])
    assert.ok(value[, message])

    assert.ifError(value)
    ```

*   expect

    ```
    assert.fail(actual, expected, message, operator)
    ```

*   equal or not

    ```
    assert.equal(actual, expected[, message])
    assert.strictEqual(actual, expected[, message])
    assert.deepEqual(actual, expected[, message])
    assert.deepStrictEqual(actual, expected[, message])

    assert.notEqual(actual, expected[, message])
    assert.notStrictEqual(actual, expected[, message])
    assert.notDeepEqual(actual, expected[, message])
    assert.notDeepStrictEqual(actual, expected[, message])
    ```

*   throw or not

    ```
    assert.throws(block[, error][, message])
    assert.doesNotThrow(block[, error][, message])
    ```
