# Researching Commands
We will be diving deep into the options of the `grep` command. For all examples, assume the working directory is the parent directory of `written_2` unless otherwise specified.

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
By adding the `-c` option to `grep`, we can count the occurences of the desired word in the desired file(s).
The command `grep -c the written_2/non-fiction/OUP/Berk/CH4.txt` outputs `189`, meaning there are 189 instances of the string "the" in the file. This is obviously much easier than counting all the instances.

How about searching multiple files? When using a pattern like in the command `grep -c trial written_2/non-fiction/OUP/Berk/*.txt`, we get:
```
written_2/non-fiction/OUP/Berk/CH4.txt:0
written_2/non-fiction/OUP/Berk/ch1.txt:4
written_2/non-fiction/OUP/Berk/ch2.txt:2
written_2/non-fiction/OUP/Berk/ch7.txt:0
```
Now, all the files are listed, including the ones without any instances of the word. No total count is formed. 

## Case Sensitivity
Using the `-i` option will cause `grep` ignore whether a letter is upper or lower case when comparing strings.
The word "Lucayans" is a proper noun and always capitalized, but we can find all instances of it with the following command `grep -i -r lucayans  written_2`. This returns:
```
written_2/travel_guides/berlitz2/Bahamas-History.txt:Centuries before the arrival of Columbus, a peaceful Amerindian people who called themselves the Luccucairi had settled in the Bahamas. Originally from South America, they had traveled up through the Caribbean islands, surviving by cultivating modest crops and from what they caught from sea and shore. Nothing in the experience of these gentle people could have prepared them for the arrival of the Pinta, the Niña, and the Santa Maria at San Salvador on 12 October 1492. Columbus believed that he had reached the East Indies and mistakenly called these people Indians. We know them today as the Lucayans. Columbus claimed the island and others in the Bahamas for his royal Spanish patrons, but not finding the gold and other riches he was seeking, he stayed for only two weeks before sailing towards Cuba.
written_2/travel_guides/berlitz2/Bahamas-History.txt:The Spaniards never bothered to settle in the Bahamas, but the number of shipwrecks attest that their galleons frequently passed through the archipelago en route to and from the Caribbean, Florida, Bermuda, and their home ports. On Eleuthera the explorers dug a fresh-water well — at a spot now known as “Spanish Wells” — which was used to replenish the supplies of water on their ships before they began the long journey back to Europe with their cargoes of South American gold. As for the Lucayans, within 25 years all of them, perhaps some 30,000 people, were removed from the Bahamas to work — and die — in Spanish gold mines and on farms and pearl fisheries on Hispaniola (Haiti), Cuba, and elsewhere in the Caribbean.
```
This would be most useful, if a word is only sometimes capitalized, so you can get all instances of it.

Returning to our search for "the", we may have missed times when "the" is at the beginning of the sentence and capitalized. Adding the `-i` option, the command looks like `grep -c -i the written_2/non-fiction/OUP/Berk/CH4.txt` and returns `193`. This is greater than the 189 we saw earlier, so adding the `-i` option got us some more results.

## Inverted Results
Using the `-L` option will instead print out the files that don't contain the string. 
Previously, we established that in `written_2/non-fiction/OUP/Berk`, `CH4.txt` and `ch7.txt` don't contain the string "trial". So in theory, `grep -L trial written_2/non-fiction/OUP/Berk/*.txt` should list those files. And it does. It returns:
```
written_2/non-fiction/OUP/Berk/CH4.txt
written_2/non-fiction/OUP/Berk/ch7.txt
```
This is a more concise listing of files that contain no instances of a given string than using the `-c` option.

As a final example, we will combine several modifiers in the command `grep -i -r -L are written_2`. This will recursively search the subdirectories of `written_2` for the string "are", ignoring capitalization, and will return a list of files that don't contain the string "are". The result is: 
```
written_2/travel_guides/berlitz1/WhatToFrance.txt
written_2/travel_guides/berlitz1/HandRIbiza.txt
```
Despite being such a common word, there are still two files that do not contain "are". With so many files inside of the subdirectories of `written_2`, it's much easier to work with a list like this than a list of all the files that contain "are".
