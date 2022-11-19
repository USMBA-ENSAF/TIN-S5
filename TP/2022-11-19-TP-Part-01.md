---
title: LAB01 - Lane Lines Detector with OpenCV
author: Pr. Hicham Belkebir
date: 2022-11-23
---

# Partie 01

## Objectives 

Nous désirons dans cet atelier développer un détecteur efficace de lignes de voie d'une route quelconque en utilisant `Python` comme langage de programmation et OpenCv comme bibliothèque qui mettra a notre disposions les différents fonctionnalités permettant la manipulation des images et enfin matplotlib comme bibliothèque graphique pour gérer les différents graphiques générés par nos programmes.

Au cours de cet atelier nous allons explorer les aspects suivant du traitement d'image :

- Changement d'espace calorimétrique;

- Détection de contour;

- Sélection de région d'intérêt dans une image (ROI);

- Implémentation de la transformée de Hough pour la détection des lignes de la voie.

---

## Pré requis du LAB

Environnement Python fonctionnel dans lequel est installé les paquetages suivants : 

- Numpy;

- Matplotlib;

- Scikit-learn;

- Scikit-image;

- OpenCV 3.6; 

- Opencv-python;

- Pillow,

- Scipy.

- ffmpeg-python

- pprint

## Extraction des images à partir d'une vidéo.

La première étape de ce Lab consiste a extraire les images qu'on va manipuler à partir d'une séquence vidéo au format mp4. Pour ce faire, nous allons utiliser le paquetage `ffmpeg` :

1. Utiliser la méthode `probe` de `ffmpeg` et créer un objet probe qui vous donne l'accès aux propriétés de la séquence vidéo.

2. Filtrez le contenu de l'objet probe pour en sortir les propriétés du stream vidéo.

3. Afficher la résolution de la vidéo et le nombre de frame quelle contient.

>NB: Pour l'impression a la sortie standard, on utilisera le paquetage `pprint`.

4. En utilisant les méthodes `input`, `filter`, `output` et 'run', charger les données de la séquence vidéo sous forme d'un tenseur numpy de dimension ([indice de la frame, nombre de ligne, nombre de colonnes, nombre de canaux de couleur]). Choisir un $fps=5:1$.

5. Créer une fonction: 

    ```python
        def show_images(images:numpy.ndarray,cmap:str):
            # Utiliser une grille de deux colonnes et 5 ligne pour l'affichage
            # des images chargees dans le tableau numpy genere precedement.

    ```
6. Afficher les 10 premières frames chargées dans votre tableau numpy.

7. En utilisant maintenant le module Image du paquetage PIL (pillow) sauvegarder l'ensemble des frames au format `PNG` dans le répertoire test_image.

8. Validez cette étape avant de passer a la suivante.

---

## Manipulation de l'espace calorimétrique avec OpenCV.


En utilisant les méthodes `pprint` de pprint, `filter` et `map` de `python`, `Image.open` de `pillow` et `cvtColor` de `OpenCV` écrire un script python qui permet d'accomplir les taches ci-dessous tout en utilisant le paradigme fonctionnel:
    
1. Charger le chemin des images dans une liste.

2. Charger a partir de cette liste les images dans une liste d'objet `pillow`;

3. Convertir le contenu de cette liste dans un premier temps  au format `Lab` et afficher les composantes de luminescence.

4. Convertir ensuite la même liste dans l'espace HSV et afficher les composantes de luminescence.

5. Convertir toujours la même liste au format YCbCr et afficher le résultat.

6. Comparez et conclure.

## Utilisation des masques de couleurs.

Notre intérêt principale au cours de ce Lab porte sur l'isolation des lignes de voie qui sont colores dans la plus part du temps soit en blanc ou en jaune. Partant de ce constat, nous allons élaborer un masque de couleur qui permet d'éliminer les composantes colorimétrique de nos images autres que le blanc et le jaune. Notez bien qu'on va prendre pour représenter  le jaune dans l'espace sRGB le vecteur `[190,190,0]` comme ton avec saturation minimale et `[255, 25, 0]` comme ton avec saturation maximale. Nous allons utilisez les fonction `bitwise_or`, `bitwise_and` et `inRange` d'openCv pour mettre en oeuvre cette partie du Lab.

1. Commencez par définir la fonction `im2YW(im:PIL)->im:PIL`

2. Appliquer cette fonction sur la liste des images représentées dans l'espace sRGB puis en représentation YcbCr puis en Lab et enfin en HSV.

3. Afficher les résultats et comparez les performances et conclure.

---

## Détection des contours

Dans cette partie, nous allons appliquée la démarche développée dans le cours pour détecter les contours présents dans les images issues de l'étape précédente.

1. Choisir l'espace de représentation adéquat qui permet une détection de contour de qualité.

2. Extraire la composante de luminance des images.

2. Calcul des images du gradient en utilisant le filtre de Sobel dans la direction horizontale et verticale.

3. Calcul de la norme du gradient en utilisant les normes suivantes:
   
   - Norme euclidienne;
   - Norme infinie;
   - Norme Sup.

4. Élaborez la fonction qui permet de supprimer les non-maximas locales de l'image de la norme du gradient et exécutez la pour les trois types de normes.

5. Écrire la fonction qui permet de réaliser le seuillage par hystéries et appliquer la aux images générés lors de l'étape précédente.

6. Comparez le résultat obtenu avec celui qu'on peut obtenir avec la méthode de détection de Canny implémenté dans openCV

7. Procédez au fermeture des contours détectés par l'utilisation des opérateurs morphologiques.

>NB: Dans chaque étape vous devez afficher les résultats et générez vos analyses et conclusion.

---
