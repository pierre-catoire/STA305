---
output:
  pdf_document: default
  html_document: default
---
## Description analytique du modèle

### Lois du modèle

$$
\mu \sim \mathcal{N}(0,4) \\
\sigma^2 \sim \mathcal{U}(0,4) \\
\theta_i \sim \mathcal{N}(\mu,\sigma^2) \\
Y_i \sim \mathcal{N}(\theta_i,\sigma_i^2)
$$

On cherche à obtenir $\mathbb{P}(\mu|\theta)$. On a par le théorème de Bayes :

$$
\mathbb{P}(\mu,\theta|Y) = \frac{\mathbb{P}(\mu)}{\mathbb{P}(Y)}\mathbb{P}(\mu,\theta|Y)
$$

En intégrant sur $\theta$ on obtient la quantité recherchée :

$$
\mathbb{P}(\mu|Y) = \int^\Theta \mathbb{P}(\mu,\theta|Y) d\theta= \int^\Theta \frac{\mathbb{P}(\mu,\theta)}{\mathbb{P}(Y)}\mathbb{P}(Y|\mu,\theta) d\theta
$$

On décompose le problème pour retrouver les trois quantités $\mathbb{P}(\mu,\theta|Y)$, $\mathbb{P}(\mu,\theta)$ et $\mathbb{P}(Y)$ :

Pour $\mathbb{P}(Y|\mu,\theta)$ :

$$
\mathbb{P}(Y|\mu,\theta) = \overset{k}{\underset{i=1}{\prod}}\Bigg[\frac{1}{\sqrt{2\pi\sigma_i^2}}e^{-\frac{1}{2 \sigma_i^2}(Y_i-\theta_i)^2}\Bigg]
$$

Pour $\mathbb{P}(\mu,\theta)$ :

$$
\mathbb{P}(\mu,\theta) = \int_0^4\mathbb{P}(\mu,\theta,\sigma^2)d\sigma^2 = 
\int_0^4
\mathbb{P}(\theta|\mu,\sigma^2) \mathbb{P}(\mu,\sigma^2)
d\sigma^2 \\
= \int_0^4
\mathbb{P}(\theta|\mu,\sigma^2) \mathbb{P}(\mu)\mathbb{P}(\sigma^2)
d\sigma^2
$$

$$
= \mathbb{P}(\mu) \int_0^4
\mathbb{P}(\theta|\mu,\sigma^2) \mathbb{P}(\sigma^2)
d\sigma^2$$

$$
= \mathbb{P}(\mu) \int_0^4
\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{1}{2 \sigma^2}(\theta_i-\mu)^2}
\frac{1}{4}\mathbb{1}_{\sigma^2 \in [0;4]}
d\sigma^2
$$


Pour $\mathbb{P}(Y)$ :

$$
\mathbb{P}(Y,\theta,\mu,\sigma^2) = \mathbb{P}(Y|\theta,\mu,\sigma^2)
\times \mathbb{P}(\theta|\mu,\sigma^2)
\times \mathbb{P}(\mu,\sigma^2) \\
=\mathbb{P}(Y|\theta)
\times \mathbb{P}(\theta|\mu,\sigma^2)
\times \mathbb{P}(\mu)\times\mathbb{P}(\sigma^2)
$$

On a donc :

$$
\mathbb{P}(Y) = \int^\Theta \int^\mu \int_0^4 \mathbb{P}(Y,\theta,\mu,\sigma^2) d\theta d\mu d\sigma^2 \\
= \int^\Theta \int^\mu \int^{\sigma^2} \mathbb{P}(Y|\theta)
\times \mathbb{P}(\theta|\mu,\sigma^2)
\times \mathbb{P}(\mu)\times\mathbb{P}(\sigma^2) d\theta d\mu d\sigma^2 
$$

Au total :

$$
\mathbb{P}(\mu|\theta) =
\int^\Theta \frac{
\mathbb{P}(\mu) \int_0^4
\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{1}{2 \sigma^2}(\theta_i-\mu)^2}
\frac{1}{4}\mathbb{1}_{\sigma^2 \in [0;4]}
d\sigma^2
}
{\int^\Theta \int^\mu \int^{\sigma^2} \mathbb{P}(Y|\theta)
\times \mathbb{P}(\theta|\mu,\sigma^2)
\times \mathbb{P}(\mu)\times\mathbb{P}(\sigma^2) d\theta d\mu d\sigma^2 }
\overset{k}{\underset{i=1}{\prod}}\Bigg[\frac{1}{\sqrt{2\pi\sigma_i^2}}e^{-\frac{1}{2 \sigma_i^2}(Y_i-\theta_i)^2}\Bigg] d\theta
$$

