**PW:** nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu

This level is essentially the same as the last except that some characters are filtered.
We can see that indeed
```
if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
}
```
This means we can't use a semi-colon to exit the ```grep``` prematurely like we did in the last level.

However, we can still use regex wildcards to grab data from files outside of ```dictionary.txt```.
```
. /etc/natas_webpass/natas11 #
```

This essentially tells grep to look for anything with a valid first character in ```/etc/natas_webpass/natas11```.
We then use ```#``` again to exclude the other files (dictionary.txt) in the grep command.

**Flag:** U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
