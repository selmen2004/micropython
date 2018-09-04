Mouvement
--------

Ton BBC micro:bit est munit d'un accéléromètre. Il mesure le mouvement selon trois
axes :

* X - l'inclinaison de gauche à droite.
* Y - l'inclinaison d'avant en arrière.
* Z - le mouvement haut et bas.

Il y a une méthode pour chaque axe qui renvoie un nombre positif ou négatif qui
indique une mesure en milli-g. Lorsque la lecture est de 0, tu es "aligné" selon
cet axe.

Par exemple, voici un "niveau à bulle" très simple qui utilise ``get_x`` pour
mesurer l'aligmenet de l'appareil selon l'axe X::

    from microbit import *

    while True:
        lecture = accelerometer.get_x()
        if lecture > 20:
            display.show("D")
        elif lecture < -20:
            display.show("G")
        else:
            display.show("-")

Si tu tiens l'appareil horizontalement il devrait afficher ``-``; en revanche,
si tu l'inclines vers la gauche ou vers la droite il devrait afficher ``G`` ou
``D`` respectivement.

Nous voulons que l'appareil réagisse aux changement en permanence, donc nous
utilisons une boucle ``while`` infinie. La première chose que l'on fait *dans
le corps de cette boucle* est une mesure selon l'axe X que l'on nomme ``lecture``.
L'accéléromètre étant *tellement* sensible j'ai mis une  marge de +/-20 pour le
niveau. L'instruction ``else`` signifie que si ``lecture`` n'est pas entre -20
et 20 alors on considère qu'on n'est pas de niveau. Pour chacune des conditions
on utilise l'affichage pour montrer le caractère approprié.

Il y a aussi une méthode ``get_y`` pour l'axe Y et une méthode ``get_z`` pour
l'axe Z.

Si tu t'es déjà demandé comment un téléphone portable sait dans quel sens afficher
les images sur son écran, c'est parce qu'il utilise un accéléromètre de la même
façon que le programme ci-dessus. Les manettes de jeux contiennent aussi des
accéléromètres pour t'aider à tourner et à te déplacer dans les jeux.

Chaos musical
++++++++++++++

L'un des aspects les plus merveilleux du MicroPython sur le BBC micro:bit est la
façon dont il te permet facilement de relier les différentes possiblités de
l'appareil entres elles. Par exemple, transformons-le en un instrument de musique
(en quelque sorte)


Connecte un haut-parleur comme tu l'as fait dans le tutoriel sur la musique. Utilise
des pinces crocodile pour relier les pin 0 et GND aux connecteurs positif et
négatif du haut-parleur - le sens n'a pas d'importance.

.. image:: pin0-gnd.png

Que se passe-t-il si nous utilisons les  données de l'accéléromètre pour les jouer
comme des hauteurs de note ?

    from microbit import *
    import music

    while True:
        music.pitch(accelerometer.get_y(), 10)

La ligne clé est à la fin et est remarquablement simple. Nous *imbriquons* la
lecture de l'inclinaison sur l'axe Y en tant que fréquence dans la méthode
``music.pitch``. Nous ne la jouons que 10 millisecondes car nous voulons que le
ton change rapidement à mesure que l'appareil est incliné. Puisque l'appareil est
dans une boucle infinie il réagit constamment aux changements de la mesure sur
l'axe Y.

C'est tout!

Incline l'appareil en avant et en arrière. Si la lecture de l'inclinaison sur
l'axe Y est positive, cela changera le ton joué par le micro:bit.

Imagine un orchestre symphonique complet de ces appareil. Peux-tu jouer une
mélodie ? Comment pourrais-tu améliorer le programme pour que le micro:bit joue
de façon plus musicale ?
