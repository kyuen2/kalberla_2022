# Our official response to Kalberla et.al (2022)

Author: Ka Ho Yuen (UW Madison, kyuen2@wisc.edu), Ka Wai Ho (UW Madison, kho33@wisc.edu)

Our official response to the recent publication Kalberla et.al (2022, P. M. W. Kalberla, J. Kerp, U. Haud, DOI: https://doi.org/10.1051/0004-6361/202142250). Step-by-step code and tutorial included. For formal response, see A&A ... / arXiv ...

## TL;DR? 

We suggest the authors of Kalberla et.al (2022) to **perform an internal code check before publishing an article claiming something is wrong.**

## What is this github page about?

Recently Kalberla et. al (2022) wrote an interesting article (arXiv: https://arxiv.org/pdf/2202.01610.pdf) commenting on our previous publication (Velocity Decomposition Algorithm, Yuen et.al, 2021, ApJ, 910, 2, 161) claiming that our technique and also our prior simulations are not compatible to realistic neutral hydrogen (HI) observations. However, upon investigation, we discovered that Kalberla et.al (2022) made a very simple programmatic mistake, by typing (in julia code)
```julia
p_v = p - (mean(p.*I).-mean(p)*mean(I)).*(I.-mean(I))./std(I)^2
```

to something that we reserve engineered (See A&A ...)
```julia
p_v = p - (mean(p).-mean(p)*mean(I)).*(I.-mean(I))./std(I)^2
```

Notice that the second term changes from `mean(p.*I)` to `mean(p)`. This programmatic mistake that we found will invalidate their _whole_ paper, including 14 out of 15 of their figures, all discussions starting from Sec 1 to 7, 9, and also the claims that they made to us. We found that the publicity of our computational process would facilitate the general scientific community to understand why we can recognize their mistakes so easily _without even access their codes_.

## What is Velocity Decomposition Algorithm?

Velocity Decomposition Algorithm (VDA) is an innovative algorithm (see github: kyuen2/LazDDA.jl) in retrieving the "velocity casutics" in observations. Velocity caustics is an imprint of MHD turbulence velocity motions left in the velocity channel space. The caustics will appear even when the astrophysical plasma has no density perturbations (i.e. incompressible fluid). We include a number of examples illustating the power of the VDA for different kinds of media.

## So what does this github page contains?

Here we provide a streamlined `Julia` template for anyone who has access of the page to replicate our results. We will also provide comments step by step to make sure the readers can understand each step.

