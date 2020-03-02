**PW:** aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1

We are given a text box where we input a "secret", and depending on whether or not the secret is correct, we will be given the flag.

We are also given a "*View sourcecode*" link which give us some insight into how this query process works.

```
<?

include "includes/secret.inc";

    if(array_key_exists("submit", $_POST)) {
        if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
    }
?>
```

The interesting part here is the `include "includs/secret.inc"`. We can navigate to that subpage and inspect it. We find a comment called "secret"... convienent.
We copy the secret: FOEIUWGHFEEUHOFUOIU into the text box and query, giving us the flag.

**Flag:** 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9
