---
layout: post
title:  "Learning Which Features Matter: RoBERTa Acquires a Preference for
Linguistic Generalizations (Eventually)"
date:   2021-08-10 23:02:17 -0400
categories: paper discussion
---

Learning Which Features Matter: RoBERTa Acquires a Preference for
Linguistic Generalizations (Eventually)

Alex Warstadt, Yian Zhang, Haau-Sing Li, Haokun Liu, Samuel R. Bowman

This paper was a great read for two reasons. Firstly, its findings rebuke a recommendation against expansive training sets laid out by the paper in [my last post](https://danpechi.github.io/paper/discussion/2021/08/01/human-like-linguistic-generalization.html). Secondly, I didn't understand this paper well when I first tried reading it a month or two ago, and now I have a great idea of what it's about, and really like it.
It's papers like these that make me remember the feeling of first understanding how the hell an LSTM worked and getting context for subsequent papers, although admittedly probing is not quite as technically demanding on the layreader to understand.

Although I need to read more papers, it seems probing is the newest avenue along which much of the research I care about is expanding. Just finding minor algorithmic modifications that achieve marginal accuracy or perplexity has given way to actually understanding what language models (LMs) like BERT understand.
The authors of this paper dig into [ROBERTa](https://arxiv.org/abs/1907.11692), the female and more powerful descendant of BERT. The authors achieve this through an experimental setup that takes the idea of probing to an extreme.
In [the paper from my first post](https://arxiv.org/abs/2106.00737) the authors sought to understand what meaning was implicitly represented. This paper explores similar concepts to ask not what meaning is represented and whether it's useful, but whether the model has inductive biases towards surface level meaning or actual linguistic meaning. It's all the same in the world of distributional semantics though, right?
The idea here is that one can ask two questions of a sentence, one which requires attending to surface level information, and another requiring attention to linguistic information. Let's use these sentences: 

"He hugged the angry girl" and "He who hugged the sad girl was angry"  

A probe requiring surface level information would ask "Does 'he' proceed 'girl'?" A probe requiring linguistic information would ask "Does 'angry' refer to 'he' or 'the girl'?" The first question could be solved with 'an expert system', the latter requires doing the sort of tree parsing of [early RNN models](https://nlp.stanford.edu/pubs/tai-socher-manning-acl2015.pdf).
An overparameterized LM (or more general neural network) can just as well [encode these surface level heuristics](https://arxiv.org/pdf/1711.11561.pdf). This is obviously bad, and we would hope pre-trained models actually have embedded linguistic meaning in favor of surface level meaning.
To test this, the authors use an experimental setup that involve overlapping objectives of a surface-based classification and a linguistic based classification in what the authors refer to as an ambiguous experiment which follows the [poverty of the stimulus design](https://linguistics.ucla.edu/people/wilson/VelarPalCogSciWilson.pdf). This ambiguous fine-tuning is performed on a pre-trained model, with the subsequent model tested on disambiguated data to determine whether the model has learned to use linguistic meaning.
This would be sufficient if not for the fact that these initial models demonstrate limited linguistic representation. So, the experimenters perform an 'inoculation' experiment in which the model is further fine-tuned on an ambiguous dataset with non-ambiguous training samples mixed in. The idea here is that models which already exhibit some biases towards using linguistic information will require less inoculation than those that haven't learned to use linguistic information.
This design, while a bit complicated, at its core tests language model's preference for using linguistic generalizations as opposed to surface level generalizations. 

In addition to running different combinations of ambiguous linguistic and surface level feature experiments, the authors experiment with different pre-trained models, different sizes of pre-trained data sets, and different degrees of inoculation.

For the first set of IV's, there is a noticeable difference in model performance. The authors note that they excluded some experiments because they were unable to achieve a good enough performance on control experiments, so the full range of combinations is not explored. However, for those combinations that do persist, all linguistic-based classification ambiguated by lexical content classification demonstrate linguistic preference in the pre-trained model.
The authors tested 12 ROBERTA models they pre-trained, likely as a form of cross-validation, and 1 pre-trained ROBERTAbase model that had been trained on approximately 30B words. The authors demonstrate that with increased training data, all models derive preferences for linguistic generalization. The authors point to the orthography and morphology experiment as being representative of a broader trend in which increasing linguistic bias is achieved by each additional factor by which the training set is expanded.
Unsurprisingly, increasing levels of inoculation also improves linguistic preference, however it is usually the combination of inoculation and increased dataset size that achieves models with the strongest linguistic preferences. ROBERTAbase requires the least amount of inoculation and demonstrates some linguistic preference without it, however ROBERTA language models more generally seem to require more training data to induce inductive biases for linguistic and not surface information.

So, the solution here is to just train your model on as many words as possible to create strong inductive biases for linguistic generalizations. Well, in the short term, this may be the case, but this begs the question whether there are more efficient means of producing these linguistic inductive biases. As [Linzen notes](https://tallinzen.net/media/papers/linzen_2020_acl.pdf), we shouldn't need 30 billion words of training data to use linguistic features given human language acquisition. In my mind, there's so much dependent on training data here that remains unexplored.
I can imagine giving a language model a series of sentences that would bias it in such a way that it may never encounter certain linguistic concepts, or at least encounter them infrequently. This is obviously non-conducive to achieving the inductive biases we hope for, and is likely to occur in our smaller datasets, but could the 1M word sample merely be arranged in such a way to achieve the same model weights as a much larger sample? This paper again underscores the need for simplified training regiments that lead to useful inductive biases.

Worth noting is they do a great job documenting their experimental setup, and their examples of ambiguous training samples were helpful for understanding their experimental setup. I wonder how these ideas fit in with a reader's attention while reading - do they have biases towards one task over the other? I imagine an experiment in which the ambiguous training examples are given to children to read, and an eye motion sensor can be used to detect what they are looking at to parse the sentence. Regardless, this paper had many wonderful citations that I want to read more on;
of particular interest are [(Voita & Titov 2020)](https://arxiv.org/pdf/2003.12298.pdf) and [(Warstadt et al. 2020)](https://arxiv.org/pdf/2007.06761.pdf).

I had a chance this past weekend to chat with some folks about NLP in NYU's neurolinguistics program, and hear about their work, which was very inspiring and cool. I notably got some great recommendations for the Basque country from a local, and discuss some ideas about linguistic drift and information theory I have with people who are a lot closer to this exciting area of research. 