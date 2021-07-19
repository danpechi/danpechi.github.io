---
layout: post
title:  "Intermediate-Task Transfer Learning with Pretrained Models for Natural
Language Understanding: When and Why Does It Work?"
date:   2021-07-16 23:02:17 -0400
categories: paper discussion
---

Intermediate-Task Transfer Learning with Pretrained Models for Natural Language Understanding: When and Why Does It Work?

This is my second blog post. I intend to make these posts more frequently now as I've done the post-vaccination family visits I wanted to make.
I saw a thread from NLP Twitter icon [Yoav Goldberg](https://twitter.com/yoavgo) a few days ago about it being a bad time to get into ML, and presumably by extension, NLP research. I think this paper gives some ideas of why this is the case.
In the post-generalized-pre-training (GPT) age of NLP, there's an exceeding amount of focus on these models. In the fall/winter of 2018, there was a flurry of hype around these models, and the hype has perhaps, started to die down.
I should take this time to plug some research that sought a different path at around the same time as GPT mania swept in. Harvard NLP put out [this tutorial on latent variable models](https://arxiv.org/pdf/1812.06834.pdf) that was a stark, and novel contrast to seemingly everything else coming out at the time. 

Now, getting back to the GPT hype. At present, there still exists tons of questions around why and how GPT works. My previous post explored a paper that delved into the how in a good level of detail, the main finding that there was poor semantic encoding as shown through probing tasks.
This paper exists as an exhaustive search of approaches around transfer learning and probing tasks to brute force an answer to how and why these models perform the way they do.
More specifically, the paper focuses on answering the following:

• What kind of tasks tend to make good intermediate tasks across a wide variety of target
tasks?

• Which linguistic skills does a model learn
from intermediate-task training?

• Which skills learned from intermediate tasks
help the model succeed on which target tasks?

An intermediate task is a task meant to fine-tune the parameters of the model. For instance, one might imagine using an intermediate task of broader QA before tackling a more specific QA dataset; a transfer learning experience if you will.
After learning this intermediate task, the model is then fine-tuned on and applied to a target task. You can imagine 2 intermediate tasks and a single target task and being able to answer which intermediate task was more helpful. This paper expands this to 11 intermediate tasks and 10 target tasks.
A final step is taken with a probing task akin to the previous paper, used to answer what exactly was learned that contributed to performance on the target task.

The paper finds that specific intermediate task training does matter, and that there's a pattern to which tasks improve performance the most.
More specifically, the authors found certain tasks that would lead the model astray in target task performance, and others that led to gains in target task performance. 
The intermediate tasks that improved performance were of a similar ilk: those focused on broad, general knowledge. [Commonsense QA](https://aclanthology.org/D19-1243/) focuses on a form of reading comprehension, and [HellaSwag](https://aclanthology.org/P19-1472/) requires the model to complete a story. 
This is compared with poor performance on tasks that are more narrow, including one testing social intelligence, and another tagging word tokens. 
This ties into the authors' explanation of catastrophic forgetting deriving from intermediate task training impacting target task performance. The remedies the authors suggest here make sense. I would be interested in seeing whether freezing certain layers of the network would also be beneficial here as described by [Howard & Ruder, 2018](https://arxiv.org/pdf/1801.06146.pdf) and in [my last old blog post](https://dandeeplearningblog.wordpress.com/2019/01/13/1-13-19-an-update-on-fine-tuned-language-models-and-nlps-imagenet-moment/)

The authors point out that the probing tasks which correlate best with target task performance closely resemble masked language modeling, which is effectively the pre-trained model, so not all that surprising in this case. Otherwise, "there is little to no correlation between target-task and probing-task performance for these skills." Spooky.
I think there remains a lot more work to be done with probing to make this a completely fruitful venture as any probing data set likely exhibits biases that makes it difficult to say that performance on such a task means knowledge of a concept. Unclear what that solution is exactly, although I think pruning the dataset of outlier data points, or expanding the datasets could perhaps be useful.

Overall, this paper partially peels back the layers of the mysterious black boxes of GPT models. This touches on an idea I've wanted to explore for a while around training regiments, and ordering of training tasks to be completed in a way that builds and doesn't chip away at consolidated learning (catastrophic forgetting).
Concepts in humans are built hierarchically (one needs to know some basic human biology before understanding the limbic system), and we should expect the same from the BERT's and ELMO's of this world. I'd be curious to play around with layer freezing and creation to vaguely mimic the growth of new human neural networks. 
Ultimately, this paper leaves a lot more questions that I hope to explore in future blog posts. 