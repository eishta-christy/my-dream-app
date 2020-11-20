---
title: Preprocessing of linguistic data for machine learning
description: Why do we need preprocessing.
published: true
---

# Preprocessing of linguistic data for machine learning
![banner](https://source.unsplash.com/970x150 "Linguistic Intelligence")

Let's say we see a text: 
> "Bei Split-Brain-Patienten wird die zentrale Verbindung zwischen den Gehirnhälften, der Balken, durchtrennt. So dramatisch die Durchtrennung der Verbindung zwischen den beiden Gehirnhälften für den einzelnen Patienten ist: Die Neurowissenschaftler haben durch diese Operation enorm viel über das menschliche *Gehirn* erfahren. Die Hälften des *Gehirns* repräsentierten bald zwei isolierte Egos. Obwohl die Sache so einfach nie dargestellt wurde, treiben einige Vorurteile und populärwissenschaftliche Ansichten darüber immer noch ihr Unwesen." 

And have a goal to somehow get to know how the words are organized in the sentences, which of them tend to stay in the same contextes and which of the don't.
> "You shall know a word by the company it keeps." [1] 

One can do whatever he/she wants with this information. Get to know what and how should a chatbot answer to a particular question, which sentence in a film review counts for a positive or a negative opinion, or what is a structure of an assult for example. But what connects all this problems is that in the beginning we most of the time have so-called row-data. Row data only sounds like a dirty word, but actually it is precious. It has linguistic data as it is: alive, diverse, unrestricted. And isn't it exactly what one want to learn? Any application made based on natural language is there for humans and should not be limited. Nevertheless, to find the structure in the data one should take care of some formalities.

## Find the words

So first of all we should get to know where teh words are. If we imagine that we do not know the language of the text, we will feel like a computer: we'll see a bunch of unfamiliar carachters and wouldn't have a chance to say where a word ends and where it begins. But we are humans and probably even know German. Then we can say that words are the strings which are separated with spaces or puctuation. So now we our text in this format:
[Bei, Split, -, Brain, -, Patienten, wird, die, zentrale, Verbindung, zwischen, den, Gehirnhälften, ,, der, Balken,, durchtrennt, ., So, dramatisch, die, Durchtrennung, der, Verbindung, zwischen, den, beiden, Gehirnhälften, für, den, einzelnen, Patienten, ist, :, Die, Neurowissenschaftler, haben, durch, diese, Operation, enorm, viel, über, das, menschliche, *Gehirn*, erfahren , ., Die, Hälften, des, *Gehirns*, repräsentierten, bald, zwei, isolierte, Egos., Obwohl, die, Sache, so, einfach, nie, dargestellt, wurde, , treiben, einige, Vorurteile, und, populärwissenschaftliche, Ansichten, darüber, immer, noch, ihr, Unwesen.]
This could be easier if we divide a text into sentences at first, but that's a matter of taste. What is also the matter of taste **and** your analysis goal ist what to do with words like *Split-Brain-Patienten*, how to analyse those if they are actually divided by punctuation? And what to do with punctuation? Are those words too? 

And the imagine we have a word written like this *Split Brain Patienten*, is there no way we see it as one word?

## Find unique words

When we solved these problems for our particular case. let's look particularly at one word: *Gehirn*. We see it in the paragraph above twice. If we are about to take the words as they are we will look at the context (embeddigns) of these two mentions separately. But actually it is one word in the vocabularly, and their forms differ just because of grammatical rules in the language. So one of the important steps in preprocessing is lemmatisation. 

### Lemmatization

> Lemmatize - to group together the inflected forms of (a word) for analysis as a single item. [2]

What we have after this step should look approximately like this:
[Bei, Split, -, Brain, -, Patient, sein, die, zentral, Verbindung, zwischen, der, Gehirnhälfte, ,, der, Balke,, durchtrennen, ., So, dramatisch, der, Durchtrennung, der, Verbindung, zwischen, der, beide, Gehirnhälfte, für, der, einzeln, Patient, ist, :, Der, Neurowissenschaftler, haben, durch, diese, Operation, enorm, viel, über, das, menschlich, *Gehirn*, erfahren , ., Der, Hälfte, der, *Gehirn*, repräsentierten, bald, zwei, isolieren, Ego., Obwohl, der, Sache, so, einfach, nie, darstellen, sein, , treiben, einige, Vorurteil, und, populärwissenschaftlich, Ansicht, darüber, immer, noch, sein, Unwesen.]
How exactly it looks depends on 2 things: the lemmatizer: does it know all the words? Can it correctly recornize Part-of-Speech of any word? And the quality of the text: does it have typos or strange formatting (*GeHirN*) disabling a lemmatizer to do his job? I also hope at this point you yourself start asking questions like that.

### Lower-case method

So now we brought the words to there common forms. But "Der" und "der" will still be seen as different words when a computer sees them: 01000100 01100101 01110010 vs. 01100100 01100101 01110010. So most always one goes one step further and modifies all the words (also known as tokens) to lower case. So it'll look like this:
[bei, split, -, brain, -, patient, sein, die, zentral, Verbindung, zwischen, der, gehirnhälfte, ,, der, balke,, durchtrennen, ., So, dramatisch, der, durchtrennung, der, Verbindung, zwischen, der, beide, Gehirnhälfte, für, der, einzeln, Patient, ist, :, der, Neurowissenschaftler, haben, durch, diese, Operation, enorm, viel, über, das, menschlich, *gehirn*, erfahren , ., der, Hälfte, der, *gehirn*, repräsentierten, bald, zwei, isolieren, ego., obwohl, der, sache, so, einfach, nie, darstellen, sein, , treiben, einige, vorurteil, und, populärwissenschaftlich, ansicht, darüber, immer, noch, sein, unwesen.]


## Almost there

It seems that we are ready to move on and analyse text data! :)
But is it so?

Here is just a couple of questions for you to think about:

- What should one do with numbers? 1 is definetely not 2, but does it matter in a text? Sould numbers be removed or replaced?
- Some special characters, what to do with them? Should we remove smilies? What else can or should be removed?
- *Wissen* (NOUN) und *wissen* (VERB) would have different contexts in real life, but what happens when we lowercase them? So maybe e shouldn't?

There are no unique answers to these and many more questions. Each of them is answered depending on the situation of analysis: language, analysis goal, resources. And of course do not forget teh questions we've already asked throught this post. Decisions at this step would affect everything that follows. To relieve the dramatism, here's a picture that sums it up:


___
![alt text](https://scotsirishpadreblog.files.wordpress.com/2017/02/gigo.jpg?w=300&h=300&zoom=2) 

[1] Firth, John R. 1957. A synopsis of linguistic theory 1930–1955. In Studies in linguistic analysis, 1–32. Oxford:
Blackwell.

[2] https://www.collinsdictionary.com/dictionary/english/lemmatize

