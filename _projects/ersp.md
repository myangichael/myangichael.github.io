---
layout: page
title: ERSP Research
description: detailing my Early Research Scholars Program work, image credited to Arthur Selle Jacobs, Roman Beltiukov
img: assets/img/projects/ersp/trustee_jacobs_beltiukov.jpeg
importance: 2
---

I undertook a year-long (academic year) research project alongside Abel Atnafu, Luis Bravo, Aditi Phatak, and Emily Hu as part of the UCSB Early Research Scholars Program (ERSP). This research was a partnership with the UCSB Systems and Networking Lab, headed by Professor Arpit Gupta. Our research mentor was Roman Beltiukov, and the project we were working with was published by Arthur Selle Jacobs and Roman Beltiukov, titled [AI/ML for Network Security: The Emperor has no Clothes](https://sites.cs.ucsb.edu/~arpitgupta/pdfs/trustee.pdf)

All of my technical work was done in Python, with heavy usage of `pandas` and `PyTorch` to load data and build/train my models. Also used a great deal of `sklearn` for tree-based models, and `matplotlib` for data visualization. We ended the project with a poster presentation at the UCSB CS department's undergraduate research fair.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ersp/poster.png" title="Final Research Poster" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

You can view our final research poster in greater resolution [here](https://docs.google.com/presentation/d/1V1tX5XgU97CPWW8AC1FKUjQi0PnCE7a0baB7sWcHmwM/edit?usp=sharing). I recently got a new laptop and no longer have access to the server on which much of my code is stored. Once I go home and open that laptop, I will transfer more code over. 

# A quick summary with TLDRs throughout:

## Context:

The networking space stands to benefit greatly from advances in machine learning and artificial intelligence. Network providers/operators receive and send tons of network data regularly, all of which needs to be safe. Naturally, you might think that AI could be applied as a way to classify network packets as safe or unsafe.

There's just one issue: most network operators don't quite trust ML to manage their systems. Why?

First, networking data used to train models is hard to access. Classification tasks require lots human-labeled data—labeling data. Labeling network data specifically requires a high level of expertise and is extremely time consuming.

Also, lots of networking data is privately controlled by network operators, and for privacy and reasons they can't release it to the public or for research. 

Therefore, many modern network datasets we might use to train models for network-related tasks are synthetic. But because these are technically not "real" data, they don't always properly represent real-world network data flow. They might also be structured differently based on the devices involved, the experimenter's decisions, etc. 

Also, industry standard machine learning models like neural networks (and even some non-deep learning models like random forests and gradient boosting) are what we call [black-box models](https://umdearborn.edu/news/ais-mysterious-black-box-problem-explained). We can't directly access a black-box model's logic to make sure it's basing its decisions on the correct features.

Consider a dataset built with a network of three devices, `A`, `B`, and `C`. We'll send network packets from `A` and `B` to `C` to build the dataset. However, say we've designed `A` to send only normal network data, and `B` to send malicious data. In our dataset, if we have IP Address as a feature, the model will probably figure out that only `B` sends bad data. Therefore, under the hood, the model learns a shortcut: all data from `B` is labeled as malicious.

In practice, this could be catastrophic. If we switch out `A` and `B` for new devices with different IP addresses, the model might not be able to differentiate between safe or bad packets anymore. Of course, there is the possibility that it still can, but technically we won't ever know until we evaluate it on data out of the original training set (black-box model issue). But because not many datasets are available (and often different datasets are formatted differently), we might not have a proper testing set to look at (i.e. the testing set is still using `A` and `B`), and so we falsely believe our model is robust.

This example seems fairly obvious to deal with in experimental setup, but similar issues like this can occur with any feature if we're not careful. As the original paper shows, these issues absolutely *have happened*, and in large, recently published datasets as well.

#### TLDR
Networking tasks are good opportunity to apply ML (lots of data, high frequency). Networking datasets are hard to create due to cost and privacy, we rely on synthetic. Good ML models are black-box, with no observable logic. These combine to make ML models hard to analyze, hard to evaluate their quality. Network operators don't like that, and therefore they don't trust many black-box ML solutions.

## Solution

Thus, TRUSTEE, or TRUSt-oriented decision TreE Extraction comes into play. TRUSTEE was developed by Arthur Selle Jacobs and Roman Beltiukov (and others listed in the paper), and is a framework for training easily readable surrogate decision trees on black-box models. That way, we can find out about some of the decision-making process in the model without using extra data.

I don't explain decision trees, but you can read about them [here](https://en.wikipedia.org/wiki/Decision_tree).

The specific TRUSTEE documentation is available [here](https://trusteeml.github.io/), but in general know that it can be used on any Python model object that has a `forward` and a `predict` method.

The goal of the surrogate decision tree is to learn the decision-making process of the black-box model (to the best of the tree's ability). If the fit is very accurate, we can *somewhat* assume that the black-box is making decisions based on what's outlined in the tree.

We then look at the top, most significant splits in the tree, and ensure that none of the features being used are problematic [shortcut features](https://www.nature.com/articles/s42256-020-00257-z). "Problematic" is extremely subjective to the dataset—what's problematic about some feature in dataset A maybe not be in dataset B.

That being said, my immediate question was, why bother with the black-box at all? If this architecture can fit decision trees to get similar results as compared to the black-box (which we'll assume has fairly high accuracy), why spend the extra resources and time to train the black-box?

Short answer (and what some of the research demonstrates), decision trees lack complexity. If the relationship between features and classification result is more complex than a DT can represent, they will oftentimes underfit. So, there are very likely cases where a neural network might outperform decision trees *significantly*, and there's no way to fit a surrogate decision tree. This case applies much more often in vision and NLP problems, where decision trees are essentially unusuable compared to modern approaches.

We tested boosting/bagging tree models, like [XGBoost](https://xgboost.readthedocs.io/en/stable/) and [Random Forests](https://en.wikipedia.org/wiki/Random_forest), but I admittedly didn't work much on tree-based black-box models, so I don't have much to say about their performance with TRUSTEE.

Back to NNs though—general intuition was that if the DT fits the NN really well, we might have an issue: there might be some really highly valued feature the NN is using as a shortcut that's expressed as the top-few splits in the decision tree. We use the first DT splits (technically we display only the top-`k` decisions with some predefined `k`; Abel worked on tuning the default `k` value), because they split the most data points (DTs trained with entropy) and are the most likely candidates for shortcuts.

Given these high impact features, we can then evaluate and see if they're problematic. Because they're network features though, it does require some networking expertise to determine how problematic they really are.

If the DT doesn't fit the NN at all, this framework isn't really applicable anymore. TRUSTEE is good at immediately catching shortcuts if they're there, but other types of black-box model issues can't really be caught.

#### TLDR

TRUSTEE trains surrogate DTs on black-boxes. DTs are easily readable, and we use them to analyze the black-box models. NNs are more complex than DTs, and DTs often underfit in complex tasks that require NNs. So if the DT fits the NN really well, it might mean we have a couple highly valued features involved that we should look at. Overall, TRUSTEE provides good insights into model decision making, but the features should be analyzed by a networking expert for final evaluation.

## Conclusion

TODO

TODO: add my code to repo and link, add proper citation below, maybe add some other research materials used