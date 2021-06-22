---
layout: post
title:  "Implicit Representations of Meaning in Neural Language Models"
date:   2021-06-21 23:02:17 -0400
categories: paper discussion
---

Implicit Representations of Meaning in Neural Language Models

This is my first blog post on an actual paper in ages, so this is likely to be relatively poor quality. I wanted to start out with a more recent paper as there is inevitably some information-dense content worth unpacking for those like myself who haven’t been keeping quite as up to date with advances in NLP. This paper did not disappoint in this respect.
The paper tackles an increasingly important question around what neural language models (NLM’s) know. This question of what LM’s know has come a long way from [Andrej Karpathy’s sentiment neuron](http://karpathy.github.io/2015/05/21/rnn-effectiveness/), and seeks to integrate notions of explainable AI with formal linguistic theories centering around world models. There are some clear threads here as well between this paper and [Experience Grounds Language](https://arxiv.org/pdf/2004.10151.pdf), which I will be posting about on this blog in the future.
So, how do we get to what a language model knows? The answer, in short, is probing. 

Probing allows one to determine what a language model (or layers in a model) represent by comparing the accuracies of models built using the weights. The weights are used to construct models on a target task, and a general, control task. If the weights are salient, say for encoding parts-of-speech, higher accuracy will be achieved on a downstream part-of-speech tagging than a control task associating word types with random outputs. The authors cast some doubt on what ELMo knows in the paper which is worth checking out in and of itself as we contend with such models and their biases being deployed IRL.
([Hewitt and Liang, 2019](https://arxiv.org/pdf/1909.03368.pdf)). 

The authors probe their model using 2 datasets, one which involves relatively straightforward manipulations of beakers, and another involving a more complex world of entities, and relations that, as we will find out, is a bit harder to encode meaning from. We take our language model representations of this world, and to assess their semantic value, input them alongside propositions that are either true, false, or unknown into a simple, linear classifier:
cls$\theta$(embed($\phi$), loc($\phi$, E(x))) = I($\phi$)

“the classifier is a linear model which maps each NLM representation and proposition to a truth value. In Alchemy, a linear transformation is applied to the NLM representation, and then the proposition with the maximum dot product with that vector is labelled T (the rest are labelled F).”

The idea here is that our classifier shouldn’t have to be complex because we have encoded everything we need to know (or at least enough of what we need to know) in our LM embedding. If this is the case, our classifier will have high accuracy in resolving our information state I($\phi$). 

The authors of the paper find that the NLM does present some signs of encoding meaning, although I remain a little unconvinced. As the authors reluctantly admit at the end of their paper, “even in the best case, complete information states can only be recovered 53.8% of the time in tasks that most humans would find very simple.”  I would be curious to see activations and activation patterns be considered in the context of meaning more broadly, especially in the context of probing. Although the weights of the model certainly should encode meaning, and these impact activations, the specificity, especially of the language used in Alchemy is so limited compared to the generalized embeddings of the base LM. Some fine-tuning, on say, a science-oriented corpus may also prove useful.

However, assuming the search for meaning (in LM's) is indeed a fool's errand, the findings of this paper really bring home the idea that distributional semantics are no stand-in for the colorful semantic world beyond any corpus. I'd be curious to see how T5 and BART perform relative to the 84.6% accuracy achieved by a fine-tuned BERT ([Brown et al.](https://arxiv.org/pdf/2005.14165.pdf)).  


Here are some future papers that I will hopefully get to that get into greater detail on biases and meaning in language models:

Emily M. Bender and Alexander Koller. 2020. Climbing towards NLU: On meaning, form, and understanding in the age of data.

Emily M Bender, Timnit Gebru, Angelina McMillanMajor, and Shmargaret Shmitchell. 2021. On the dangers of stochastic parrots: Can language models be too big?