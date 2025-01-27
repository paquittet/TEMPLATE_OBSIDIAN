---
aliases:
 - individual fitness and measures of univariate selection
 - lecture 12
authors: Walsh
year: 2018
---

## **Individual fitness and measures of univariate selection**

**Goal** : Mesure comment la sélection agit sur un trait phénotypique (sélection phénotypique) 

**2 composantes majeurs** :
* Mesure de la fitness individuelle
* Mesure la relation entre le phénotype et la fitness: $W(z)$


<br>
<br>

### A. Episodes de sélection
#### Composantes de fitness
On distingue la [[viability selection]] de la [[fertility selection]]. Des tradeoffs peuvent émerger lorsque le phénotype est avantageux dans un épisode donné et pas dans un autre. Ces différentes peuvent être liées aux conditions environnementales, mais aussi à l'histoire de vie notamment via des intérêts différentiés au cours du développement.  

Des tradeoffs entre sélection naturelle et sélection sexuelle peuvent aussi exister. La sélection sexuelle résulte de la variance dans le succès reproducteur des mâles liés à la compétition intra-sexuelle et/ou du choix de la femelle de mâles en particulier, alors que la sélection naturelle résulte de dans tous les autres composants de la fitness (viabilité, fertilité, comportements parentaux...).

<br>

#### Mesurer les fitness
De façon simplifiée, la fitness total d'un individu est le nombre de descendant qu'il produit au début de la prochaine génération.  

Cependant, il y a quelques considérations à prendre en compte dans le calcul de la fitness, notamment :
* **ne pas croiser les générations** - si on croise les générations (e.g. compter le nombre d'adulte produits à la génération t+1 par les adultes de la génération t), on va mesurer la fitness des adultes de t mais également celles des descendants de t+1 car ils ont subit des épisodes de sélection précoce. Dans un monde parfait, on mesurerait le nombre de [[zygote]] produit par les adultes de t pour mesurer leur contribution au pool génétique à t+1.
* **ne pas ignorer les âges de vie sur lesquels la sélection peut agir** - si on mesure la fitness sur les adultes uniquement, on ignore les épisodes de sélection des life stages précédents ce qui pourrait avoir comme effet une surestimation / sous-estimation de la fitness (e.g. épisode de sélection de viabilité de développement précoce)

Les deux points sont en réalité assez similaire. L'idée est que mesurer la fitness autrement qu'au moment de la formation du zygote résulte dans une représentation erronée de la fitness des individus.

En condition expérimentale, la mesure du LRS est bien développé (revue par Sved, 1989). En revanche, en population naturelle c'est moins le cas et on mesure en général les épisodes de sélection par étape de développement qu'on va ensuite associer multiplicativement : 

$$
LRS = (p(\text{survie}) * (n_{\text{mate}}) * (n_{\text{zygote par mating}}))
$$

Le nombre de partenaire est une mesure de sélection sexuelle alors que la viabilité et la fertilité de la sélection naturelle.

<br>

#### Calculer la fitness
Soit une cohorte de $n$ individus indexés tel que $1 \leq r \leq n$ et suivi sur plusieurs épisodes de sélection. On notera **$W_j(r)$** la mesure de fitness du $j^e$ épisode de sélection du $r^e$ individu (e.g. si mesure de viabilité, alors 0 si mort, 1 si survie).  

On notera la fitness relative $\overline{w}$ de l'individu $r$ :

$$
\overline{w}(r) = \frac{W_j(r)} {\overline{W}_j}
$$
correspondant à la fitness de l'individu $r$ lors de l'épisode de sélection $j$ **relativement** à la fitness de la population au même épisode de sélection.

<br> 


Au début de l'étude, la fréquence des individus est $1/n$ pour le premier épisode **observé** de sélection est simplement la moyenne des fitness individuelles:

$$
	\overline{W}_1 = \frac{1}{n} \sum^n_{r=1} W_1(r)
$$
> [!caution]
> **Avoir en tête** que des épisodes de sélection majeurs ont déjà pu être survenu avant le stade de développement étudié !

Après le premier épisode de sélection, la nouvelle fréquence de fitness relative du $r^e$ individu est $w_1(r)/n$ soit : 

$$
\overline{W}_2 = \sum^n_{r=1} W_2(r) \cdot w_1(r) \cdot (\frac{1}{n})  
$$

Avec : 
- $W_2(r)$ la fitness de l'individu $r$ à l'épisode de sélection 2
- $w_1(r)$ la fitness relative de l'individu $r$ à l'épisode de sélection 1

> [!bug]
> Pas sûr de comprendre ce que représente cette nouvelle pondération $w_1(r) \cdot 1/n$

L'équation générale pour le $j^e$ épisode de sélection est donc :

$$
\overline{W}_j = \sum^n_{r=1} W_j(r) \cdot w_{j-1}(r) \cdot w_{j-2}(r) \dots w_{1}(r) \cdot (\frac{1}{n})
$$

On notera que si un individu a une fitness de 0 à un moment donné, alors les composantes de fitness futur sont égale à 0 (fonctionne pour la sélection de viability mais absolument pas pour le succès reproducteur : **oui mais succès reproducteur est calculé sur la vie entière de l'individu**).



<br>

**Tags**:: 
 - [[viability selection]]
 - [[fertility selection]]
 - [[tradeoff]]
 - [[fitness]]
 - [[relative fitness]]
 - [[selection]]



