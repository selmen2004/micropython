Hasard
------

Des fois tu as envie des laisser le hasard choisir, ou d'introduire un peu de
hasard: tu veux que l'appareil agisse aléatoirement.

MicroPython est fourni avec un module ``random`` qui facilite l'introduction de
hasard et d'un peu de chaos dans ton code. Par exemple, voilà comment montrer un
nom au hasard sur l'affichage::

    from microbit import *
    import random

    noms = ["Mary", "Yolanda", "Damien", "Alia", "Kushal", "Mei Xiu", "Zoltan" ]

    display.scroll(random.choice(noms))

La liste ``noms`` contient sept noms définis par des chaînes de caractères. La
ligne finale est *imbriquée* (L'effet *oignon* présenté plus tôt): la méthode
``random.choice`` prend la liste ``noms`` comme argument et renvoie un élément
choisi au hasard. Cet élément (le nom choisi au hasard) est l'argument de la
méthode ``dispaly.scroll``.

Peux-tu modifier la liste pour y inclure ton propre ensemble de noms ?

Nombres aléatoires
++++++++++++++++++

Les nombres aléatoires sont très utiles. Ils sont communs dans les jeux. Pour
quelle autre raison avons-nous des dés ?

MicroPython est fourni avec plusieurs méthodes utiles pour les nombres aléatoires.
Voici comment faire un simple dé::

    from microbit import *
    import random

    display.show(str(random.randint(1, 6)))

A chaque fois que l'appareil est réinitialisé, il affiche un nombre entre 1 et 6.
Tu commences à avoir l'habitude de l'imbrication, donc il est important que tu
remarques ``random.randint`` qui renvoie un nombre entier entre ses deux arguments
inclus (un nombre entier est appelé *integer* en anglais d'où le nom de la méthodes).
Et que puisque ``display.show`` nécessite un argument sous forme de caractère
on utilise la fonction ``str```pour convertir la valeur numérique en un caractère
(on converti par exemple ``6`` en ``"6"``)

Si tu sais que tu voudras toujours un nombre entre ``0`` et ``N`` alors tu dois
utiliser la méthode ``random.range``. Si tu lui fournis un seul argument elle te
renverra un entier aléatoire **strictement** inférieur à cet argument. (ce qui est
différent du comportement de la méthode``random.randint``)

Des fois tu as besoin de nombres décimaux. Ils sont appelés nombres *à virgule
flottante* en informatique souvent abrégé en ``float`` et il est possible d'en
générer de façon aléatoire avec la méthode ``random.random``. Elle ne renvoie que
des valeurs comprises entre ``0.0`` et ``1.0`` inclus. Si tu as besoin de nombres
décimaux aléatoires plus grands, ajoute les résultats de ``random.randrange`` et
de ``random.random`` comme ça::

    from microbit import *
    import random

    reponse = random.randrange(100) + random.random()
    display.scroll(str(reponse))

Les Graines du Chaos
++++++++++++++++++++

Les générateurs de nombres aléatoire d'un ordinateur ne sont pas vraiment aléatoires.
Ils fournissent seulement des résultats semblant aléatoires étant donnée une
valeur initiale appelée valeur *graine* (ou *seed* en anglais). Cette graine est
souvent générée à partir de valeurs plus ou moins aléatoires comme l'heure du
moment ou des lectures de capteurs comme des thermomètres intégrés aux puces
électroniques.

Parfois tu auras besoin d'un comportement à peu près aléatoire mais répétable:
c'est-à-dire une source de hasard reproductible. C'est comme de dire que tu veux
les mêmes cinq valeurs aléatoire à chaque fois que tu lances cinq fois de suite
un dé.

C'est facile à accomplir en fixant toi-même la valeur *graine*. A partir d'une
même valeur *graine* le générateur de nombres aléatoires produira toujours la
même suite de nombres "aléatoires". La graine est fixée avec la méthode ``random.seed``
et n'importe quel nombre entier. Cette version du programme de dé produit toujours
les mêmes résultats::

    from microbit import *
    import random

    random.seed(1337)
    while True:
        if button_a.was_pressed():
            display.show(str(random.randint(1, 6)))

Comprends-tu pourquoi ce programme nécessite l'appuie sur le bouton A plutôt que
de réinitialier le micro:bit comme dans le premier exemple ?
