Hello, World!
-------------

La manière traditionnelle de commencer la programmation dans une nouvelle
langue est de demander à votre ordinateur de dire "Hello, World!".

.. image:: ../scroll-hello.gif

C'est facile avec MicroPython::

    from microbit import *
    display.scroll("Hello, World!")

Chaque ligne fait quelque chose de spécial. La première ligne::

    from microbit import *

    ... demande à MicroPython de récupérer tout ce dont il a besoin pour
    fonctionner avec le micro:bit BBC. Tout cela se trouve dans un module appelé
    ``microbit``(un module est une bibliothèque de code préexistant). Quand vous
    ``import`` quelque chose, vous dites à MicroPython que vous voulez l’utiliser, et
    ``*``c’est le moyen de Python de dire "tout" . Donc, en français, "je veux pouvoir tout
     utiliser depuis la bibliothèque de code microbit". ``from microbit import *``

La deuxième ligne::

    display.scroll("Hello, World!")

    ... indique à MicroPython d'utiliser l'affichage pour faire défiler la chaîne de caractères "Hello, World!".
     La partie ``display`` de cette ligne est un *objet* du module ``microbit``
     qui représente l'affichage physique du périphérique (on dit "objet" au lieu de
     "chose", "quoi" ou "doodah"). Nous pouvons dire à l'affichage de faire les
     choses avec un point ``.`` uivi de ce qui ressemble à une commande
     (en fait, c'est quelque chose que nous appelons une *méthode* ). Dans ce
      cas, nous utilisons la méthode``scroll``. Puisque ``scroll`` ndoit savoir
      quels caractères faire défiler l'affichage physique, nous les spécifions
      entre guillemets ((``"``) entre les parenthèses (``(`` et ``)``). Ce sont
      les *arguments*. Ainsi,``display.scroll("Hello, World!")`` signifie, en
      français, "Je veux que tu utilises l'écran pour faire défiler le texte
      'Hello, World!'". Si une méthode n'a pas besoin d'arguments que nous
      faisons cela clairement en utilisant des parenthèses vides comme ceci: ``()``.

Copiez le code "Hello, World!" Dans votre éditeur et flashez-le sur le
périphérique. Pouvez-vous trouver comment changer le message? Peux-tu le faire
dire bonjour? Par exemple, je pourrais dire "Bonjour, Nicolas!". Voici un
indice, vous devez changer l'argument de la méthode de défilement.

.. warning::

Cela peut ne pas fonctionner. :-)

C'est là que les choses amusantes commencent et que MicroPython essaie d'être utile.
S'il rencontre une erreur, il fera défiler un message utile sur l'écran du
micro-bit. Si c'est le cas, il vous indiquera le numéro de ligne où l'erreur
peut être trouvée.

Python s'attend à ce que vous tapiez EXACTEMENT la bonne chose. Ainsi, par
exemple, ``Microbit``, ``microbit`` et ``microBit`` sont toutes des choses
différentes pour Python. Si MicroPython se plaint à propos d'un ``NameError``
c'est probablement parce que vous avez tapé quelque chose de manière incorrecte.
 C'est comme la différence entre faire référence à "Nicholas" et "Nicolas".
 Ils sont deux personnes différentes mais leurs noms sont très similaires.

    Si MicroPython se plaint de ``SyntaxError`` ous avez simplement tapé du
    code d'une manière que MicroPython ne peut pas comprendre. Vérifiez que
    vous ne manquez pas de caractères spéciaux comme ``"`` ou ``:``.  C'est
    comme mettre un point au milieu d'une phrase. Il est difficile de comprendre
    exactement ce que vous voulez dire.

    Votre microbite peut cesser de répondre: vous ne pouvez pas lui envoyer un
    nouveau code ou entrer des commandes dans le REPL. Si cela se produit,
    essayez de le rallumer. En d'autres termes, débranchez le câble USB (et le
    câble de la batterie s'il est connecté), puis rebranchez le câble. Vous
    devrez peut-être également quitter et redémarrer votre application d'éditeur
     de code.
