# Our official response to Kalberla et.al (2022)

Author: Ka Ho Yuen (UW Madison, kyuen2@wisc.edu), Ka Wai Ho (UW Madison, kho33@wisc.edu)

Our official response to the recent publication Kalberla et.al (2022, P. M. W. Kalberla, J. Kerp, U. Haud, DOI: https://doi.org/10.1051/0004-6361/202142250). Step-by-step code and tutorial included here: https://github.com/kyuen2/kalberla_2022/blob/main/Kalberla_2022_workout.ipynb.  For formal response, see A&A ... / arXiv: https://arxiv.org/abs/2202.07871

## TL;DR? 

We suggest the authors of Kalberla et.al (2022) to **perform an internal code check before publishing an article claiming something is wrong.**

## What is this github page about?

Recently Kalberla et. al (2022) wrote an interesting article (arXiv: https://arxiv.org/pdf/2202.01610.pdf) commenting on our previous publication (Velocity Decomposition Algorithm, Yuen et.al, 2021, ApJ, 910, 2, 161) claiming that our technique and also our prior simulations are not compatible to realistic neutral hydrogen (HI) observations. However, upon investigation, we discovered that Kalberla et.al (2022) very likely made a very simple programmatic mistake, by typing (in julia code)
```julia
p_v = p - (mean(p.*I).-mean(p)*mean(I)).*(I.-mean(I))./std(I)^2
```

to something that they might have done (See A&A ...)
```julia
p_v = p - (mean(p).-mean(p)*mean(I)).*(I.-mean(I))./std(I)^2
```

Notice that the second term changes from `mean(p.*I)` to `mean(p)`. This programmatic mistake [1] that we found will invalidate their _whole_ paper, including 14 out of 15 of their figures, all discussions starting from Sec 1 to 7, 9, and also the claims that they made to us. We found that the publicity of our computational process would facilitate the general scientific community to understand why we can recognize their mistakes so easily _without even accessing their codes_. See `readme` of https://github.com/kyuen2/LazDDA for further examples.


[1]: Notice that our template reproduces very similar results of their mistakes, it can be more.. However, it is not our full responsibility to find out the mistakes in others' publications. Moreover, mathematically <pdpv>=0 no matter what choice of p and I you pick, see https://github.com/kyuen2/LazDDA

## What is Velocity Decomposition Algorithm?

Velocity Decomposition Algorithm (VDA) is an innovative algorithm (see https://github.com/kyuen2/LazDDA) in retrieving the "velocity casutics" in observations. Velocity caustics is an imprint of MHD turbulence velocity motions left in the velocity channel space. The caustics will appear even when the astrophysical plasma has no density perturbations (i.e. incompressible fluid). We include a number of examples illustating the power of the VDA for different kinds of media.

## So what does this github page contains?

Here we provide a streamlined `Julia` template for anyone who has access of the page to replicate our results. We will also provide comments step by step to make sure the readers can understand each step.

  
## `Julia` is too complicated to install, what should I do?
  
I have built a standard environment here (https://hub.docker.com/repository/docker/kyuen2/gsa-hi) which you can upload the template in this repository and reproduce the exact same results. If some standard package is missing, refer to the docker instruction I wrote there.

