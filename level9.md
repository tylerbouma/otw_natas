**PW:** W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl

This level presents us with a search bar with a description of "Find words containing:".
Some quick messing around with this shows it is basically a dictionary lookup and viewing the source code confirms that we are grepping through a file called *dictionary.txt*.
```
passthru("grep -i $key dictionary.txt");
```
A quick scan through the ```dictionary.txt``` file produces nothing out of the normal - just a file with a bunch of words.

Nothing else in the source code points to a sort of question and answer type prompt that we have seen in the previous levels.

With nothing else standing out I do a bit of googling, and find that ```passthru()``` is notorious for exploitation.
I find that I can manually insert commands if the function is not properly sanitizing input - it's not.

I now remember back to the intro page of this CTF and recall that all passwords are stored in ```/etc/natas_webpass/```, and are accessible to both the level's user and the level's below it user (ex. natas8 and natas9).

I find that by entering ```; cat /etc/natas_webpass/natas10 # ``` I am able to first exit the grep (```;```) and then look into the ```/etc/natas_webpass/natas10``` file.
The ```#``` is only used to end the call without ```cat```ing out ```dictionary.txt```.

We are given the flag as the output.

**Flag:** nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu
