**PW:** 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9

We are presented a page with links to a "Home" and an "About" page.
Both of these links call on a php index page

**index.php?page=home** and **index.php?page=about** respectively.

The view sourcecode does give us something interesting however. We are given a hint in the form of a comment: 

"\<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 \-->"

If we simply replace the *'page=xxx'* portion of the link, we can navigate directly to the directory given to us in the hint.
Doing so gives us the flag for level 8. *http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8*

**Flag:** DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
