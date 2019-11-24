# CUE
- derive the bias variance decomposition
- what are the three parts of the decomposition?
- How bias and variance relates to under and over fitting?
- What do training and testing error reflex?
- what would be the effect of adding a good or bad feature on bias and variance?
# Bias variance decomposition
$$
\begin{array}{c}{\mathbb{E}[Y]=\mathbb{E}[f(\mathbf{x})+Z]=f(\mathbf{x})+\mathbb{E}[Z]=f(\mathbf{x})} \\ {\operatorname{Var}(Y)=\operatorname{Var}(f(\mathbf{x})+Z)=\operatorname{Var}(Z)}\end{array}
$$

$$
\begin{aligned} \varepsilon(\mathbf{x} ; h) &=\mathbb{E}\left[(h(\mathbf{x} ; \mathcal{D})-Y)^{2}\right]=\mathbb{E}\left[h(\mathbf{x} ; \mathcal{D})^{2}\right]+\mathbb{E}\left[Y^{2}\right]-2 \mathbb{E}[h(\mathbf{x} ; \mathcal{D}) \cdot Y] \\ &=\left(\operatorname{Var}(h(\mathbf{x} ; \mathcal{D}))+\mathbb{E}[h(\mathbf{x} ; \mathcal{D})]^{2}\right)+\left(\operatorname{Var}(Y)+\mathbb{E}[Y]^{2}\right)-2 \mathbb{E}[h(\mathbf{x} ; \mathcal{D})] \cdot \mathbb{E}[Y] \\ &=\left(\mathbb{E}[h(\mathbf{x} ; \mathcal{D}))^{2}-2 \mathbb{E}[h(\mathbf{x} ; \mathcal{D})] \cdot \mathbb{E}[Y]+\mathbb{E}[Y]^{2}\right)+\operatorname{Var}(h(\mathbf{x} ; \mathcal{D}))+\operatorname{Var}(Y) \\ &=(\mathbb{E}[h(\mathbf{x} ; \mathcal{D})]-\mathbb{E}[Y])^{2}+\operatorname{Var}(h(\mathbf{x} ; \mathcal{D}))+\operatorname{Var}(Y) \\ &=\underbrace{(\mathbb{E}[h(\mathbf{x} ; \mathcal{D})]-f(\mathbf{x}))^{2}}_{\text {bias2 of method }}+\underbrace{\operatorname{Var}(h(\mathbf{x} ; \mathcal{D}))}_{\text{variance of the method}}+\underbrace{\operatorname{Var}(Z)}_{\text {irreducible error }} \end{aligned}
$$

**Or, we can derive this with following**
$$
\mathbb{E}\left[(Z-Y)^{2}\right]=\mathbb{E}\left[((Z-\mathbb{E}[Z])+(\mathbb{E}[Z]-Y))^{2}\right]
$$

## Explaination
- Bias$^2$ of method: Measures how well the average hypothesis (over all possible training sets)
can come close to the true underlying value f(x), for a fixed value of x. A low bias means
that on average the regressor h(x) accurately estimates f(x).
- Variance of method: Measures the variance of the hypothesis (over all possible training
sets), for a fixed value of x. A low variance means that the prediction does not change much
as the training set varies. An un-biased method (bias = 0) could have a large variance.
- Irreducible error: This is the error in our model that we cannot control or eliminate, because
it is due to errors inherent in our noisy observation Y .


# Take aways
- Underfitting is equivalent to high bias; most overfitting correlates to high variance.
- Training error reflects bias but not variance. Test error reflects both. In practice, if the training
error is much smaller than the test error, then there is overfitting.
- Adding good features will decrease the bias, but adding a bad feature rarely increase the bias.
- Adding a feature usually increase the variance, so a feature should only be added if it decreases bias more than it increases variance.

