Introduction
------------

Nous suggérons de télécharger et d'utiliser `l'éditeur mu <http://codewith.mu/>`_
pour travailler avec ces tutoriaux. Les instructions pour télécharger et installer
Mu se trouvent sur son site. Tu seras peut-être amené à installer un pilote de
périphérique selon ton système d'exploitation (les instructions sont sur le site
web).

Mu fonctionne sous Windows, OSX et Linux.

Une fois que Mu est installé, connect ton micro:bit à ton ordinateur avec un
câble USB.

Ecris ton script dans la fenêtre d'édition et click sur le bouton "Flash" pour le
transférer dans le micro:bit. Si ça ne marche pas, vérifie que ton micro:bit
apparait comme un stockage USB dans ton explorateur de fichiers.

.. toctree::
    :maxdepth: 2
    :caption: Tutoriels

    hello
    images
    buttons
    io
    music
    random
    movement
    gestures
    direction
    storage
    speech
    network
    radio
    next

Python est l'un des langages de programmation
`les plus populaires du monde <http://www.tiobe.com/index.php/content/paperinfo/tpci/index.html>`.
Tous les jours, sans le savoir, tu tuilises probablement un logiciel écrit en
Python. Toutes sortes de sociétés et d'organisations utilisent Python dans une
grande variété d'applications. Google, NASA, Bank of America, Disney, CERN,
YouTube, Mozilla, The Guardian - la liste continue et couvre tous les secteurs
de l'économie, des sciences et des arts.

Par exemple, te rappeles-tu de l'annonce de 'la découverte des ondes gravitationelles <http://www.bbc.co.uk/news/science-environment-35552207>`_?
Les instruments utilisés pour faire les mesures étaient controllés `avec Python <https://www.reddit.com/r/IAmA/comments/45g8qu/we_are_the_ligo_scientific_collaboration_and_we/czxnlux>`_.

Dit simplement, si tu enseigne ou apprend Python, tu développes un talent de grande
valeur qui s'applique à tous les domaines de l'activté humaine.

L'un de ces domaines est l'appareil micro:bit de la BBC. Il embarque une version
de Python appelée MicroPython qui est destinée à tourner sur de petits ordinateurs
comme le BBC micro:bit. C'est une implémentation complète de Python 3 donc lorsque
tu passeras sur d'autres ordinateurs (comme programmer en Python sur une Raspberry
 Pi) tu utiliseras exactement le même langage.

MicroPython n'inclut pas toutes les bibliothèques standards qui sont présente
dans la version "habituelle" de Python. Néanmoins, nous avons créé un module
spécial ``microbit`` dans MicroPython qui te permet de controller l'appareil.

Python et MicroPython sont des logiciels libres. Cela ne signifie pas seulement
qu'il n'y a rien a payer pour utiliser Python, mais aussi que tu es libre de
contribuer à la communauté Python. Cela peut être fait sous la forme de code,
de documentation, de rapports de bugs, gérer un groupe ou écrire des tutoriels
(comme celui-ci). En fait, toutes les ressources Python pour le BBC micro:bit ont
été créées par une équipe internationale de bénévoles travaillant sur leur temps
libre.

Ces leçons présentent MicroPython et le BBC micro:bit en étapes faciles à suivre.
N'hésite pas à les adopter et à les adapter pour des leçons en classe, ou peut-être
simplement à les suivre par toi-même chez toi.

Tu y arriveras mieux si tu explores, expérimentes et joues. Tu ne peux pas casser
un BBC micro:bit avec un code incorrect. Lance-toi !



Un mot d'avertissement : *tu vas souvent rater*, et ce n'est pas grave. **L'échec
est le moyen qu'on les bon développeurs de logiciel d'apprendre**. Ceux parmi
nous qui développent des logiciels s'amusent beaucoup à rechercher les bugs et à 
éviter la répétition des erreurs.

If in doubt, remember the Zen of MicroPython::

En cas de doute, rappele-toi la maxime Zen de MicroPython::

    Code,
    Bidouille,
    Moins est plus,
    Reste simple,
    Petit, c'est beau,

    Sois courageux! Casse les trucs! Apprend et amuse-toi!
    Exprime-toi avec MicroPython.

    Bon bidouillage! :-)

Bonne chance!
