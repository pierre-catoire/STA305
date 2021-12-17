# Méta-analyse bayésienne de l'efficacité de l'hydroxychloroquine dans le COVID-19 : STA305 🎓

*Auteurs : Fourmond M, Mukakalisa C, Catoire P*

## 🥇 Objectif

<p align="center">
  <b>
Evaluer par une approche bayésienne l'effet de l'hydroxychloroquine sur le risque de décès parmi les patients atteints de COVID-19, à partir des données de Axfors et al. 💊[1]
  </b>
</p>

## 🏥 Données

Sont extrait de l'article initial les résultats de 34 études, publiées ou en cours au moment de la rédaction de l'article. Pour chaque étude, les variables d'intérêt recueillies sont :

- Nombre de sujets décédés dans le groupe traitement
- Nombre total de sujets dans le groupe traitement
- Nombre de sujets décédés dans le groupe traitement
- Nombre total de sujets dans le groupe traitement
- Dose d'hydroxychloroquine dans le protocole : haute dose vs. faible dose
- Statut de la publication :
  - AP : étude portant sur l'hydroxychloroquine, publiée
  - ANP : étude portant sur l'hydroxychloroquine, non publiée
  - B : étude portant sur la chloroquine
 
## 🧮 Analyse 

### 📘 Modèle :

Le modèle bayésien est défini par :

- **quantité d'intérêt** : OR ($\mu$) du risque de décès entre les groupe HCQ et contrôle
- **Modèle d'échantillonnage** :
  - $Y_i \sim \mathcal{N}(\theta_i,\sigma_i^2)$ avec : $Y_i$ le log-OR observé de l'étude $i$, $\sigma_i^2$ la variance de l'estimation du log-OR de l'étude $i$ (considéré comme une valeur fixe et non une variable aléatoire dans notre modèle)
  - $\theta_i \sim \mathcal{N}(\mu,\sigma^2)$ avec $\sigma$ la variance interétude
- **Priors** :
  - $\mu \sim \mathcal{N}(0,4)$
  - $\sigma^2 \sim 

### 🎯 Mesures d'intérêt :

- Médiane a posteriori
- Intervalle de crédibilité à 95% par la méthode de plus haute densité
- p-direction pour OR < 1 et OR < 0.9

### 🛠️ Stratégie d'analyse :

- Calcul de l'OR observé pour chaque étude
- Estimation d'un modèle naïf pour définition de `burnin`, `thin` et `n.iter`
- Estimation du modèle global
- Analyse en sous-groupes :
  - Etudes publiées vs. non publiées
  - Forte dose vs. faible dose
- Analyse de sensibilité
  - Paramètres des distributions a priori
  - Choix de la distribution a priori du paramètre de dispersion interétude $\sigma^2$ : uniforme vs. beta inverse
- Discussion

### 🖥️ Packages 

- RJags
- HDInterval
- coda
- metafor
