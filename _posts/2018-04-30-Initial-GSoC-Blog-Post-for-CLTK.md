---
title: "Google Summer of Code Initial Post"
layout: post
date: 2018-04-30 11:59
tag: Corpus Linguistics
tag: Google
teaching: false
blog: true
draft: false
author: James Gawley
summary: "Introduction to 2018 Google Summer of Code Project"
 
---
<em>This post was originally submitted to the Classical Language Toolkit's blog at the outset of the 2018 GSoC period.</em>

My name is James Gawley, and I'm a PhD candidate in Classics at the University at Buffalo, SUNY. My dissertation is about how poets manipulate reader attention and memory to craft successful allusions. In particular I'm focused on Vergil's relationship to Homer, which means I'm looking at Latin allusions to Greek poetry. I take two fundamentally different approaches to the research: on the one hand I gather responses from expert readers who try to formally describe the similarities between known allusions, and on the other hand I build computer models to derive all the points of similarity between the entire texts, not limited to known connections. I believe that when we compare what a computer derives and what a human notices, we will learn something fundamental about how allusion is signalled to the reader.

The first part of my GSoC proposal for CLTK involves two steps. First, I will add the dictionaries my friends and I have developed for suggesting Latin-to-Greek translations (and vice versa), as well as dictionaries of intra-language synonyms. Second, I will combine those translations and synonyms with CLTK's 'backoff' approach to lemma disambiguation. Right now, the translation and synonym dictionaries suggest a list of words without telling the user which translation or synonym is more probable. But the probability of each translation or synonym is critical for many NLP applications. So what determines which translation or synonym is most likely? The answer is context, and that's what CLTK's backoff lemmatizer analyzes. Once these tools have been combined, CLTK users will be able to ask, for any given word in context, what the most probable translations or synonyms might be.

The second thing I'm going to do during my GSoC fellowship is to add pre-trained word embeddings to CLTK. Embeddings are a way of getting at the meaning of a word through the context in which it appears. For example, the words 'monarch' and 'king' probably appear in similar contexts in an English corpus. The neat thing about embeddings in particular is that they use latent variables that are so finely tuned that they incorporate all the contexts in which a word appears, and one can add or subtract parts of that context with interesting results. To take a famous example, if one subtracts the vector-representation of the word 'man' from the vector representation of the word 'king' in a well-trained model of English, the resulting vector representation is closest to that of the word 'queen.' In other words 'king' – 'man' = 'queen' in English. The same thing is true for the Greek and Latin vector models I have trained for Latin and Greek, which I will add to the CLTK.

I'm looking forward to working with Patrick Burns and Kyle Johnson over the next few months, and I can't wait to make this technology available to the CLTK user base!