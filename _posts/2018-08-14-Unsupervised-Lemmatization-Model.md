---
title: "Unsupervised Lemmatization Model"
layout: post
date: 2018-08-14 11:59
tag: Corpus Linguistics
tag: Google
teaching: false
blog: true
research: true
draft: false
author: James Gawley
summary: "A Model for Disambiguating between Possible Lemmata Using Unsupervised Lemma Frequency Counts"
 
---
<em>[The code for this unsupervised lemmatization model can be found here.](https://github.com/jamesgawley/cltk/blob/master/cltk/lemmatize/latin/unsupervised.py)</em>

## How frequent is each word in a language?

This is a basic question in language modeling. To answer it, we need to group together all the strings in our corpus that belong to the same word. This is called lemmatization. The difficult thing about lemmatization is that sometimes it isn't obvious which lemma, or dictionary-entry, a word in our text stems from. This is especially true in inflected languages like Latin and Ancient Greek.



One approach to solving this problem, implemented by Patrick Burns in his 2016 Google Summer of Code project for CLTK, involves supervised training data. 'Supervised training data,' in this case, means a lot of texts whose lemmatizations have been solved by hand. Various machine learning techniques can pick up patterns in the trainin data, and then the computer can look for those patterns in fresh, unlemmatized texts. The presence of such patterns helps the computer make an educated guess in ambiguous cases. But what happens when we want to know the frequency of words, but we don't have a training data set? This is the situation in ancient languages other than Greek and Latin, and it also comes up when one wants to scrutinize a sub-set of Latin, for example Flavian poets, without relying on models trained on texts that were written centuries apart.

To build an unsupervised model of word frequency, I grouped together all the tokens in the text that might have come from the same lemma. Whenever a word <em>could</em> stem from a particular lemma, I count that lemma as 'seen' in the text.

```xml
<myxml>
<mxfile userAgent="Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36" version="9.0.5" editor="www.draw.io" type="device"><diagram id="ce38d9e4-6dba-9bcd-ecb4-3782d756e4bb" name="Page-1">7Vtbd6o4FP41rp7z4uIiiI+t7VweptN1ejqXxxSiZgrEE+Kl8+tnh4sCCYIUUbumDxU2YSf5vs2+oQNzGmx/Zmi5+I162B8YmrcdmPcDw9D1iQMfQvKeSMaanQjmjHjpoL3gmfyLU6GWSlfEw1FhIKfU52RZFLo0DLHLCzLEGN0Uh82oX5x1ieZYEjy7yJelfxKPLxKpY2l7+S+YzBfZzLqWXnlF7tuc0VWYzjcwzFn8l1wOUKYrHR8tkEc3OZH5MDCnjFKeHAXbKfYFthlsyX0/VVzdrZvhkDe5wU55WSN/hbMlxwvj7xkYmwXh+HmJXHG+AcIH5t2CBz6c6XCIomVCwYxsMai9SzVixvG2cln6brNgRJgGmLN3GLIt2kFqPmYG72ZPhu6kskWeiEyIUgOY71TvQYCDFIcKEK16TGKKxW7vNdhxDUJdAGIWEdEnCkQMBSJ2B4A0sJG+8SjBoUJjpEBj1AEasnXcsgAJCWGr4AcIwS+hkEoYwW55EYiIM/qGp9SnDCQhDWHk3Yz4fkmEfDIP4dQFdDDI7wR2BNzVbXohIJ4nplEiX+TmBOBbzcA3OwB/XG+KOPRuRQjYwyeZHvYk91+799zuLMXmMhnDPuJkXVSv2nE6wxMlMPEO2pFTfMyNEmYRXTEXpzfl/XpJz1g7rIcjNsdc0hPDv9t0I0acoxhxfRRFxL0uUuwaMJuSUtYzORkpk4+TAtCz97+E0xha2enfBR9STxhkbfGW8nH1Uki0WpKolx+thiwC2Og9N2wpBkTV693pLS14bxSJxrYmouv1NtJbVD9HVpPlmMVAPphaAweO4Xa4bvsiYhM4mIuDdSYB3TvhUIw0b+H/Dadx/REkt8dn+MeKLG8kZOtyAagbXh1rZGmlhEDUE46LXfeCsoKMPEeRB6jIG3dBnqkibxVUEBeqiYtZ22C0pGFyI3AHj6T2ZekPv7bhzDFeTSipJM48Czve6II4qyoreuWwQTLXd10xMi21d+/FIzXIpXovtEqA9Flp6XIa84jXOHlOERcHAQpX0dFP6vVUWmX0eyy1DDk+SkBfda1lTszis942rzedGkUdpYQjQz1PVymhIQfV8/sf7YwO2RhJgFxUinht6YZEZp/pRkXjjov4oaQSef8cSBuBQ4AGdo9ZlKWPEfU9gtmwDZdXk+5XZUq9cvnp+4CaUUTXstrFJknR6TqBrVuBEayBN21GjaBsKLWj4pMnzAgsVjwZiXBLeK59BWfHd68SkIuxIN/RMs7a0Sonh61tBBzPYUUd5S+mrZ6nMq+aHDd+5Bwc/+H8yLrAF2Fj44z5kXWBFbxtnK9gtWQPGCG8pqKnRMIkaSCfuFyVsO+xXLWOe+dxfSnBWOvs3WCNoo7cfdU8levKTONE5W3m8S7JW1nlENfr9zrkV0CiiV5VD4VDVTmU1rXRgq58D3xQfO/MR+EbfH6hM7HGkATI//q534JUEdpnWWQbSkKTZoONArHj8DVaxlv9/xVJuwSrV0IbdOSuO6hlt3y0hpEUna7OteWu4CFSLq3OzRe1WQTIF7WZE7kYGylnla1txKkrmDtKfGzruLrVPly3yrY+Pm2dm5XpOQO/+f7t5QECuDb9/eXxexwVkmjxyrJYcfT79yS2GEpN9Lj2eqxJlzXJkpfH55enh29//Pr8cN9wO20CZ/3ejtiYWk3rzrUCp7ZpXyPIj84SrqbeLX1N3XAUyftY4RiN8pfPGuQGcLr/WUDyUO9/e2E+/Ac=</diagram></mxfile>
</myxml>
```

This works because different inflected forms of a lemma 'overlap' with different other lemmata. So while 'arma' in <em>Aeneid</em> 1.1 could be 'armum' the noun or 'armo' the verb, 'armate' in <em>Aeneid</em> 9.114 could be 'armo' the verb or 'armatus' the adjective (the former option is correct in both cases). Over millions of tokens, the frequency counts in the model gradually begin to reflect the true rate of appearance of each lemma. 

## How well does this work?

I trained this model on the Tesserae Latin corpus (some 8 million words of Latin poetry and prose). Then I used the model to create a lemmatizer that returns all possibilities for an ambiguous form, but weights the probability of each lemma according to its frequency in the model. 

I tested the lemmatizer against ~17,000 words of Latin from the cltk corpus whose correct lemmatizations have been entered by hand. In ambiguous cases, my script chooses the most probable lemma according to the unsupervised model. The result was correct roughly 91% of the time. Let's break down those results.

First, it should be said that 73% of the tokens in this data set are unambiguous–they can only come from one lemma, so you basically get those for free.

Second, if you guess randomly in ambiguous cases, you happen to be right about about 30% of the time. So a random selection gives roughly 81% accuracy.

Using the unsupervised frequency model, we end up guessing correctly in 66% of ambiguous cases, for a total accuracy of ~91%. That's strong enough to suggest that the model of language frequency seen here is good enough to expand to other NLP tasks or combing with other unsupervised lemmatization techniques.

## Observations

A few things about this model surprised me. First, if we only count unambiguous forms, the model doesn't lead to a successful lemmatizer. In fact its accuracy drops <em>below</em> what we see through random selection.

Originally this model was developed as part of a more complex lemmatizer that looked at surrounding language. It became clear that nearby words were not as effectual as word frequency during development.