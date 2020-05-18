**PW:** DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe

This level presents us with an input box where we are presumably meant to enter a secret code, which will then return the flag.
We are also given the "View sourcecode" link, which gives us some interesting insight into the functionality of the input form.

First we notice that a variable called *$encodedSecret*" is set to **3d3d516343746d4d6d6c315669563362**. We then notice a php function:

```
function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}
```

This function does multiple levels of encoding. A couple lines down we see the logic attached to the input box:

```
if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
    print "Access granted. The password for natas9 is <censored>";
    } else {
    print "Wrong secret";
    }
}
```
This tells us that the string we input will be encoded and compared against the string in the *$encodedSecret* variable.
With this being the case, the next logical step is to work backwards from the given encoded string.

To do this I found an online PHP sandbox and started reversing the calls in the **encodedSecret** funtion.

```
$rev1 = hex2bin("3d3d516343746d4d6d6c315669563362");
$rev2 = strrev($rev1);
$rev3 = base64_decode($rev2);
print $rev3;
````

This returns **oubWYf2kBq**. I use that output as the input and we are successful in receiving the flag.

**Flag:** W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl
