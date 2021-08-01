---
layout: post
title:  "How Can We Accelerate Progress Towards Human-like Linguistic
Generalization?"
date:   2021-07-31 23:02:17 -0400
categories: paper discussion
---

How Can We Accelerate Progress Towards Human-like Linguistic
Generalization?

This is a position paper, and frankly a lighter read for folks who perhaps haven't delved too deeply into NLP research. With that being said, the paper covers some historical research developments in the last few years that are definitely appreciated better with some background in generative pre-trained (GPT) models.
I will give that context here too. It really begins with what has been termed ["NLP's Imagenet moment"](https://ruder.io/nlp-imagenet/) when the first GPT models came into existence. These models were already pretty heavily parameterized, with weights learned on a generative language modeling task. The big idea, which had been circulating in the computer vision community for years, was to then use these
these models with generalized language modeling capabilities to fine-tune on downstream tasks so as to build on top of the linguistic capabilities encoded in the base model.

This was genuinely cool in 2018, but it's been 3 years since then. What's changed? Instead of instituting architectural innovations to push NLP forward, the industry-adjacent research labs of the world have gotten a ton of credit for increasing the amount of training data these models use, and building bigger models.
There are commensurate increases in the performance metrics achieved by these models due to these changes, but "this jump in accuracy does not reflect significant modeling innovations." 
This is indeed true, assuming you have the prerequisite hundreds of GPU's to actually work with and train these models.
The advances that non-NLP people have paid attention to in the past few years has been directed towards these GPT-3's and RoBERTa's of the world. It is inarguably cool to have a conversation with a surface level competent bot. 

But, Tal Linzen points out in this paper that while great for clicks, these models have led us astray from what NLP research should really be aiming towards: achieving human-like linguisitic generalization. And on this premise alone, I cannot agree more. The author points out two areas of concern here: model evaluations that are agnostic of pretrained datasets, and the identical distribution of training and test sets.
These issues are pretty heavily related. The first concerns issues arising from pre-training on massive corpora. The author provides some concern around actually comparing different model architectures when trained on alternative samples of datasets. This is less of a concern than the cognitive science consideration the author brings up: training on more data leads us astray from mirroring the sample-efficient learning humans exhibit.
We don't need to read 3 billion tokens of the internet to use language.

The second area of concern is the identical distribution of the pre-training dataset with downstream evaluation datasets. Train-test splits are not a valid way of assessing language model performance because the system acquires generalizations from the data that positively reflect in accuracy metrics, but would appear catastrophic to a human evaluator. The author suggests evaluation on separate tasks and datasets in order to assess exactly what generalizations, if any, a model has learned.
This includes multi-modal datasets, an idea which theoretically makes sense, but in practice might prove complicated as different architectures are better suited to say, spectrogram data. I think this suggestion is mainly embodied in current approaches around probing datasets to understand if a model trained for one task has implicitly encoded abilities required for that task. For instance, a model trained for part-of-speech tagging should also exhibit robust verb identification capabilities. My previous post covers the idea of probing in greater detail, and it seems this approach has been adopted across significant NLP research contributors, which in short, is awesome.

I want to now take issue with some of the ideas presented in this paper around mirroring human learning. 'Human' is mentioned 40 times in the paper, so this notion of human language learning is pretty essential to the argument the author is making. They discuss our inductive biases that lead us to acquire and learn language robustly, a discussion I find so refreshing in NLP research.
However, we should really consider what this inductive bias looks like and how it manifests. Thinking on an evolutionary scale from the early signaling of our prehistoric ancestors, one could make the case that this genetically encoded experience is our generative pre-training. This is a vast over-simplification, but the presence of innate language faculties suggests that we have adapted to have architecture suited for advanced language skills, acquired evolutionarily.
The architecture search may very well have been random, as opposed to a gradient-descending pre-training algorithm, but we got to a point where we as a species have general, language acquisition faculties that advantage us over our closest relatives incapable of conceiving colorless green ideas. We may not be personally pre-trained, but our internal architecture most certainly is a productive of eons of linguistic experience, so I hesitate to do away with the idea that pre-training is wholly at odds with the derivation of our human language faculties.
Jung's collective unconscious comes to mind here as the clearest psychological analog to human pre-training. 
This is veering off, but I have some alternative ideas around generative pre-training with smaller sample sizes to mimic human language acquisition. I took a class my senior year on this subject, and am excited that the cutting edge of NLP research is moving in this direction.
 
At the end of the day, I would hesitate to say that general pre-training is at odds with mirroring human language acquisition. After all, our neural weights are generally not randomly configured at birth. Most importantly, I don't think mirroring human language acquisition should be taken as dogma. DaVinci did not succeed in mimicking birds' wings to fly; we took the underlying principles to create something even more powerful.