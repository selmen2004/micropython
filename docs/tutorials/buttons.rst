Boutons
-------

Jusqu'à maintenant nous avons créé du code fait faire quelque chose à l'appareil.
C'est ce qu'on appelle une *sortie* ou *output*. Cependant, nous avons aussi
besoin que l'appareil réagisse à quelque chose.C'est ce qu'on appelle des
*entrées* ou *inputs*.

C'est facile à retenir : une sortie est ce que l'appareil fait ressortir vers
le monde extérieur tandis qu'une entrée c'est qui provient du monde extérieur
et entre dans  l'appareil.

Les moyen les plus évidents d'entrées sur le micro:bit sont ses deux boutons,
nommés ``A`` et ``B``. D'une certaine façon, nous avons besoin que MicroPython
réagisse à l'appui sur ces boutons.

C'est extrêmement simple::

    from microbit import *

    sleep(10000)
    display.scroll(str(button_a.get_presses()))

Tout ce que fait ce script c'est de dormir pendant dix milles millisecondes,
(c'est-à-dire 10 secondes) et ensuite de faire défiler le nombre d'appuis sur le
bouton ``A``. C'est tout!

While it's a pretty useless script, it introduces a couple of interesting new
ideas:

Bien que ce soit un script plutôt inutile, il montre quelques nouvelles idées
intéressantes :

#. La *fonction* ``sleep`` fait dormir le micro:bitpendant un certain nombre
   de millisecondes. Si tu veux une pause dans ton programme, c'est ce qu'il
   faut faire. Une *fonction* est comme une *méthode* mais elle n'est pas attachée
   par un point à un *objet*.
#. Il y un objetc nommé ``button_a`` et il permet d'obtenir le nombre de fois où
   il a été pressé avec la *méthode* ``get_presses``.

Puisque ``get_presses`` renvoie une valeur numérique et que ``display.scroll``
ne peut afficher que des caractères, nous devons convertir la valeur numérique en
une chaîne de caractères. Nous le faisons avec la fonction ``str`` (qui un
raccourci pour *string* qui signifie chaîne en anglais). Cette fonction converti
son argument en une chaîne de caractères.

La troisième ligne est un peu comme un oignon. Si les parenthèses sont les
couches de l'onion alors tu remarqueras que ``display.scroll`` contient ``str``
qui lui-même contient ``button_a.get_presses``. Python essaye d'interpréter
d'abord ce qui se trouve le plus à l'intérieur, puis remonte les couches vers
l'extérieur. On appelle ça en anglais *nesting* (imbrication)- qui est l'équivalent en
programmation d'une poupée russe.

.. image:: matrioshka.jpg

Supposons que tu as appuyé 10 fois sur le bouton. Voilà comment Python interprète
ce qu'il se passe sur la troisème ligne :

Python voit la ligne complète et obtient la valeur de ``get_presses``::

    display.scroll(str(button_a.get_presses()))

Maintenant que Python sait combien d'appui sur le bouton il y eu, il converti la
valeur numérique en une chaîne de caracères ::

    display.scroll(str(10))

Enfin, Python sait ce qu'il doit faire défiler sur l'affichage::

    display.scroll("10")

Même si ça à l'air d'être beaucoup de travail, MicroPython fait ça de façon
extrêmement rapide.

Boucles événementielles
+++++++++++++++++++++++

Tu auras souvent besoin que ton programme soit dans l'attente que quelque chose
se produise. Pour ce faire, tu devras le faire "boucler" sur un morceau de code
qui défini comment réagir à certains événements attendus comme l'appui sur un
bouton.

Pour faire des boucles en Python on utilise le mot-clé ``while`` qui signifie
*tant que*. Il vérifie si quelque chose est ``True`` c'est-à-dire *Vrai*. Tant que
c'est le cas, il exécute un *bloc de code* appelé *corps* de la boucle. Lorsque
ce n'est plus le cas, il sort de la boucle (en ignorant son corps) et le reste du
programme peut continuer.

En Python, il est facile de définir un bloc de code. Disons que j'ai une liste
de chose à faire écrite sur un bout de papier. Elle ressemble surement à ça ::

    Courses
    Réparer la gouttière
    Tondre la pelouse

Si je veux rendre ma liste un peu plus précise, je peux écrire quelque chose
comme ça ::

    Courses:
        Oeufs
        Bacon
        Tomates
    Réparer la gouttière:
        Emprunter l'échelle du voisin
        Trouver un marteau et des clous
        Rendre l'échelle
    Tondre la pelouse:
        Vérifier qu'il n'y a pas de grenouille près de l'étang
        Vérifier le niveau d'essence dans la tondeuse

It's obvious that the main tasks are broken down into sub-tasks that are
*indented* underneath the main task to which they are related. So ``Eggs``,
``Bacon`` and ``Tomatoes`` are obviously related to ``Shopping``. By indenting
things we make it easy to see, at a glance, how the tasks relate to each other.

Il est évident que les tâches principales sont divisées en sous-tâches qui sont
*indentées* en-dessous de la tâche principale à laquelle elles sont reliées. Ainsi
``Oeufs``, ``Bacon`` et ``Tomates`` sont clairement reliés à ``Courses``. En
indentant les lignes, on permet facilement de voir en un coup d'oeil comment les
différente tâches sont relièes entres elles.

Là encore on parle de *nesting* (imbrication). On utilise l'imbrication pour
définir des blocs de code comme ça ::

    from microbit import *

    while running_time() < 10000:
        display.show(Image.ASLEEP)

    display.show(Image.SURPRISED)

La fonction ``running_time`` renvoie le nombre de millisecondes depuis que
l'appareil a démarré.

La ligne ``while running_time() < 10000:`` vérifie si le temps écoulé est
inférieur à 10000 millisecondes (c'est-à-dire 10 secondes). Tant que c'est le cas,
il affichera ``Image.ASLEEP``. Remarque comme c'est indenté en dessous de
l'instruction ``while`` comme dans notre *liste de choses à faire*.

Evidemment, si le temps écoulé est supérieur ou égal à 1000 millisecondes alors
l'affichage montrera ``Image.SURPRISED``. Pourquoi ? Parce que la condition du
``while`` sera fausse (``running_time`` ne sera plus ``<10000``). Dans ce cas
la boucle est terminée et le programme continue après le corps de la boucle
``while``. Cela fait comme si l'appareil était endormi pendant 10 secondes avant
de se réveiller avec un air surpris.
Essaie-le !

Gérer un événement
++++++++++++++++++

Si nous voulons que MicroPython réagisse aux événement "*appui sur un bouton*"
nous devrions le mettre dans une boucle infinie et vérifier si le bouton ``is_pressed``.

Une boucle infinie est facile::

    while True:
        # Faire des trucs

(Rappelle-toi, ``while`` vérifie si quelque chose est ``True`` pour déterminer si
il doit exécuter son corps. Puisque ``True`` est évidemment ``True`` tout le
temps, on obtient une boucle infinie !)

Faisons un cyber-animal très simple. Il est tout le temps triste sauf quand tu
appuies sur le bouton ``A``. Si tu appuies sur le bouton ``B``, il meurt. (Je me
rends compte que ce n'est pas un jeu très amusant, donc peut-être que tu peux
trouver comment l'améliorer)::

    from microbit import *

    while True:
        if button_a.is_pressed():
            display.show(Image.HAPPY)
        elif button_b.is_pressed():
            break
        else:
            display.show(Image.SAD)

    display.clear()

Can you see how we check what buttons are pressed? We used ``if``,
``elif`` (short for "else if") and ``else``. These are called *conditionals*
and work like this::

As-tu vu comment on vérifie quel bouton est pressé ? On utilise ``if``
(qui veut dire *si*), ``elif`` (qui veut dire *autre si*) et ``else`` (qui veut
dire *sinon*). Ce sont des *instructions conditionnelles* et elles marchent
comme ça ::
    if quelque chose est vrai (``True``):
        # fais un truc
    elif autre chose est vrai (``True``):
        # fais un autre truc
    else:
        # fais encore autre chose.

C'est très proche de l'anglais !

La méthode ``is_pressed`` ne renvoie que deux résultats possibles : ``True`` ou
``False``. Si tu appuie sur le bouton, elle renvoie ``True``, sinon elle renvoie
``False``.Finalement, exprimé en français, le code ci-dessus dit : "Pour toujours,
si le bouton A est pressé montre un visage joyeux, sinon, si le bouton B est pressé
sort de la boucle, sinon montre un visage triste." On peut sortir de la boucle
infinie avec l'instruction ``break``.

A la toute fin, lorsque notre cyber-animal est mort, on efface l'affichage (avec
la méthode ``clear``).

Peux-tu trouver des façons de rendre ce jeu moins tragique ? Comme pourrais-tu
vérifier que les deux boutons sont pressés ? (Indice : Pyhon possède des opérateurs
logiques : ``and`` -> *et* ; ``or`` -> *ou* ; ``not`` -> *non*)

.. footer:: The image of Matrioshka dolls is licensed CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=69402
