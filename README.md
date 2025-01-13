# Portfolio-Optimization-Bloomberg-Trading-Challenge
Initial strategy and code developed for the 2024 Bloomberg Global Trading Challenge to optimize our portfolio of selected stocks

Rapport stratégie – Bloomberg Challenge
Dans le cadre du Bloomberg Trading Challenge, nous visons à maximiser la performance de notre portefeuille tout en minimisant les risques liés aux fluctuations du marché. Notre stratégie repose sur deux approches principales : la stratégie de Constant Proportion Portfolio Insurance (CPPI) et une méthode de réplication d'indice pour le volet risqué. Cette combinaison nous permet de diversifier notre portefeuille et d’équilibrer l’exposition aux actifs risqués, tout en capitalisant sur la performance globale du marché à travers la réplication d'un indice de référence du S&P 500.
Stratégie d'allocation :
1. Réplication d'indice
Nous avons alloué 300 000 dollars à une stratégie de réplication d'indice, en choisissant spécifiquement de suivre la performance du S&P 500. Cette approche nous permet de diversifier notre portefeuille tout en capturant la performance de l'une des références les plus importantes des marchés financiers américains.
Pourquoi le S&P 500 ?
Le S&P 500 est un indice diversifié qui représente environ 80 % de la capitalisation boursière totale du marché américain, composé des 500 plus grandes entreprises cotées. Il offre une exposition équilibrée à plusieurs secteurs, tels que la technologie de l'information, la santé et les services financiers, ce qui nous permet de bénéficier d’une croissance robuste tout en limitant le risque. En investissant dans cet indice, nous évitons la gestion active des titres individuels et maximisons notre potentiel de rendement à long terme.
Répartition sectorielle
Nous avons divisé notre investissement en fonction des pondérations sectorielles du S&P 500. Voici les principales allocations :
Secteur 	Pourcentage (%) 
Technologie de l'information 	28% 
Santé 	13% 
Consommation discrétionnaire 	10.5% 
Services financiers 	11% 
Industrie 	8.5% 
Consommation de base 	7% 
Services de communication 	9% 
Énergie 	4.5% 
Matériaux 	2.5% 
Services publics 	3% 
Immobilier 	3% 

Pour chaque secteur, nous avons identifié les trois actions les plus représentatives pour y allouer les fonds.

2. Stratégie CPPI (Constant Proportion Portfolio Insurance)
Dans notre stratégie CPPI, nous avons utilisé un modèle en Python qui nous permet de répartir les actifs entre actifs risqués et non risqués, tout en optimisant le rendement global. L’objectif principal du CPPI est de garantir un certain niveau de protection du capital tout en maximisant l’exposition aux actifs risqués lorsque le marché est favorable. Voici comment nous avons implémenté cela dans le code.
a) Collecte des données et volatilité
Le code commence par collecter des données sur les actions sélectionnées à partir de Yahoo Finance (via la bibliothèque yfinance). Pour chaque action, nous avons calculé la volatilité normalisée sur une année en tenant compte des prix hauts et bas, puis en divisant cette variation par le prix moyen. Cela permet d’obtenir un indicateur du niveau de risque lié à chaque titre. Cette étape est cruciale pour sélectionner les actions à inclure dans le portefeuille risqué en fonction de leur volatilité. 
b) Répartition du portefeuille risqué
Le code sélectionne des actions provenant de divers secteurs comme la technologie, la santé, la défense, ou encore l’énergie. Pour chaque secteur, nous avons choisi des actions en fonction de leur potentiel de rendement et de volatilité. Le modèle attribue ensuite une part du capital à chaque action en fonction de cette volatilité.
La répartition des actifs risqués est optimisée de la manière suivante :
•	Les actifs plus volatils obtiennent une allocation moindre, car ils comportent un risque plus élevé.
•	Les secteurs plus stables reçoivent une allocation plus importante, car ils sont considérés comme des actifs moins volatils.
Le code utilise des méthodes d’optimisation Monte Carlo pour tester plusieurs allocations différentes d’actifs risqués. Cela permet de déterminer la combinaison optimale entre les actifs tout en maximisant le rendement pour un niveau de risque donné.
c) Calcul du ratio de Sharpe
Dans cette étape, le code simule plusieurs portefeuilles avec des allocations différentes d'actifs et calcule le ratio de Sharpe pour chaque portefeuille. Le ratio de Sharpe est un indicateur de la performance ajustée au risque, il mesure combien de rendement supplémentaire on obtient pour chaque unité de risque qu’on prend.
Le code génère aléatoirement des combinaisons de poids pour les actifs risqués, calcule les rendements annuels attendus pour chaque portefeuille, ainsi que le risque (l'écart-type de la volatilité). Le Sharpe Ratio est ensuite utilisé pour sélectionner le portefeuille qui offre le meilleur compromis entre rendement et risque.
d) Gestion dynamique des risques avec le floor à 560 000 
Le floor est un élément central de la stratégie CPPI, et dans notre modèle, il est défini à 560 000 dollars. Si la valeur totale du portefeuille descend en dessous de ce seuil, le modèle réduit l'exposition aux actifs risqués pour protéger le capital : si le portefeuille risque de perdre trop de valeur, la répartition des actifs risqués est ajustée pour investir davantage dans des actifs non risqués.
Le code réévalue la situation du portefeuille régulièrement (deux fois par semaine dans notre cas) et ajuste automatiquement l’allocation pour garantir que le floor de 560 000 $ soit maintenu. Cela protège le capital tout en nous permettant de maximiser l’exposition aux actifs risqués lorsque le marché est favorable.
