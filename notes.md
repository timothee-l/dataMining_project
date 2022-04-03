# 24 mars

## Requête à Wikidata
*Valeurs temporaires*  
- On limite le nombre de mouvements à 10  
- On limite le nombre d'artistes à 40  
- On limite le nombre total de tableaux à 200  
- On limite les dates (1000 à 2022)

## Affichage
On affiche k tableaux (image) avec un numéro  
L'utilisateur entre le num du tableau choisi (ou mieux il clique sur le tableau)

## Paramètres initiaux
  Variance : maximale  
  Espérance : Au milieu  
  Pourcentage pour mouvements : 1/nombre de mouvements

## Interprétation du choix
- Mouvement : on augmente le pourcentage du mouvement choisi (incrémentation fixe genre 50%)  
  **À modifier, car pas adapté, mais c'est simple donc ok pour l'instant**  
  On diminue tous les autres mouvements pour équilibrer 
- Image/Date : 
  - si le choix < à delta fixé (genre 20) alors cohérent avec prédiction donc on diminue la variance (*2/3 ?)
  - sinon on garde variance constante 
  Dans tous les cas on déplace l'espérance, qqch comme  
  `E = E + (E - indexChoix)/nombreDeChoix`

## Trouver artiste  
On veut comme résultat l'artiste préféré donc il faut associer un artiste aux valeurs dominantes de nos 3 paramètres
- Le peintre qui a des tableaux en moyenne proche de l'année dominante (espérance)
- Pareille couleur dominante ou intensité dominante (espérance)
- Bon mouvement  

Problème : pas fiable, car 2 artistes du même mouvement auront quasi les mêmes résultats je pense
Solutions : 
  - on limite le nombre d'artistes pour éviter trop de recouvrement (pas idéal, mais facile)
  - on utilise des paramètres plus précis / plus de paramètres (bien, mais pas le temps)
  - si doute on compte combien de tableaux ont été choisis pour chaque artiste comme ça on prend celui avec le plus de tableaux choisis
  - même délire, mais à la fin on propose un tableau pour chaque artiste sur lesquels on hésite et on valide l'artiste choisi


## Choix tableaux
Il faut prendre en compte les 3 paramètres
- Image/Date
  - On classe les tableaux par ordre croissant (basse à haute luminosité, plus vieux au plus récente, ...)
  - On associe à chaque tableau une probabilité 
  - On calcule la proba `P=(Pimage+Pdate)/2` ou `P=(kP1 + P2)/(k + 1)` avec P1 k fois plus important que P2
- Mouvement
  - Même principe Ptotal = `(k*P+Pmouvement)/(k+1)`
  
On a finalement une proba pour chaque tableau et on peut les tirer au hasard avec un random comme ça

## Rendu détaillé
Faudrait faire un deuxième notebook où on présente nos informations.  
En gros on propose un choix et on affiche tous nos résultats sous forme stylée. 
- Graphiques pour montrer les probabilités partielles
- Découpage en beaucoup de cellules pour expliquer chaque élément indépendamment

## Reconnaissance Image  
Première itération
- 1 valeur : intensité grayscale
- 3 valeurs : intensités des 3 canaux de couleur (3x plus de calcul)

## Améliorations
- Analyse de l'image plus poussée 
    - Analyse histogramme à la de faire la moyenne
    - Reconnaissance de contenu : Humain ? Paysage ? ...
- Optimisation du code pour pas calculer une proba pour chaque tableau à chaque itération