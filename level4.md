**PW:** Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ

This level "disallows" us by stating that we need to access the page via http://natas5.natas.labs.overthewire.org/.
We don't have access to that level yet, but we notice there is a *Refresh page* link that essentially refreshes the page, but pulls in the current page's HTTP data.

After reading up a bit on HTTP headers, I figure we may be able to intercept the request and insert our own headers; fooling the page into thinking we came from http://natas5.natas.labs.overthewire.org/.
I used a plugin called "Tamper Data" for Firefox, but any plugin that allows HTTP header manipulation will work.

We edit the "Requester" item and refresh the page, giving us the flag.

**Flag:** iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq
