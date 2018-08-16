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

This is a basic question in language modeling. To answer it, we need to group together all the strings in our corpus that belong to the same word. This is called lemmatization.

To do this in an unsupervised way, I grouped together all the tokens in the text that might have come from the same lemma. The same token can be included in more than one grouping, which means some lemmata are being counted even when they aren't actually present. It happens when an inflected form in the text could come from more than one lemma. So how does this help create a useful language model?

The answer is that most (if not all) lemmata have inflected forms that aren't ambiguous. Whenever an unambiguous form is seen, only the correct lemma is counted. Over millions of tokens, the frequency counts in the model gradually begin to reflect the true rate of appearance of each lemma. 

## How well does this work?

I trained this model on the Tesserae Latin corpus (some 8 million words of Latin poetry and prose). Then I used the model to create a lemmatizer that returns all possibilities for an ambiguous form, but weights the probability of each lemma according to its frequency in the model. 

I tested the lemmatizer against ~17,000 words of Latin from the cltk corpus whose correct lemmatizations have been entered by hand. In ambiguous cases, my script chooses the most probable lemma according to the unsupervised model. The result was correct roughly 91% of the time. Let's break down those results.

First, it should be said that 73% of the tokens in this data set are unambiguous–they can only come from one lemma, so you basically get those for free.

Second, if you guess randomly in ambiguous cases, you happen to be right about about 30% of the time. So a random selection gives roughly 81% accuracy.

Using the unsupervised frequency model, we end up guessing correctly in 66% of ambiguous cases, for a total accuracy of ~91%. That's strong enough to suggest that the model of language frequency seen here is good enough to expand to other NLP tasks or combing with other unsupervised lemmatization techniques.

## Observations

A few things about this model surprised me. First, if we only count unambiguous forms, the model doesn't lead to a successful lemmatizer. In fact its accuracy drops <em>below</em> what we see through random selection.

Originally this model was developed as part of a more complex lemmatizer that looked at surrounding language. It became clear that nearby words were not as effectual as word frequency during development.