Entrée/Sortie
------------

Il y a des bandes de métal sur  le côté bas du BBC micro:bit qui lui font des
sortes de dents. Ce sont les pin d'entrée/sortie (ou pin E/S pour faire court)

.. image:: blue-microbit.png

Certains de ces pins sont plus gros que d'autres donc il est possible d'y
accrocher des pinces crocodiles. Ceux sont numérotés 0, 1, 2, 3V et GND (les
ordinateurs comptent toujours à partir de zéro). Si tu branche une carte dédiée
à ton micro:bit, il est également possible de relier des câbles aux autres
(plus petits) pins.

Chaque pin sur le BBC micro:bit est représenté par un *objet* appelé ``pinN``
où ``N`` est le numéro du pin. Donc, par exemple, pour faire quelque chose avec
le pin numéroté 0 (zéro), on utilise l'objet appelé ``pin0``.

Facile!

Ces objets ont des *méthodes* variées qui leur sont associée en fonction de ce
que ce pin particulier est capable de faire.

Python chatouilleux
+++++++++++++++++++

L'exemple le plus simple d'entrée par les pins est de déterminer si ils sont
touchés. Donc, tu peux chatouiller ton appareil et le faire rire comme ça::

    from microbit import *

    while True:
        if pin0.is_touched():
            display.show(Image.HAPPY)
        else:
            display.show(Image.SAD)

Avec une main, tiens ton appareil par le pin GND. Puis, avec ton autre main,
touche (ou chatouille) le pin 0 (zéro). Tu devrais voir l'image affichée passer
de grognon à content.

C'est une forme simpliste de mesure de l'entrée. On commence vraiment à
s'amuser lorsque l'on connecte des circuits et d'autres appareils grâce aux pins.

Bip Bip
+++++++

La chose la plus simple que nous puission raccorder à l'appareil est un buzzer.
Nous allons l'utiliser comme une sortie.

.. image:: piezo_buzzer.jpg

Ces petits appareils émettent un bip aigü lorsqu'ils sont connecté à un circuit.
Pour en relier un à ton micro:bit, tu dois raccorder une pince crocodile aux pins
0 et GND (voir ci-dessous)

.. image:: pin0-gnd.png

Le câble partant du pin 0 doit raccordé au connecteur positif du buzzer et celui
partant du GND à connecteur négatif.

Le programme suivant fera émettre un son au buzzer::

    from microbit import *

    pin0.write_digital(1)

This is fun for about 5 seconds and then you'll want to make the horrible
squeaking stop. Let's improve our example and make the device bleep::

C'est marrant pendant à peu près 5 secondes et ensuite tu auras envie d'arrêter
cet horrible couinement. Améliorons notre exemple en le faisant bipper par
intervalles::

    from microbit import *

    while True:
        pin0.write_digital(1)
        sleep(20)
        pin0.write_digital(0)
        sleep(480)

Peux-tu comprendre comment ce script fonctionne ? Rappele-toi que ``1`` est "on"
et ``0`` est "off" dans le monde digital.

The device is put into an infinite loop and immediately switches pin 0 on. This
causes the buzzer to emit a beep. While the buzzer is beeping, the device
sleeps for twenty milliseconds and then switches pin 0 off. This gives the
effect of a short bleep. Finally, the device sleeps for 480 milliseconds before
looping back and starting all over again. This means you'll get two bleeps per
second (one every 500 milliseconds).

L'appareil est mis dans une boucle infinie et met immédiatement le pin 0 sur "on".
Ce qui fait que le buzzer émet un son. Pendant qu'il fait du bruit, l'appareil
dort pendant vingt millisecondes puis passe le pin 0 sur "off". Cela donne l'effet
d'un bip court (20ms). Enfin, l'appareil dort pendant 480 millisecondes avant de
recommencer la boucle indéfiniment. Ce qui signifie que tu obtiens deux "bip" par
seconde (un toutes les 500 millisecondes)

On a fait un métronome !

.. footer:: The image of the pizeo buzzer is CC BY-NC-SA 3.0 from https://www.flickr.com/photos/tronixstuff/4821350094
