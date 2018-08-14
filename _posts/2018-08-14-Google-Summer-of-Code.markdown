---
title: "Google Summer of Code Results"
layout: post
date: 2018-08-14 11:59
tag: Corpus Linguistics
tag: Google
teaching: false
research: true
blog: true
draft: false
author: James Gawley
summary: "Results of 2018 Google Summer of Code Fellowship through the Classical Language Toolkit"
 
---
Overview: 

The Classical Language Toolkit (CLTK) is a suite of Natural Language Processing (NLP) tools used by humanists to study ancient texts. The original focus of the project was Latin and Greek, and the most sophisticated tools are available only for these languages. However, one of the main goals of the project is to support scholarship into cultures outside of the Western canon, particularly where NLP tools are not available.

What I Set Out to Do:

Most NLP techniques rely on a large corpus of training data. For example 'lemmatization,' wherein all the inflected forms of a word are analysed as a single item, is often done by training a lemmatizer on a large group of texts whose words have already been grouped by lemma. Machine learning techniques are applied to build a model, and the model is then used to lemmatize texts which have not been analyzed by hand.

However, under-studied languages lack adequate training data to support this standard approach; there just aren't enough texts which have been hand-curated to train a model. Therefore I set out to build an unsupervised model which can learn, for example, the correct lemmatization without 'knowing the answers.' The goal is to provide accuracy comparable to supervised approaches, without the need for hand-curated training data.

Lemmatization is a first step, and it is useful because the success of an unsupervised algorithm can be easily tested. However my unsupervised model can be extended to create tools for, e.g., cross-language document alignment, where testing is more difficult.

# Steps Completed:

* Added lemmatizers for Greek and For Latin that provide all possible word groupings
* Built an unsupervised language model extensible to other NLP tasks such as translation or document alignment
* Used the language model to build an unsupervised Latin lemmatizer with > 90% accuracy
* Added tools to suggest synonyms for Latin and Greek words
* Added tools to suggest Latin translations for Greek words, and vice versa

# Additional Service Completed:

* Coordinated the incorporation of CLTK into the core logic of the next generation of the open-source [Tesserae Project](http://tesserae.caset.buffalo.edu)
* Expanded the CLTK corpus of texts with aligned translation of Latin and Greek (useful for testing translation tools)

# Steps Remaining:

* Build an unsupervised language model for Greek
* Use Greek model to build unsupervised lemmatizer for Greek
* Use Greek and Latin language models to assign probabilities to potential synonyms and translations

# Where the code lives:

## Already Pulled into CLTK:
* [A dictionary of lemmas for Latin word-forms](https://github.com/cltk/latin_models_cltk/blob/master/semantics/lemmata.py)
* [A dictionary of Greek translations for Latin lemmas](https://github.com/cltk/latin_models_cltk/blob/master/semantics/translations.py)
* [A dictionary of Latin synonyms for Latin lemmas](https://github.com/cltk/latin_models_cltk/blob/master/semantics/synonyms.py)
* [Dictionaries of lemmata, synonyms, and Latin translations for Greek words](https://github.com/cltk/greek_models_cltk/tree/master/semantics)
* [A tool for looking up all possible lemmas of a Greek or Latin word](https://github.com/cltk/cltk/blob/master/cltk/semantics/latin/lookup.py)

## Not Yet Pulled into CLTK:

* [The unsupervised model and unsupervised lemmatization tool](https://github.com/jamesgawley/cltk/tree/master/cltk/lemmatize/latin/unsupervised.py)
* [Experiments with various unsupervised language models](https://github.com/jamesgawley/latin_lemma_disambiguation_models)
* [The new corpus of plaintext, aligned Latin and Greek](https://github.com/jamesgawley/greek_text_greek_fragmentary_historians)
* [A corpus of 10 million words of Latin poetry and prose, used to train the unsupervised model](https://github.com/jamesgawley/latin_text_tesserae_collection)

# Documentation:

* [How to use the lemma lookup tool](http://docs.cltk.org/en/latest/latin.html#semantics)
* [The logic behind the unsupervised lemmatization model](https://jamesgawley.github.io/Unsupervised-Lemmatization-Model)
* [Initial GSoC blog post](https://jamesgawley.github.io/Initial-GSoC-Blog-Post-for-CLTK)

# Learning Experience:

* Improved Python coding skill
* Developed better habits for open-source contributions
* Learned how large coding projects are managed smoothly