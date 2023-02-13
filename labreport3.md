# Researching Commands
We will be diving deep into the options of the `grep` command. 

## Recursion
Using the `-r` option will result in a recursive search, so `grep` will look through all subdirectories.

From the parent directory of `written_2` we can search all subdirectories for the string "meow" with `grep -r meow written_2`. This returns the following:
```
written_2/travel_guides/berlitz1/WhereToMallorca.txt:        English package tourists, retirees, and vacation homeowners.
written_2/travel_guides/berlitz2/Canada-WhereToGo.txt:Many of the sculptures you see were incorporated into the structure of a house as posts and crossbeams. One Kwakiutl giant accompanied by two slaves, emphasizing the homeowner’s power and prestige, originally supported a massive central roof beam. Others represent the tribes’ totemic animals, such as the bear, protecting a human being in his bosom. Prehistoric stone carvings show the continuity of totemic styles. Some smaller figures, in soft black argillite stone, were turned out by Haida craftsmen specifically for 19th-century European tourists who found themselves “caricatured” in the carvings.
```
Here, grep was able to reach into the `/travel_guides/berlitz1` and `/travel_guides/berlitz2` subdirectories to find the string "meow". It seems to only occur twice as part of the word "homeower". 

Let's try another example. In the same working directory, the command `grep -r interpretive written_2/`returns:
 ```
 written_2//non-fiction/OUP/Berk/ch2.txt:The communicative competence inherent in intersubjectivity blossoms within a zone of proximal development in which parents and other signiﬁcant adults are “stimulating, attentive, conﬁrmatory, interpretive, and highly supportive.”37 Parent–child intersubjectivity makes a vital contribution to the development of attachment, attention, language, and understanding of others’ perspectives. These capacities, in turn, ease the task of establishing an intersubjective connection, and that connection provides the platform for the creation of additional “zones,” enabling children to master complex, culturally adaptive skills. 
written_2//travel_guides/berlitz1/WhereToDublin.txt:        sample the brew. Plans are being made for an enlarged interpretive
written_2//travel_guides/berlitz2/Nepal-WhereToGo.txt:Along the park boundary and especially at Sauraha near park headquarters, dozens of lodges and inexpensive guest houses cater to budget-minded tourists. Elephant rides, jeep tours, and canoe trips can all be arranged at the park entrance, where an interesting interpretive center provides a history of the area and information about its ecology. One is reminded that in 1938, during a safari arranged for the British Viceroy of India, hundreds of elephants took part in a hunt that bagged 120 tigers, 38 rhinos, and 27 leopards. Today, hundreds of soldiers are stationed in the park to keep out poachers.
 ```
 As we can see, the recursive search can look into completely different branches of the file structure. There are entries from `written_2/non-fiction` and `written_2/travel_guides`.

## Counting words
By adding the `-c` option to `grep`, we can count the occurences of the desired word. 

## Case Sensitivity
Using the `-i` option will cause `grep` ignore whether a letter is upper or lower case when comparing stirngs.

## Inverted Results
Using the `-L` option will instead print out the files that don't contain the string. 
