**PW:** U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK

This level is a bit different in that the source code is more complex.
We are presented with code that sets and ciphers two array items - ```bgcolor``` and ```showpassword```.

After a bit of poking around I found that ```bgcolor``` isn't too useful and to focus on ```showpassword```.
The goal appears to be to set ```showpassword``` from "no" to "yes".
Although this is a cookie value, we are unable to directly set it as the data is in an xor cipher.

One thing that xor ciphers are vulnerable to are known-plaintext attacks.
Since I know what the default values are and I know what the ending cipher is, I can work back from there to create a cipher that would have ```showpassword``` set to "yes"
To do that, I create a PHP file and use the following code:

```
$ciph = "ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw=";  
  
function xor_encrypt($in) {  
    $key = json_encode(array( "showpassword"=>"no", "bgcolor"=>"#ffffff"));  
    $text = $in;  
    $outText = '';  
  
    // Iterate through each character  
    for($i=0;$i<strlen($text);$i++) {  
    $outText .= $text[$i] ^ $key[$i % strlen($key)];  
    }  
  
    return $outText;  
}  
  
echo xor_encrypt(base64_decode($ciph));
```
Returning

```
qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq
```

I can now use that cipher in the original code and then change ```showpassword``` to "yes"

```
$d = array( "showpassword"=>"yes", "bgcolor"=>"#ffffff");
function xor_encrypt($in) {
    $key = 'qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq';
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}

echo base64_encode(xor_encrypt(json_encode($d)));
```

This now returns the new cookie we need to set. After doing that in Chrome and refreshing the page, we are given the flag.

**Flag:** EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3
