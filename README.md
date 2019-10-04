Spatial Explicit Island Community Occupancy Modeling using Markov Random Field Model with Imperfect Observation, Study of Carnivore Community in Apostle Island National Lakeshore
==================================================================================================================================================================================

Introduction
------------

MacArthur and Wilson’s (2001) well known book, *The Theory of Island
Biogeography* ([@macarthur2001theory]), introduced their theoretical and
empirical work on spatial patterns of species richness. Their
equilibrium theory of island biogeography emphasized the importance of
random colonization and extinction in forming species richness patterns
on islands which contributed to Stephen Hubbell’s neutral theory on
community assemblage ([@hubbell2001unified], see [@RN8] for a review).
Before the era of island biography and neutral theory, ecologists were
largely concentrated on the deterministic drivers of community
assemblage using for instance, niche theory
([@hutchinson1957multivariate]), Lotka-Voterra models
[@lotka1910; @volterra1928], etc. In contrast to these essentially
deterministic models, in which presence is a function of niche
optimizing or habitat and interactions between species, island biography
theory and neutral theory emphasized the effect of stochastic
colonization and extinction rates where life-history differences at the
species level are immaterial. Restated, both theories assert that
species are interchangeable, thus we could infer statistical property of
a species pool by studying a “typical” species [@RN40] using mean field
approximation. There remains a debate over the relative contribution of
spatial stochastic processes and life history related processes in
shaping community. Much work has already been done on plant communities
(e.g. Lesky et al. 2017), marine systems (e.g.
[@RN14; @gothe2013; @RN6]), and microbial systems to separate different
processes in both experimental and natural communities (see [@RN11] for
a review). However, neither large mammal communities nor temperate
systems have generated much attention. Reasons may include cryptic life
histories of large mammals and the relative rarity of temperate islands.

It is beneficial to model different processes explicitly to understand
their relative importance([@RN10], [@RN26]). It is common to use
correlations between random variables to model underlying processes. A
general framework for this task is Probabilistic Graph Modeling (PGMs,
[@koller2009PGM]). Markov Random Field modeling (MRF) is a kind of PGM
that defines joint distribution of set of random variables linked by
non-directed graphics which allows cycles ([@RN23; @cressie1992]) . MRF
has long been used to model spatial correlations in different areas of
ecology and agriculture, e.g. in spatial ecology ([@RN29; @RN28]), as
well as temporal analysis (e.g. [@RN22]) and interspecific interactions
(e.g. [@RN27]). It was also widely used for modeling networks in social
(e.g. [@socialnet]), genetic (e.g. [@genenet]), as well as competing
species (e.g. [@RN27]).

Due to a recent flourish of camera-trapping research, we now have
opportunities to get vast amount of detection-nondetection data which
can be used to infer presence-absence (P/A) of certain moderate to
large-sized animals. However, imperfect detection is a problem since
detection-nondetection is not presence-absence
[@kery2008_imperfect_det]. Researchers developed occupancy modeling
([@RN48]) whose main idea is to infer true P/A and detection rates from
repeat sampling. This idea was also explored by computer vision and
image modeling communities earlier than ecologists especially after the
development of the EM (Expectation-Maximization) algorithm which allows
maximum likelihood estimation when the model depends on unobserved
latent variables (e.g. true occupancy [@dempster1977]). MRF with
imperfect observations were also explored in this context
([@chalmond1989], also see [@ibanez2003parameter] for a review in
computer science). We can build various occupancy-like models based on
this main idea, i.e. the view of observations as samples taken from the
detection distribution conditioned on an unobserved latent true pattern
that follows another distribution. These techniques facilitate research
on assembly of animal communities on both island and other landscapes.

Apostle Island National Lakeshore (APIS) is located on the southwest
shore of Lake Superior and lies in the transition zone between temperate
and boreal forest regions. APIS is distinct from tropical islands (where
much research on community assembly has occurred) because of severe
winters and relative low productivity. But despite these challenges,
during surveys conducted by University of Wisconsin Madison and National
Park Services, 10 species of the native carnivore guild were detected
during 2014-2017. How these species coexist and how richness differs
between islands is fundamental for understanding community dynamics in
temperate island systems. In the 10-species pool, red fox (*Vulpes
vulpes*) and coyote (*Canis latrans*), as well as fisher (*Pekania
pennanti*) and marten (*Martes americana*) are pairs of species that
share a similar trophic positions, have similar body sizes, and, hence
show potential for niche overlap but also show different coexistence
patterns. Coyote and red fox show a spatial overlap pattern at the
camera site level while fisher and marten show a partitioning pattern.
By comparing these two pairs of species we may gain insight into the
interplay of deterministic and stochastic process in shaping community
assembly.

In this study, I will attempt to use a binary MRF (a.k.a. Ising model in
physics, [@ising1925]) together with occupancy-like modeling to account
for imperfect detections to assess the relative importance of spatial
and interspecific factors in shaping the spatial distributions of two
pairs of similar carnivores (Fisher-Marten, Coyote-Fox) in APIS. My goal
is to contribute to our understanding of island communities and by
extension, patterns of community assembly.

Study Area
----------

The Apostle Island National Lakeshore (APIS) is located on the
southwestern shore of Lake Superior, on the northern edge of the state
of Wisconsin, USA. It consists of 21 of the 22 islands which make up the
archipelago. Formation of the archipelago dates to the Pleistocene epoch
when the islands were carved out from mainland Wisconsin by glacial
retreat. The archipelago has a long history of logging, quarrying and
residences before the 1970s when it was designated as National
Lakeshore. Madeline island was excluded because it is home to a large
year-round community. During 2014-2017, the University of
Wisconsin-Madison and APIS conducted a camera-trapping survey to
determine distributions and abundance of carnivores in the National
Lakeshore ([@allen2017survey]). During the study period, temperatures
ranged from -30.0to 32.8with average of 4.4 . Annual precipitation
averaged 82.8cm of rain and 197.4cm of snow ([@arguez2010noaa]). Surface
ice during winter likely facilitates movement of animals between
islands. However, ice cover has decreased 3days/year within Bayfield
Harbor in the past 150yr ([@howk2009]) which reveals the possible
vulnerability of the system to climate change.

Target Species and Working Hypothesis
-------------------------------------

Though there are 10 carnivore species detected in APIS, we chose 2 pairs
of species which are in a similar trophic position and have similar body
size, and, hence show potential for niche overlap but show different
coexistence patterns. Coyote and red fox (CF later) show an overlap
while fisher and marten (FM later) show a partition pattern.

For the FM system, I have two working hypothesis for the partition
pattern:

-   Two species have similar island biography pattern, meanwhile, they
    partition the space due to competition.

-   Two species have opposite island biography pattern, i.e. different
    source-sink dynamic, but have minor competition.

For the CF system, I have two working hypothesis for the overlapping
pattern:

-   They have similar island biography pattern. They partition the time
    to achieve coexistence or competition is minor.

-   There is a bottom-up (e.g. prey) or top-down control make two
    species coexist while island biography is relative minor.

Method
------

### Spatial Explicit Community Occupancy Analysis using Markov Random Field Regression Model

I will use the Markov Random Field (MRF) modeling framework to conduct a
spatially explicit analysis of interspecific relationships between MF
and CF systems in the APIS archipeligo. Follow conventions of linear
regressions, denote the design matrix for environmental covariates as
$\mathbf{X}$ and parameters correspond to $\mathbf{X}$ as $\beta$. To
make comparisons between spatial and intersepcific processes in shaping
spatial distributions, two main components will be considered
simultaneously in the graph associated with the MRF: nearest
neighborhood spatial autocorrelation at camera-site level (site level
hereafter) within and among islands and local species associations at
site level. Further, due to the different nature of site linkages within
and across islands, I will model inter-island and intra-island
correlations separately. I denote the strength parameters of these two
correlations as$\eta^{ex}$ and $\eta^{in}$, and graph matrix
$\mathbf{D}^{ex}$, $\mathbf{D}^{in}$ (eqn.\[Ham\]). To make MRF models
more explainable and robust when interactions are strong ([@RN31]), I
will use 1 and -1 to code presence and absence respectively, rather than
convention 0 and 1 coding in occupancy-like modeling. For occupancy or
occupancy like models, I use vector $\mathbf{Z}_k$ to note species k’s
presence-absence at all camera sites, $\mathbf{Z}$ is a vector of all
species’ occupancy and I use w to denote number of species. The
probability of observing a certain pattern is given by: 

$$\label{Ham}
    P(\mathbf{Z}|\theta)\propto exp[ \sum_{k=1}^{w} (\mathbf{X}\beta_{k} \mathbf{Z}_{k} 
    + \frac{1}{2}\eta_{k}^{in}\mathbf{Z}_{k}^{T}\mathbf{D}_{k}^{in}\mathbf{Z}_{k}
    + \frac{1}{2}\eta_{k}^{ex}\mathbf{Z}_{k}^{T}\mathbf{D}_{k}^{ex}\mathbf{Z}_{k}
    + \sum_{l>k}\eta_{lk}\mathbf{Z}_{k}^{T}\mathbf{Z}_{l})]$$

The right hand part of this expression is denoted as $q(\mathbf{Z})$ and
$log(q(\mathbf{Z}))$ is called negative potential function later in the
proposal. Comparing terms’ relative contribution in negative potential
function’s estimation will give us insights onto different processes’
relative contribution on the given landscape. Comparing the relative
strength parameters will give us insights onto relative strength between
different processes. Note that since there is a large number of possible
patterns ($\mathbf{Z}$s), this likelihood function is not tractable due
to the intractable normalizing constant (note as $C(\theta)$ later) so
we need special treatment in taking the posterior samples.

### Mainland-island Model and Stepping Stone Model for Interisland correlation

Trapping sites within islands were designated using a regular lattice
with grids  1km in length making it easy to find nearest neighborhoods.
However among islands, camera sites are not on a regular lattice. Two
island biography models will be attempted and compared via model
selection, 1) a mainland island model and 2) a stepping stone model. In
the mainland island model I assume that there is no relationship between
discrete islands but all sites are linked to mainland whose linkage
strength decays exponentially with normalized distance ([@RN14]) while
in the stepping stone model, I use Veronoi polygons
([@okabe2009Voronoi]) to find nearest neighborhood linkages (a.k.a.
Delaunay trianglization [@okabe2009Voronoi]) between camera sites on the
edges of islands and only those sites whose nearest neighbor is mainland
will be directly connected to mainland Fig.\[Stepping\_stone\]. Also,
the correlation strength was assumed to decay exponentially with
normalized distance.

![Nearest neighborhood used in stepping stone
model[]{data-label="Stepping_stone"}](_figs_/fig/APIS_graph.png)

### Accounting for Imperfect Detection

Following the main idea of occupancy-like modeling ([@RN48]), we can
model the observed detection-nondetection as repeated samples from a
detection distribution. We further assume that the interspecific
interactions are local (i.e. no spatial auto correlations considered). I
will use another binary MRF conditioned on whether the site being
occupied by certain species to model the detection distribution. Only
species occupying a certain site will be included in the MRF and species
not occupying will have probability of non-detection = 1. Formally, I
use $y_{kij}$ to note species $k$’s detection status at site $i$ during
period $j$. The likelihood function at site $i$ and period $j$ is given
by eqn.\[Isingdet\]

$$\label{Isingdet}
    P(y_{1ij},y_{2ij},...|Z_{1i},Z_{2i},...)\propto exp(\sum_{k=1}^{w}[\beta^{det}_{k}X^{det}_{ij}y_{kij}I_{Z_{ki}=1}+\sum_{l> k}(1-\delta_{kl})y_{kij}y_{lij}I_{\mathbf{Z}_{ki}=1}I_{\mathbf{Z}_{li}=1}])$$

which $I_{\{\}}$ is the indicator function and $\delta_{kl}$ is
Kronecker’s $\delta$ function, $=1$ if $k=l$ and $=0$ otherwise. Unlike
the occupancy part, this likelihood function is tractable for small
number of species (with rule of thumb &lt;10). The full (unnormalized)
likelihood function then can be calculated by multiplying eqn.\[Ham\]
and eqn.\[Isingdet\]. Posterior distribution of missing Zs can be
estimated using a fully Bayesian approach as estimating unknown
parameters.

### Bayesian Inference for MRF

Before Moller’s work in 2006, Bayesian inference on MRF models was
precluded because the intractable normalizing constant is a function of
parameters of interest. Moller proposed an auxiliary variable based on
the Metropolis–Hastings ratio ([@RN52]). A further development due to
[@RN79] is called the single parameter change method. In our case, we
follow [@RN79] by sampling an auxiliary variable $X$ to follow the MRF
distribution whose parameters are proposed $\theta'$. Together with
imperfect detection, the Metropolis–Hastings ratio is given by
eqn.\[MH\].

$$\label{MH}
\begin{aligned}
    H(\theta'|\theta)=\frac{\pi(\theta')p(y|Z')q_{\theta'}(Z')q_{\theta}(X)}{\pi(\theta)p(y|Z)q_{\theta}(Z)q_{\theta'}(X)}
\end{aligned}$$

The required perfect sample can be drawn using the Coupling From the
Past algorithm (CFTP [@propp1996cftp]) implemented in `R` and `C++`
modified from `R` package `IsingSampler` [@isingsampler] with help of
`RcppArmadillo` [@RcppArmadillo] and sparse matrix `C++` class provided
by `R` package `Matrix` [@Matrix] to optimized for the sparse graph as I
have (open sourcesed as `R` package `SparseIsingSampler` available on
`GitHub`). Posterior sample of $\mathbf{Z}$ will also be taken in this
process. Diagnoses of the MH algorithm will be done in `R` package
`coda` [@CODA].



### Model Selection

Bayes Factor (BF), a Bayesian generalization of Likelihood ratio test,
will be used for model selection ([@gelman2013]). One obstacle to using
BF in this model is the intractable likelihood function. But following
[@descombes1999], formally, by taking sample $\mathbf{Y}$ from parameter
setting $\phi$, the ratio of normalizing constant $C(\theta)$ and
$C(\phi)$ can be calculated as expectation:
$Eq_{\theta-\phi}(\mathbf{Y})$. We can calculate log likelihood added by
$-log(C(\phi))$ which is intractable. However, by choosing the same
$\phi$ for two competing models, we can calculate BF of two models by
canceling out the intractable constant induced by $\phi$. Since the
ratio is also estimated, robustness diagnostics following
[@descombes1999] will be conducted.

### Test of working hypothesis

For FM, if hypothesis 1 is true, we should be able to detect a
significant negative interspecific coefficient ($\eta_{FM}$
competition). Inter-island spatial autocorrelation coefficient should
have same sign for two species ($\eta^{ex}$, similar mainland-island or
stepping stone pattern). If hypothesis 2 is true, we may not be able to
detect a significant negative interspecific coefficient, and
inter-island spatial autocorrelation coefficients should have different
signs for two species. For CF, if hypothesis 1 is true, we should be
able to detect a significant negative interspecific coefficient in
detection but not in occupancy. Inter-island spatial autocorrelation
coefficients should have same sign for both species ($\eta^{ex}$),
similar mainland-island or stepping stone pattern). If hypothesis 2 is
true, we should be able to detect a significant positive interspecific
coefficient in occupancy and inter-island spatial autocorrelation
coefficients should have same or different signs for both species.

Further analysis of the contributions of different processes will be
done by analyzing different terms in the negative potential function.

Preliminary Results
-------------------

### FM System, Selection between Mainland-Island and Stepping Stone

I calculated the BF between Mainland-Island model and Stepping Stone
models for spatial correlations. The log10BF between these two is
61.9&gt;2, hence data decisively supports Mainland-Island rather than
the Stepping Stone model ([@kass1995]). Thus further analysis will be
based on the Mainland-Island model.

### FM under Mainland-Island Model

I failed to detect a significant association between fisher and marten
in either occupancy or detection (p=0.248, p=0.596 respectively). The
mainland-island association has different sign in fisher (mean=2.78,
sd=0.88, p=0.00) and marten (mean= -0.70, sd=0.40,p=0.011). This result
suggests the second working hypothesis. Additionally, during the camera
trapping survey on mainland, we failed to detect marten for () camera
days and () camera sites. Marten may be a special case where the island
serves as source rather than sink of the population in mainland-island
process. For intra-island spatial auto-correlation, I detected a
significant positive value in marten (posterior mean=0.30,sd=0.085,
p=0.00075) but no significance for fisher (mean=0.085,sd=0.16,p=0.434)
fig.\[FM\_para\].

![Posterior parameter estimation of FM system, mainland-island
system[]{data-label="FM_para"}](_figs_/fig/APIS/FM/parameters_MI.jpg)

I used the negative potential function to evaluate the contribution of
different term in the observed pattern, in which the mainland-island
term for fisher contributes the most while marten’s intra-island and
mainland-island also contributed fig.\[FM\_Ham\].

![Contribution of different terms of FM, mainland-island
system[]{data-label="FM_Ham"}](_figs_/fig/APIS/FM/FM_postH_mainland.jpg)

### CF under Mainland-Island Model

I detected a significant positive association in both occupancy
(0.55,p=0.0052) and detection (0.41,p=0.000) between coyote and fox,
while mainland-island strength had the same sign but was not significant
for coyote (coyote 0.25, p=0.23 fox 1.33, p=0.0000). This suggests the
second working hypothesis of the overlapping pattern observed in CF
system. Intra island spatial autocorrelation is not significant for both
coyote and fox (p=0.1246, 0.4140 respectively) fig.\[CF\_para\].

![Posterior parameter estimation of CF system, mainland-island
system[]{data-label="CF_para"}](_figs_/fig/APIS/CFB/CF_parameter_MI_50K.jpg)

Initial Discussion
------------------

### Contrasting FM and CF Systems

Different patterns were observed in these two pairs of similar species.
The CF system shows more positive inter-specific association in both
longer and shorter time scale (i.e. occupancy and detection). This
finding may be related to diet and finer time scale relationships.

FM system provides a possible example that mainland serves as sink
rather than source for a species in a meta population point of view.
This is a counter example for IBT’s assumption that species are
immigrants from the mainland. A more general meta-community framework
should be used in considering island or island-like systems.

Comparison of these two systems provides an example that even for
species with similar natural history, relationship between them can have
large differences in the same island landscape. Large differences in
interspecific relationships suggests a difficulty in studying patterns
in the species pool as an outcome of the probablistic “typical species”
as assumed in IBT and neutral theory. When number of species is small
enough, detailed study of the network should be conducted to understand
the whole system after studying the statistical property of richness.

Next step
---------

In the analysis above, I include intra-island spatial correlation which
may or may not be necessary for the pattern observed. It is necessary to
do model selection on it. A Stepping stone model for the CF system needs
to be evaluated and evaluated relative to the mainland-island model.
Other species observation in the data set should be evaluated to
reconstruct network from a larger species pool.
