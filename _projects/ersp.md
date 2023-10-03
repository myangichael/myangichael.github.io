---
layout: page
title: ERSP Research
description: detailing my Early Research Scholars Program work, image credited to Arthur Selle Jacobs, Roman Beltiukov
img: assets/img/projects/ersp/trustee_jacobs_beltiukov.jpeg
importance: 3
---

I undertook a year-long (academic year) research project alongside Abel Atnafu, Luis Bravo, Aditi Phatak, and Emily Hu as part of the UCSB Early Research Scholars Program (ERSP). This research was a partnership with the UCSB Systems and Networking Lab, headed by Professor Arpit Gupta. Our research mentor was Roman Beltiukov, and the project we were working with was published by Arthur Selle Jacobs and Roman Beltiukov, titled [AI/ML for Network Security: The Emperor has no Clothes](https://sites.cs.ucsb.edu/~arpitgupta/pdfs/trustee.pdf)

Brief summary of the work itself: the networking space stands to benefit greatly from advances in machine learning and artificial intelligence. Network providers/operators receive and send tons of network data regularly, all of which needs to be safe. Naturally, you might think that AI could be applied as a way to classify network packets as safe or unsafe.

However, networking data is privately controlled by network operators, and for privacy reasons they can't release it to the public or for research. So, many modern network datasets we might use to train models for network-related tasks are synthetic (artificially generated specifically for publication so no one's privacy is infringed upon). But because they're technically not "real" data, they might not always properly represent real-world network data flow. Models trained on these datasets may not always perform the way we want.

Also, because industry standard machine learning models like neural networks (and even some non-deep learning models like random forests and gradient boosting) are what we call [*black-box models*](https://umdearborn.edu/news/ais-mysterious-black-box-problem-explained), we can't directly access the model's logic to make sure it's basing its decisions on the correct features (characteristics of the data point).

Thus, TRUSTEE, or TRUSt-oriented decision TreE Extraction comes into play. TRUSTEE was developed by Arthur Selle Jacobs and Roman Beltiukov (and others listed in the paper)... todo

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ersp/poster.png" title="sample screenshot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

You can view our final research poster in greater resolution [here](https://docs.google.com/presentation/d/1V1tX5XgU97CPWW8AC1FKUjQi0PnCE7a0baB7sWcHmwM/edit?usp=sharing). I recently got a new laptop and no longer have access to the server on which much of my code is stored. Once I go home and open that laptop, I will transfer more code over. 

TODO: add my code to repo and link, add proper citation below, maybe add some other research materials used