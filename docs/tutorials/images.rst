Images
------


MicroPython est à peu près aussi bon en art que tu pourrais l'être si la seule
je que tu avais était une grille de LED de 5x5. MicroPython te donne pas mal de
contrôle sur l'affichage de façon à ce que tu puisses créer toute sorte d'effets
intéressants.

MicroPython est fourni avec beaucoup d'images intégrées à montrer sur
l'affichage. Par exemple, pour que l'appareil ait l'air heureux, tape::

    from microbit import *
    display.show(Image.HAPPY)

J'imagine que tu peux te rappeler ce fait la première ligne. La seconde utilise
l'objet ``display`` pour ``show`` (montrer) une image intégrée. L'image *heureux*
que nous voulons afficher fait partie del'objet ``Image`` et est appelée ``HAPPY``.
On écrit ``show`` pour l'utiliser en la mettant entre parenthèses (``(`` et ``)``).

.. image:: happy.png

Voici la liste des images intégrées:

    * ``Image.HEART``
    * ``Image.HEART_SMALL``
    * ``Image.HAPPY``
    * ``Image.SMILE``
    * ``Image.SAD``
    * ``Image.CONFUSED``
    * ``Image.ANGRY``
    * ``Image.ASLEEP``
    * ``Image.SURPRISED``
    * ``Image.SILLY``
    * ``Image.FABULOUS``
    * ``Image.MEH``
    * ``Image.YES``
    * ``Image.NO``
    * ``Image.CLOCK12``, ``Image.CLOCK11``, ``Image.CLOCK10``, ``Image.CLOCK9``,
      ``Image.CLOCK8``, ``Image.CLOCK7``, ``Image.CLOCK6``, ``Image.CLOCK5``,
      ``Image.CLOCK4``, ``Image.CLOCK3``, ``Image.CLOCK2``, ``Image.CLOCK1``
    * ``Image.ARROW_N``, ``Image.ARROW_NE``, ``Image.ARROW_E``,
      ``Image.ARROW_SE``, ``Image.ARROW_S``, ``Image.ARROW_SW``,
      ``Image.ARROW_W``, ``Image.ARROW_NW``
    * ``Image.TRIANGLE``
    * ``Image.TRIANGLE_LEFT``
    * ``Image.CHESSBOARD``
    * ``Image.DIAMOND``
    * ``Image.DIAMOND_SMALL``
    * ``Image.SQUARE``
    * ``Image.SQUARE_SMALL``
    * ``Image.RABBIT``
    * ``Image.COW``
    * ``Image.MUSIC_CROTCHET``
    * ``Image.MUSIC_QUAVER``
    * ``Image.MUSIC_QUAVERS``
    * ``Image.PITCHFORK``
    * ``Image.XMAS``
    * ``Image.PACMAN``
    * ``Image.TARGET``
    * ``Image.TSHIRT``
    * ``Image.ROLLERSKATE``
    * ``Image.DUCK``
    * ``Image.HOUSE``
    * ``Image.TORTOISE``
    * ``Image.BUTTERFLY``
    * ``Image.STICKFIGURE``
    * ``Image.GHOST``
    * ``Image.SWORD``
    * ``Image.GIRAFFE``
    * ``Image.SKULL``
    * ``Image.UMBRELLA``
    * ``Image.SNAKE``

Il y en a pas mal! Pourquoi ne pas modifier le code qui donne à micro:bit l'air
heureux pour voir à quoi ressemble les autres images intégrées ? (Il te suffit de
remplacer ``Image.HAPPY`` par l'une des images intégrées de la liste ci-dessus.)

Images personnelles
+++++++++++++++++++

Bien sûr, tu veux que ta propre image s'affiche sur le micro:bit, non ?

C'est facile.


Chaque pixel LED sur l'affichage physique peut prendre une parmi dix valeurs.
Si un pixel prend la valeur ``0`` (zéro) c'est qu'il est éteint. Litéralement,
il a une luminosité de zéro.En revanche, s'il prend la valeur ``9`` il est à la
luminosité maximale. Les valeurs de ``1`` à ``8`` représentent des niveaux de
luminosité entre éteint (``0``) et "à fond" (``9``).

Muni de ces informations, il est possible de créer une nouvelle image comme ça::

    from microbit import *

    boat = Image("05050:"
                 "05050:"
                 "05050:"
                 "99999:"
                 "09990")

    display.show(boat)

(Une fois lancé, l'appareil devrait afficher un bateau à voile dont le mât est
moins brillant que la coque).

As-tu compris comment dessiner une image ? As-tu remarqué que chaque ligne de
l'affichage physique est représentée par une line de nombres se terminant par ``:``
et entourée de ``"`` guillemets doubles ? Chaque nombre indique une luminosité.
Il y a cinq lignes de cinq nombres donc il est possible de spécifier la luminosité
individuelle de chacune des cinq LED sur chacune des cinq lignes sur l'affichage
physique. C'est comme ça qu'on créé une image.

Simple!

En fait, tu n'as pas besoin d'écrire tout ça sur plusieur lignes. Si tu te sent
capable de garder la trace de chaque ligne, tu peux le ré-écrire comme ça::

    boat = Image("05050:05050:05050:99999:09990")

Animation
+++++++++

Les images statiques sont amusantes, mais c'est encore plus amusant de les faire
bouger. C'est aussi incroyablement facile à faire avec MicroPython ~ il suffit
d'utiliser une liste d'images.

Voici une liste de courses::

    Oeufs
    Bacon
    Tomates

Et voici comment la représenter en Python::

    courses = ["Oeufs", "Bacon", "Tomates" ]

J'ai simplement créé une liste nommée ``courses`` et elle contient trois éléments.
Python sait que c'est une liste car elle est contenue dans des crochets (``[``
et ``]``). Les éléments de la liste sont séparés par des virgules (``,``) et dans
cet exemple les éléments sont trois chaînes de caractères: ``"Oeufs"``, ``"Bacon"``
et ``"Tomates"``. Nous savons que ce sont des chaînes de caractères parce qu'elles
sont contenues des guillemets ``"``.

Tu peux stocker n'importe quoi dans une liste en Python. Voici une liste de
nombres::

    premiers = [2, 3, 5, 7, 11, 13, 17, 19]


.. note::

    Les nombres n'ont pas besoin d'être entre guillemets puisqu'ils représentent
    une valeur (plutôt qu'une chaînes de caractères). C'est la différence entre
    ``2`` (la valeur numérique 2) et ``"2"`` (le caractères, le chiffre, qui
    représente le nombre 2). Ne t'inquiète pas si ce n'est pas très clair pour
    l'instant. Tu t'y habitueras bientôt.

Il est même possible de stocker des choses de catégories différentes dans une
même liste::

    list_variee = ["salut!", 1.234, Image.HAPPY]

As-tu remarqué le dernier élément? C'était une image!

On peut dire à MicroPython d'animer une liste d'images. Par chance npus avons
deux listes d'images déjà prêtes. Elles s'appellent ``Image.ALL_CLOCKS`` et
``Image.ALL_ARROWS``::

    from microbit import *

    display.show(Image.ALL_CLOCKS, loop=True, delay=100)

Comme avec une seule image, on utilise ``display.show`` pour la montrer sur
l'affichage du matériel. Mais ici on indique à MicroPython d'utiliser ``Image.ALL_CLOCKS``
et il comprend qu'il doit montrer chaque image de la liste, l'une après l'autre.
On indique aussi à MicroPython de parcourir la liste d'images en boucle (pour
que l'animation se répète indéfiniment) en écrivant ``loop=True``. De plus, nous lui
indiquons que nous voulons un temps de 10 millisecondes entre chaque image avec
l'argument ``delay=100``.

Peux-tu trouver comment animer la liste ``Image.ALL_ARROWS`` ? Comment éviterais-tu
de la parcourir en boucle indéfiniment ? (Indice: le contraire de ``True`` est
``False`` bien que la valeur par défaut de ``loop`` soit ``False``)? Peux-tu changer
la vitesse de l'animation ?

Enfin, voici comment créer ta propre animation. Dans mon exemple, je vais faire
couler mon bateau en bas de l'affichage::

    from microbit import *

    bateau1 = Image("05050:"
                  "05050:"
                  "05050:"
                  "99999:"
                  "09990")

    bateau2 = Image("00000:"
                  "05050:"
                  "05050:"
                  "05050:"
                  "99999")

    bateau3 = Image("00000:"
                  "00000:"
                  "05050:"
                  "05050:"
                  "05050")

    bateau4 = Image("00000:"
                  "00000:"
                  "00000:"
                  "05050:"
                  "05050")

    bateau5 = Image("00000:"
                  "00000:"
                  "00000:"
                  "00000:"
                  "05050")

    bateau6 = Image("00000:"
                  "00000:"
                  "00000:"
                  "00000:"
                  "00000")

    tous_les_bateaux = [bateau1,bateau2,bateau3,bateau4,bateau5,bateau6]
    display.show(tous_les_bateaux, delay=200)

Voici comment le code marche:

* Je créé six images de ``bateau`` de la même façon que ce que j'ai décris au-dessus.
* Ensuite, je les mets dans une liste que j'appelle ``tous_les_bateaux``
* Enfin, je demande ``display.show`` pour animer la liste avec un délai de 200 millisecondes
* Puisque je n'ai pas déclaré ``loop=True``, le bateau ne coulera qu'une fois
(rendant ainsi mon animation scientifiquement correcte). :-)

Que voudrais-tu animer ? Peux-tu animer un effet spécial ? Comment ferais-tu un
fondu d'image en sortie et en ouverture ?
