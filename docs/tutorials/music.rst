Musique
-------

MicroPython sur le BBC micro:bit est fourni avec un module de musique et de son
puissant. Il est très facile de générer des bips avec l'appareil *si tu le
raccordes à un haut-parleur*. Utilise des pinces crocodile pour relier les pns 0
et GND aux entrées positives et négatives du haut-parleur.

.. image:: pin0-gnd.png

.. note::

    N'essaye pas de le faire avec un simple buzzer Piezo - ce genre de buzzer
    est seulement capable de jouer un seul ton.

Jouons de la musique!::

    import music

    music.play(music.NYAN)

Remarque que nous importons le module ``music``. Il contient les méthodes
utilisées pour produire et contrôler le son.

MicroPython a tout un tas de mélodies pré-programmées. En voici la liste
complète :

* ``music.DADADADUM``
* ``music.ENTERTAINER``
* ``music.PRELUDE``
* ``music.ODE``
* ``music.NYAN``
* ``music.RINGTONE``
* ``music.FUNK``
* ``music.BLUES``
* ``music.BIRTHDAY``
* ``music.WEDDING``
* ``music.FUNERAL``
* ``music.PUNCHLINE``
* ``music.PYTHON``
* ``music.BADDY``
* ``music.CHASE``
* ``music.BA_DING``
* ``music.WAWAWAWAA``
* ``music.JUMP_UP``
* ``music.JUMP_DOWN``
* ``music.POWER_UP``
* ``music.POWER_DOWN``

Prend le code d'exemple et change la mélodie. Quelle est ta préférée ? Comment
pourrais-tu utiliser ces airs comme des signaux ou des indices ?

Wolfgang Amadeus Microbit
+++++++++++++++++++++++++

Créer ta propre mélodie est facile !


Chaque note a un nom (comme ``C#`` ou ``F``), une octave (pour dire à MicroPython
à quelle hauteur il faut jouer la note) et une durée (combien de temps elle dure).
Les octaves sont indiquée par un nombre ~ 0 est la plus basse et 8 est à peu près
aussi haut que ce dont tu auras besoin à moins que tu ne fasses de la musique
pour chiens. La durée s'exprime aussi à l'aide de nombres. Plus la valeur de la
durée est grande plus la note sera jouée longtemps. Ces valeurs sont reliées
entres elles - par exemple, une durée de ``4`` durera deux fois plus longtemps
qu'une durée de ``2`` (et ainsi de suite). Si tu utilises la note nommée ``R``
alors MicroPython jouera une pause (c'est-à-dire un silence) pendant la durée
spécifiée.

Chaque note est représentée par une chaîne de caractères comme ça::

    NOTE[octave][:durée]

Par exemple, ``"A1:4"`` représente la note nommée ``A`` dans l'octave numéro 1 à
jouer sur une durée de ``4``.

Fais une liste de note pour créer une  mélodie (c'est équivalent à créer une
animation avec une liste d'images). Par exemple, voici comment faire jouer à
MicroPython le début de "Frère Jacques"::

    import music

    tune = ["C4:4", "D4:4", "E4:4", "C4:4", "C4:4", "D4:4", "E4:4", "C4:4",
            "E4:4", "F4:4", "G4:8", "E4:4", "F4:4", "G4:8"]
    music.play(tune)

.. note::

    MicroPython t'aide à simplifier de telles mélodies. Il se rappelera de
    l'ocatve et de la durée jusqu'à ce que tu les changes. Grâce à cela,
    l'exemple ci-dessus peut-être ré-écrit de cette façon::

        import music

        tune = ["C4:4", "D", "E", "C", "C", "D", "E", "C", "E", "F", "G:8",
                "E:4", "F", "G:8"]
        music.play(tune)

    Remarque que l'octave et la durée ne changent que lorsqu'elles le doivent.
    Ça fait beaucoup moins à taper et c'est plus simple à lire.

Effets sonores
++++++++++++++

MicroPython te permets de faire des sons qui ne sont pas des notes de musique.
Par exemple, voici comment créer un effet de sirène de police::

    import music

    while True:
        for freq in range(880, 1760, 16):
            music.pitch(freq, 6)
        for freq in range(1760, 880, -16):
            music.pitch(freq, 6)

Remarque comment la méthode ``music.pitch`` est utilisée dans cet exemple. Elle
attend une fréquence.  Par exemple, une fréquence de ``440`` est la même chose
qu'une note ``A`` (qui correspond au LA) utilisée pour accorder un orchestre
symphonique.

Dans l'exemple ci-dessus la fonction ``range`` est utilisée pour générer un
assortiment de valeurs numériques. Ces nombres sont utiliser pour définir la
hauteur du ton. Les trois arguments de la fonction ``range`` sont la valeur de
départ, la valeur de fin et la taille du pas. Ainsi, la première utilisation de
``range`` consiste à de dire, en français, "créé un assortiment de nombres compris
entre 880 et 1760 de 16 en 16". Sa deuxième utilisation dit "créé un assortiment
de nombres compris entre 1760 et 880 de -16 en -16". C'est comme ça que l'on
obtient une liste de fréquences qui montent puis qui descendent comme une sirène.

Puisque la sirène doit durer éternellement, elle est contenue dans une boucle
``while`` infinie.

surtout, nous avons introduit une nouvelle sorte de boucle à l'intérieur de la
boucle ``while``: la boucle ``for``. En français ça revient à dire "pour chaque
élément dans une certaine collection, fais des trucs avec". Plus précisément,
dans l'exemple ci-dessus ça dit "pour chaque fréquences dans l'assortiment de
fréquences, joue la hauteur de cette fréquence pendant 6 millisecondes". Remarque
que les choses à faire dans cette boucle sont indentée (comme on l'a vu
précédemment) de façon à ce que Python sache quel code exécuter avec chaque
élément.
