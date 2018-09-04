.. BBC Microbit Micropython documentation master file, created by
   sphinx-quickstart on Tue Oct 20 10:41:30 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Documentation du BBC micro:bit MicroPython
==========================================

Bienvenu!

Le BBC micro:bit est un petit dispositif informatique pour les enfants. L'un des
langages qu'il comprend est le langage de programmation poopulaire Python. La
version utilisée sur le BBC micro:bit est appelée MicroPython.

Cette documentation comprend des leçons pour les enseignants et une documentation
de l'API pour les développeurs ( regarde l'index sur la gauche ). Nous espérons
que tu aimeras développer en MicroPython pour le BBC micro:bit.

Si tu es un programmeur débutant, un enseignant ou si tu ne sais pas par quoi
commencer, vas voir les tutoriels.

.. image:: comic.png

.. note::

    Ce projet est en cours de développement. Merci d'aider les autre développeurs
    en ajoutant des astuces, des guides et des questions/réponses à ce document.
    On te remercie d'avance !

Les projets lié au MicroPython sur le BBC micro:bit comprennent :

* `Mu <https://github.com/ntoll/mu>`_ - un éditeur de code simple pour les enfants, les enseignants et les programmeurs débutants. C'est probablement la façon la plus simple de programmer en MicroPython sur le BBC micro:bit.
* `uFlash <https://uflash.readthedocs.io/en/latest/>`_ - un outil en ligne de commande pour flasher des script Python directement sur le BBC micro:bit.

.. toctree::
    :maxdepth: 2
    :caption: Tutorials

    tutorials/introduction
    tutorials/hello
    tutorials/images
    tutorials/buttons
    tutorials/io
    tutorials/music
    tutorials/random
    tutorials/movement
    tutorials/gestures
    tutorials/direction
    tutorials/storage
    tutorials/speech
    tutorials/network
    tutorials/radio
    tutorials/next

.. toctree::
   :maxdepth: 2
   :caption: API Reference

   microbit_micropython_api.rst
   microbit.rst
   accelerometer.rst
   ble.rst
   button.rst
   compass.rst
   display.rst
   filesystem.rst
   i2c.rst
   image.rst
   music.rst
   neopixel.rst
   os.rst
   pin.rst
   radio.rst
   random.rst
   speech.rst
   spi.rst
   uart.rst

.. toctree::
   :maxdepth: 2
   :caption: Developer Guide

   devguide/installation
   devguide/flashfirmware
   devguide/repl
   devguide/devfaq
   devguide/contributing

.. toctree::
   :maxdepth: 2
   :caption: Indices and tables

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
