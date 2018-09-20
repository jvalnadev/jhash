# jhash
## Common Usage
First download the bundle. For common use, I recommend using the minified scripts, which have been processed by the YUI Compressor. Note that these only support utf-8 input and hex output. Use it like this:

```js
<script type="text/javascript" src="md5-min.js"></script>
<script type="text/javascript">
    hash = hex_md5("string");
    hmac = hex_hmac_md5("key", "data");
</script>
```
The usage for other hashes is essentially the same - sha1, sha256, sha512 or rmd160.

## Other Output Encodings
The scripts support base64 encoding, although you must use the full script, not the minified version. If necessary, you can create you own minified script, with the functionality you need. Use it like this:

```js
<script type="text/javascript" src="md5.js"></script>
<script type="text/javascript">
    hash = b64_md5("string");
    hmac = b64_hmac_md5("key", "data");
</script>
```

There is also a mode called "any output encoding". This lets you specify a string of characters, and all those characters will be used to encode the password. The string can be any length - it does not need to be a power of 2. This is useful for applications like password generation, when you want to get as much unpredictability as possible into a short password. Use it like this:

```js
<script type="text/javascript" src="md5.js"></script>
<script type="text/javascript">
    hash = any_md5("string", "encoding");
</script>
```
If the encoding is 0123456789ABCDEF the output will be identical to hex_md5. It isn't possible to create output that's identical to base64 encoding.

## Advanced Usage
If you want to use more advanced features, such as multiple repetitions of a hash, or utf-16 encoding, you need to use a slightly lower-level interface to the scripts. These have the concept of a "raw string"; this is a JavaScript string, but all the characters are between 0 and 255 - essentially a binary array. To get a hex hash, using utf-16 encoding:

```js
<script type="text/javascript" src="md5.js"></script>
<script type="text/javascript">
    hash = rstr2hex(rstr_md5(str2rstr_utf16le("string")));
</script>
```
You can also use str2rstr_utf16be. To perform a double hash:

```js
<script type="text/javascript" src="md5.js"></script>
<script type="text/javascript">
    hash = rstr2hex(rstr_md5(rstr_md5(str2rstr_utf8("string"))));
</script>
```
You can use variants of this to produce just about any hash you may need.

## Unit Tests
To run the unit tests, you will need Python 2.5 or newer. The script test.py generates an HTML file that runs the tests:

```sh
python test.py > test.html
```
Next, open test.html in a browser to run the tests, and see the results. If you want to test the minified versions of the scripts, use test-min.py.

## More info
http://pajhome.org.uk/crypt/md5/index.html
