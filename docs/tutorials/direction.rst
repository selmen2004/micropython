Direction
---------

Il y a une boussole sur le BBC micro:bit. Si tu veux faire une station météo
utilise l'appareil pour déterminer la direction du vent.

Boussole
++++++++

Il peut aussi t'indiquer la direction du Nord comme ça::

    from microbit import *

    compass.calibrate()

    while True:
        aiguille = ((15 - compass.heading()) // 30) % 12
        display.show(Image.ALL_CLOCKS[aiguille])

.. note::

        **Tu dois calibrer la boussole avant de l'utiliser.** Ne pas le faire
        entraine des résultats inutilisables. La méthode ``calibration`` lance un
        petit jeu pour aider l'appareil à déterminer sa position par rapport au
        champs magnétique de la Terre.

    Pour calibrer la boussole, incline le micro:bit dans tous les sens jusqu'à ce
    qu'un cercle de pixel soit dessiné sur les bords de l'affichage

Le programme prend la direction fournie par ``compass.heading`` et, en utilisant 
de simple maths de façon astucieuse, `division entière <https://en.wikipedia.org/wiki/Floor_and_ceiling_functions>`_ ``//``
and `modulo <https://en.wikipedia.org/wiki/Modulo_operation>`_ ``%``, détermine  le nombre que l'aiguille de la montre doit afficher pour indiquer approximaivement
le nord.
