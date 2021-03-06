# Decoding functions

|#| Name | Description | Complexity |
|:---| :--- | :--- | :--- |
| 1 | [addressFromString(String): Address&#124;Unit](#address-from-string)| Decodes address from [base58](https://en.bitcoin.it/wiki/Base58Check_encoding) string | 124 for [Standard Library](/en/ride/script/standard-library) **version 3**<br>1 for Standard Library **version 4** |
| 2 | [addressFromStringValue(String): Address](#address-from-string-value) | Decodes address from base58 string.<br>Raises an exception if the address cannot be decoded | 124 for Standard Library **version 3**<br>1 for Standard Library **version 4** |
| 3 | [fromBase16String(String): ByteVector](#from-base-16-string) | Decodes [base16](https://en.wikipedia.org/wiki/Hexadecimal) string to an array of bytes | 10 |
| 4 | [fromBase58String(String): ByteVector](#from-base-58-string) | Decodes base58 string to an array of bytes | 10 for Standard Library **version 3**<br>1 for Standard Library **version 4** |
| 5 | [fromBase64String(String): ByteVector](#from-base-64-string)| Decodes [base64](https://en.wikipedia.org/wiki/Base64) string to an array of bytes | 10 for Standard Library **version 3**<br>40 for Standard Library **version 4** |

### addressFromString(String): Address|Unit<a id="address-from-string"></a>

Decodes address from [base58](https://en.bitcoin.it/wiki/Base58Check_encoding) string.

```
addressFromString(string: String): Address|Unit
```

### Parameters

#### `string`: [String](/en/ride/data-types/string)

The string to decode.

### Examples

```ride
let address = addressFromString("3NADPfTVhGvVvvRZuqQjhSU4trVqYHwnqjF")
```

## addressFromStringValue(String): Address <a id="address-from-string-value"></a>

Decodes address from [base58](https://en.bitcoin.it/wiki/Base58Check_encoding) string.

Raises an exception if the address cannot be decoded.

```
addressFromStringValue(string: String): Address
```

### Parameters

#### `string`: [String](/en/ride/data-types/string)

The string to decode.

### Examples

```ride
let address = addressFromStringValue("3NADPfTVhGvVvvRZuqQjhSU4trVqYHwnqjF")
```

## fromBase16String(String): ByteVector<a id="from-base-16-string"></a>

Decodes a [base16](https://en.wikipedia.org/wiki/Hexadecimal) string to an array of bytes.

```
fromBase16String(str: String): ByteVector
```

### Parameters

#### `str`: [String](/en/ride/data-types/string)

The string to decode.

### Examples

```ride
let bytes = fromBase16String("52696465")
```

## fromBase58String(String): ByteVector<a id="from-base-58-string"></a>

Decodes a [base58](https://en.bitcoin.it/wiki/Base58Check_encoding) string to an array of bytes.

```
fromBase58String(str: String): ByteVector
```

### Parameters

#### `str`: [String](/en/ride/data-types/string)

The string to decode.

### Examples

```ride
let bytes = fromBase58String("37BPKA")
```

## fromBase64String(String): ByteVector<a id="from-base-64-string"></a>

Decodes a [base64](https://en.wikipedia.org/wiki/Base64) string to an array of bytes.

```
fromBase64String(str: String): ByteVector
```

### Parameters

#### `str`: [String](/en/ride/data-types/string)

The string to decode.

### Examples

```ride
let bytes = fromBase64String("UmlkZQ==")
```
