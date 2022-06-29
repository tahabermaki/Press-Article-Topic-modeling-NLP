# Topic-modeling-d'article-de-presse
La modélisation thématique est une méthode de classification non supervisée de tels documents, similaire au regroupement sur des données numériques, qui trouve des groupes naturels d'éléments même lorsque nous ne sommes pas sûrs de ce que nous recherchons. Dans ce projet, nous allons extraire le pourcentage de thèmes dans chaque article que nous avons dans l'ensemble de données.

Etapes de préparation des données :
1.	Tokenisation : transformer un texte en une série de Tokens individuels
2.	Supprimer les Stopwords : Création d’une liste de stopwords personnalisée compatible avec nos données qui peut être encore amélioré en ajoutant des mots qui ne nous intéressent pas.
3.	Lemmatization : donner aux mots la forme neutre canonique qu'ils ont.
4.	Création de Bigram and Trigram Models : à partir de notre liste de tokens nettoyés, créer des bigrammes et trigrammes (paires de mots, qui peuvent être porteurs de sens et qui sont donc utile pour le topic extraction).
5.	Supprimer les articles trop courts (Pas important) : Pour optimiser les résultats du modèle, nous pouvons éviter d'avoir des articles avec moins de 30 tokens après le nettoyage.

Topic Modeling
Modèle LDA: 
LDA prend en compte un corpus de documents, un certain nombre de k sujets et produit des distributions de probabilité de topic (sujets) pour chaque document.
Il est important de noter qu'en mentionnant "topic 0" ou "topic 1", ces sujets consistent généralement en des distributions de probabilités sur plusieurs mots qui composent le sujet.
Par exemple:
Le topic 14 pourrait consister en 40 % de « Classe », 30 % de « enfant » et 20 % de « scolaire » …
L’Output du modèle serait:
•	La répartition des mots par sujet.
•	Répartition des sujets par document.
*Plus d’informations sur le notebook*
Métrique d’évaluation : 
On utilise le score de cohérence dans le topic modeling pour mesurer à quel point les sujets sont interprétables pour les humains. Dans ce cas, les sujets sont représentés par les N premiers mots ayant la probabilité la plus élevée d'appartenir à ce sujet particulier. En bref, le score de cohérence mesure à quel point ces mots sont similaires les uns aux autres.

Nombre de topic :
Nous initialisons notre modèle LDA à l'aide de Gensim et spécifions les Topic souhaités comme 15.
Cette valeur peut être améliorer grâce à la valeur de la cohérence. 
Il n'y a pas de façon unique de déterminer si le score de cohérence est bon ou mauvais. Le score et sa valeur dépendent des données à partir desquelles il est calculé. Par exemple, dans un cas, le score de 0,5 peut être suffisant mais pas acceptable dans un autre cas. La seule règle est que nous voulons maximiser ce score.

Habituellement, le score de cohérence augmentera avec l'augmentation du nombre de sujets. Cette augmentation diminuera à mesure que le nombre de sujets augmentera. Le compromis entre le nombre de sujets et le score de cohérence peut être réalisé en utilisant la technique dite du coude. La méthode consiste à tracer le score de cohérence en fonction du nombre de sujets. Nous utilisons le coude de la courbe pour sélectionner le nombre de sujets.

Résultats : 
![image](https://user-images.githubusercontent.com/45733593/176407200-a144bdd4-9350-4f6c-b835-85380416860f.png)

  
Le score de cohérence que nous avons obtenu pour ce modèle était :
 ![image](https://user-images.githubusercontent.com/45733593/176407245-2b6a88ed-d66e-45f0-bd9a-e364b00503f0.png)

Comme la figure l’indique nous avons réussi à dégager des Topics avec une distance acceptable c’est-à-dire qu’il n’y a pas de chevauchement entre les sujets.
(Voir le notebook pour une visualisation interactive)
Par exemple le Topic 9 représenté par des mots comme : ville, mairie, travail, commune, municipal, syndicat, public, terrain… peut référer au sujet de la VILLE.
Le Topic 5 et le Topic 2 (les plus intéressants pour l’étude) représentés par des mots comme : Prix, client, consommation, entreprise, commande, usine … renvoie au sujet de l’ENTREPRISE. 

Le modèle renvoie une liste de probabilité d’appartenance à un topic comme suit : 
![image](https://user-images.githubusercontent.com/45733593/176407147-b8625894-64d0-4eb1-a9e0-a4e3786bcc7b.png)

