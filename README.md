Présenté par :

**Papa Samba Thiam**

**Jean Marc Kouadio Dongo**

**Yves-Simon Djomatchoua**

**Michael Ebenezer Lekana Bitsindou**

**Steven Otcho Akoti**

**Table des matières** 

1. **Pré-traitement**
    
    a) Démographie
    
    b) Education
    
    c) Génération de données d’éducation
    
    d) Revenue
    
2. **Election**
    
    a) Fusion des datasets
    
    b) Visualisation et Analyse
    
    c) Corrélation entre les données démographiques et économiques
    
3. **Vecteurs et Labélisation**
4. **Nettoyage de la dataset**
    - Analyse en Composantes Principales (PCA)
5. **Modèle de prédictions**
    
    a) Rééquilibrage de la Dataset
    
    b) Modèle de prédiction
    
6. **Résultats**
7. **Comparaison**

Cela résume les principales sections et sous-sections du rapport sur la prédiction des élections. Vous pouvez l'utiliser pour naviguer plus facilement dans le document.

1. **Source des datasets** 

**Introduction**

Dans ce rapport, nous présentons les résultats d'une étude exhaustive réalisée par **DataElect Analytics**, une entreprise spécialisée dans l'analyse prédictive des données électorales. Fondée en 2015, DataElect Analytics se distingue par son expertise dans l'application des technologies de machine learning et de big data pour prédire les issues des élections à différents niveaux administratifs. 

Le projet décrit dans ce rapport a été initié avec l'objectif de développer un modèle capable de prédire les résultats des élections présidentielles en France, en se basant sur une série de facteurs démographiques, économiques, et éducatifs. En exploitant des ensembles de données étendus couvrant plusieurs cycles électoraux, notre équipe a appliqué des méthodes avancées de traitement de données et de modélisation prédictive pour construire et valider un outil de prédiction robuste.

1. **Pré-traitement** 
    
     **a) Démographie**
    

Après avoir chargé le jeu de données, nous avons entrepris l’étape de la sélection des colonnes pertinentes, notamment celles qui font référence aux dates des élections. Ensuite, nous avons remodelé la structure de la dataframe pour créer une version plus manipulable. Cette démarche nous a permis de créer une nouvelle dataset comportant les colonnes suivantes :

- "Libellé de la commune" : Cette colonne renferme les noms des communes de France, offrant ainsi un contexte géographique crucial pour notre étude.
- "Population" : Cette colonne contient le nombre d'habitants par commune, une information fondamentale pour comprendre les dynamiques démographiques et électorales.
- "Date" : Cette colonne indique l'année de référence des données de la dataframe, fournissant un repère temporel pour nos analyses et interprétations. Nous avions donc les données des années 2007, 2012, 2017.

En consolidant ces informations essentielles dans une structure de données épurée, nous avons simplifié notre processus d'analyse et mis en évidence les éléments clés nécessaires à notre étude sur les élections et leur corrélation avec la population des communes en France.

**b) Éducation**

Notre jeu de données initial concernait les taux de réussite à l'échelle nationale pour chaque année. Cependant, pour nos observations à l'échelle des communes, il était impératif de disposer de données réparties sur l'ensemble du territoire

Ainsi, nous avons entrepris une démarche visant à agréger ces données nationales à l'échelle communale, afin d'obtenir une vision plus granulaire et représentative de la situation éducative dans chaque commune. Cette approche nous permettra de mieux appréhender les corrélations potentielles entre les résultats électoraux et le niveau d'éducation au sein des différentes communautés. 

**c) Génération de données d’éducation**

En supposant que les taux de réussite aux différents baccalauréats (bac technologique, bac professionnel et bac général) suivent une distribution normale, nous avons élaboré une approche pour intégrer ces données dans notre analyse.

- Nous avons d'abord établi une fonction nommée "generate_normal_samples", prenant en paramètres la moyenne et l'écart-type d'une distribution normale, ainsi que la taille désirée de l'échantillon. Cette fonction a pour but de générer des échantillons conformes à une distribution normale.
- Pour attribuer les taux de réussite aux différents types de baccalauréat en fonction du nombre d'habitants dans chaque commune, nous avons élaboré un tableau contenant les poids associés à chaque commune. Ces poids servent de facteurs permettant d'ajuster de manière raisonnable les taux de réussite en fonction de la population de chaque commune.
- Enfin, nous avons généré les échantillons de taux de réussite pour chaque commune, en nous basant sur le type de baccalauréat, et les avons pondérés en fonction de leurs poids respectifs. Ces taux générés ont ensuite été intégrés dans la dataset "Niveau_education", enrichissant ainsi notre analyse avec des données éducatives spécifiques à chaque commune.
    
    
    **d) Revenue** 
    

Dans le cadre du traitement des datasets concernant les revenus des foyers des différentes communes, nous avons initié notre démarche en effectuant une visualisation des données manquantes. Il est apparu que les cinq premières colonnes présentaient le moins d'éléments manquants. Afin d'éviter toute approximation à une échelle trop grande, risquant de biaiser notre étude, nous avons choisi de nous limiter à sélectionner les cinq premières colonnes de chaque dataset. Ensuite, pour chacune de ces cinq colonnes, nous avons identifié les valeurs manquantes que nous sommes remplacées par la médiane.
Pourquoi avons-nous opté pour la médiane comme substitut ? La médiane est préférable dans ce contexte car elle est moins sensible aux valeurs extrêmes ou aberrantes par rapport à la moyenne. En utilisant la médiane comme valeur de remplacement, nous préservons la distribution centrale des données et réduisons ainsi le risque de distorsion dans notre analyse causée par des valeurs atypiques.

Voici donc la colonne finale présente dans :

**'CODGEO' :** le code associer a chaque commune

**'NBMENFISC' :** Nombre de ménages fiscaux

**'NBPERSMENFISC12' :** Nombre de personnes dans les ménages fiscaux

**'MED' :** Médiane du niveau de vie (€)

**2. Élection**

Nous avons consolidé les résultats des élections par candidat et par commune, en rassemblant des données telles que le nombre de voix recueillies, les bulletins nuls, etc. Cette consolidation a été réalisée en fusionnant toutes ces datasets en une seule, qui contient l'ensemble des communes ainsi que les performances de chaque candidat politique.

**a) Fusion des datasets**

Après avoir effectué le traitement préalable de chaque dataset, nous entamons la fusion. Cette opération se fonde sur le nom de la commune, contenu dans la colonne "Libellé de la commune", tout en tenant compte de la date à laquelle chaque donnée est affiliée.

**b) Visualisation et Analyse**

- Visualisation

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/517f4bc9-b09f-4550-b2a0-cc38628defbf/cec8900d-8fab-4634-bce6-87136298b3c8/Untitled.png)

> Figure 1 : Niveau de réussite au Baccalauréat par commune & par type de BAC.
> 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/517f4bc9-b09f-4550-b2a0-cc38628defbf/c5d581a3-ad2d-429f-b446-4e6620eab69f/b4c06abc-d24e-440f-8e4a-f321fcb1af08.png)

> Figure 2 : Répartition des voix au sein des 5 communes les plus peuplés
> 

**c) Corrélation entre les données démographiques et économiques.**

En 2012, lors des élections dans les communes de Lyon et de Nice, on observe sur le diagramme circulaire une grande part de voix (28%) pour François Hollande, comparativement à 26,9% pour Sarkozy. Cependant, lorsque l'on se réfère à la commune de Nice, nous constatons l'effet contraire avec une majorité de voix pour Sarkozy (33,7%) contre 22,4% pour Hollande. Plusieurs facteurs puissent expliquer ce revers de situation entre Lyon et Nice lors des élections de 2012.

Premièrement, prenons en compte le niveau d'éducation et les revenus médians par foyer dans ces deux villes. À Lyon, où le revenu médian par foyer est estimé à 21 669 euros, il est possible que la population ait un niveau d'éducation et des revenus salariaux plus élevés en moyenne. En revanche, à Nice, où le revenu médian par foyer est de 18 683 euros, la situation semble moins favorable sur le plan économique.

Ensuite, regardons les préférences politiques associées à ces niveaux socio-économiques. Il est plausible que dans des régions avec un niveau d'éducation et des revenus salariaux plus élevés, les électeurs aient tendance à favoriser des candidats comme Nicolas Sarkozy, dont le parti est perçu comme représentant davantage les intérêts des classes aisées.

D'autre part, les populations à revenu moyen pourraient être plus enclines à soutenir des candidats comme François Hollande, dont le parti est souvent associé à des politiques sociales et économiques visant à soutenir les classes moyennes.
En somme, ces différences socio-économiques entre Lyon et Nice pourraient expliquer en partie le vote en faveur de Nicolas Sarkozy à Nice et de François Hollande à Lyon lors des élections de 2012. Cependant, d'autres facteurs tels que les dynamiques locales et les enjeux politiques spécifiques de chaque région pourraient également avoir joué un rôle dans ce schéma de vote.

1. **Vecteurs et Labellisation**

Dans notre dataset fusionné, nous avons ajouté une colonne appelée "label" qui contient la valeur 1 lorsque le candidat obtient le nombre de voix maximal au sein d'une commune donnée, et 0 pour les autres candidats. Cela permet d'identifier facilement le candidat victorieux dans chaque commune. Pour chaque ligne de données, nous avons associé les éléments suivants comme vecteurs de base : le nombre de personnes inscrites par tour, les données sur les revenus salariaux moyens dans la commune, le rendement scolaire au baccalauréat (taux de réussite), le parti politique du candidat, le nom et prénom du candidat, et le nom de la commune.
Ces vecteurs de base nous permettent de construire un modèle riche et pertinent pour analyser et prédire les résultats électoraux en fonction de divers facteurs socio-économiques et éducatifs, ainsi que de l'affiliation politique et des caractéristiques individuelles des candidats. Cette approche nous offre une vue d'ensemble détaillée et contextualisée des dynamiques électorales à travers différentes communes.

1. **Nettoyage de la dataset**

Après avoir fusionné toutes les datasets, nous avons obtenu une dataset générale contenant 30 colonnes. La question est de savoir si toutes ces 30 colonnes sont nécessaires pour prédire le résultat. Pour répondre à cette question et simplifier le modèle, nous pouvons utiliser une méthode de nettoyage appelée Analyse en Composantes Principales (ACP).

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/517f4bc9-b09f-4550-b2a0-cc38628defbf/5fdd750a-dc4c-40f9-9541-3497baaf7dc8/Untitled.png)

> Figure 3: Heatmap des features
> 

Avant d'utiliser l'ACP, il est nécessaire de standardiser les valeurs présentes dans la dataset. Cela permet d'éviter que l'échelle de certaines colonnes n'impacte disproportionnellement le modèle. En standardisant les données, nous ramenons les valeurs à une échelle commune, ce qui facilite la comparaison entre les différentes caractéristiques et améliore les performances de l'ACP ainsi que d'autres algorithmes d'apprentissage automatique.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/517f4bc9-b09f-4550-b2a0-cc38628defbf/8daf8f1e-0034-4e62-aec2-00b53898f36e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/517f4bc9-b09f-4550-b2a0-cc38628defbf/522878ba-779d-4ece-b485-3ec5c7ee23c7/Untitled.png)

> Figure 4: Heatmap après le PCA
> 

La matrice de corrélation après application du PCA nous montre que les features obtenu après l’usage du PCA montre de très faibles corrélations matérialiser par la couleur violette omni présente sur le Heatmap.
Nous avons utilisé la méthode d'analyse en composantes personnelles pour sélectionner les 15 meilleures composantes principales qui expliquent 99,90% des variations présentes dans les données. En choisissant ces composantes, nous avons réussi à capturer l'essentiel de la structure et des motifs des données, tout en réduisant la dimensionnalité de manière significative. Cela nous permet de travailler avec un ensemble de caractéristiques plus compact et plus représentatif, ce qui peut simplifier les calculs et améliorer les performances des modèles prédictifs.

1.  **Model de prédictions**

Notre ensemble de données contient les résultats des élections pour différents candidats dans chaque commune, ce qui génère une grande quantité de données (3,6 Go). Nous avons divisé ces données en deux jeux de données : ceux des années 2012 et 2017. Le jeu de données de 2012 a été utilisé pour l'entraînement, tandis que celui de 2017 a été réservé pour les tests. Les deux ensembles de données ont suivi les mêmes étapes de prétraitement, comprenant la standardisation et la réduction de la dimensionnalité à l'aide de l'analyse en composantes principales (PCA).
Notre objectif principal est de prédire le vainqueur des élections à l'échelle de chaque commune. Ces prédictions combinées nous permettront de conclure qui sera le président.

**a) Rééquilibrage de la Dataset :**

Nous avons un très grand déséquilibre entre les classes dans nos features, avec une occurrence des éléments de la classe 0 (perdant) qui dépasse de très loin le nombre d'éléments de la classe 1 (gagnant). Cela peut empêcher le modèle de généraliser correctement. Dans ce cas, nous pouvons utiliser des méthodes telles que SMOTE pour la génération de données afin d'équilibrer les classes, ou utiliser des méthodes de sous-échantillonnage pour réduire la classe majoritaire.

Dans ce cas précis, nous avons utilisé la méthode de sous-échantillonnage appelée « Neighbourhood Cleaning Rule ». Son objectif principal est d'améliorer la qualité des données en éliminant les exemples bruyants ou mal classés qui pourraient compromettre les performances du modèle. Cette méthode repose sur le principe que les échantillons de la classe majoritaire qui sont mal classés par leurs voisins sont plus susceptibles d'être du bruit et peuvent donc être supprimés en toute sécurité.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/517f4bc9-b09f-4550-b2a0-cc38628defbf/8d96ea83-b6ae-4d3a-a3ec-0180a163a290/Untitled.png)

**b) Modèle de prédiction**
    

- Arbre de décision

Les arbres de décision peuvent capturer des relations non linéaires entre les variables et la variable cible. Ils peuvent identifier des motifs complexes dans les données sans nécessiter de spécification explicite de la forme de la relation, ce qui nous pousse à l’implémenter dans notre cas.

1. **Résultats :**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/517f4bc9-b09f-4550-b2a0-cc38628defbf/ac7532fa-c270-4cd8-b095-c43e4d392c3d/Untitled.png)

> Figure 5: matrice de confusion de l'arbre de décision
> 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/517f4bc9-b09f-4550-b2a0-cc38628defbf/1ad2b8c2-ea15-456d-8001-968313fd3f0d/Untitled.png)

> Figure 6: performance de l'arbre de décision
> 

**Prédiction :** 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/517f4bc9-b09f-4550-b2a0-cc38628defbf/9ee3ab9e-f95b-40dd-80ec-2bbf3062121d/Untitled.png)

> Figure 7: Prediction de président
> 

**Interpretation :**

La table de performance nous présente des valeurs très acceptables pour le F1-score, la précision et le rappel, qui sont des métriques essentielles pour évaluer la qualité d'un modèle. De plus, la matrice de confusion nous offre une vision claire du nombre de prédictions correctes réalisées par notre modèle. Globalement, nous sommes très satisfaits du nombre élevé de prédictions correctes effectuées par notre modèle. Cependant, lorsqu'on examine les classes individuellement, nous constatons que notre modèle prédit de manière plus performante les éléments de la classe 0 par rapport aux éléments de la classe 1.

Après avoir réalisé la prédiction des gagnants à l'échelle de chaque commune, nous avons déterminé le gagnant potentiel des élections de 2022, serait celui qui aura remporté le plus grand nombre de victoires à l'échelle des communes. Ce qui rend notre prédiction juste, car Ils s’avèrent que le gagnant des élections présidentiels de 2022 a été Emmanuel Macron.

1. **Comparaison**

Après avoir examiné en détail les performances de différents modèles pour la prédiction des résultats des élections à l'échelle des communes, nous constatons que l'arbre de décision est un modèle de predictions qui arrive a prédire le gagnant d’une elections présidentiel avec une précision de 73.01%.

Il est important de souligner que la qualité des prédictions pour la classe (1) est cruciale pour l'objectif de notre modèle, qui vise à prédire avec une forte probabilité les résultats des suffrages à l'échelle des communes. En considérant cette importance, l'arbre de décision émerge comme le meilleur choix parmi les trois modèles évalués.

En conclusion, nous pouvons dire que les features relatifs à la densité de population des communes ou aux performances scolaires par région sont des critères qui permettent de prédire quels candidats pourront être en tête ou pourront être les gagnants lors des prochaines élections, en se basant juste sur ces éléments.

1. **Source de nos datasets.**

Données sur les elections présidentielles : https://www.data.gouv.fr/fr/pages/donnees-des-elections/

Historique des populations communales : https://www.insee.fr/fr/statistiques/3698339

Niveau de diplôme de la population en 2019 : https://www.data.gouv.fr/fr/datasets/niveau-de-diplome-de-la-population-en-2019/#/information

Revenus et pauvreté des ménages en 2015 - tous les niveaux géographiques

https://www.insee.fr/fr/statistiques/3560121

Revenus et pauvreté des ménages en 2016 - tous les niveaux géographiques

https://www.insee.fr/fr/statistiques/4190004

Revenus et pauvreté des ménages en 2017 - Tous les niveaux géographiques **au 1er janvier 2020**

[https://www.insee.fr/fr/statistiques/4507225?sommaire=4507229&q=principaux+indicateurs+sur+les+revenus+et+la+pauvreté aux+niveaux+national+et+local](https://www.insee.fr/fr/statistiques/4507225?sommaire=4507229&q=principaux+indicateurs+sur+les+revenus+et+la+pauvret%C3%A9%20aux+niveaux+national+et+local)

Revenus et pauvreté des ménages en 2020 - Tous les niveaux géographiques au **1er janvier 2023** 

https://www.insee.fr/fr/statistiques/6692392?sommaire=6692394#consulter
