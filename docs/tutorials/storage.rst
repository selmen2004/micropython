Stockage
--------

Parfois, vous devez stocker des informations utiles. Ces informations sont stockées sous la forme
données: représentation des informations (sous forme numérique lorsqu’elles sont stockées sur
des ordinateurs). Si vous stockez des données sur un ordinateur, elles devraient persister, même si vous
éteignez et rallumez l'appareil.

Heureusement, MicroPython sur le micro: bit vous permet de le faire avec un très simple
système de fichiers. En raison des contraintes de mémoire **, il y a environ 30k de
mémoire disponible ** sur le système de fichiers.

.. warning::

    Le système de fichiers micropython ne doit pas être confondu
    avec le mode de stockage de masse micro: bit qui présente l’appareil comme une clé USB.
    Le mode de stockage de masse n’est conçu que pour la copie d’un fichier HEX.
    voir les fichiers que vous créez en utilisant le système de fichiers apparaissant sur le lecteur MICROBIT.

Qu'est-ce qu'un système de fichiers?

C'est un moyen de stocker et d'organiser les données de manière persistante - toutes les données
stockés dans un système de fichiers doivent survivre aux redémarrages du périphérique. Comme le nom
suggère, les données stockées sur un système de fichiers sont organisées en fichiers.

.. image :: files.jpg

Un fichier informatique est une ressource numérique nommée qui est stockée sur un système de fichiers.
Ces ressources contiennent des informations utiles sous forme de données. C'est exactement comme ça
fichier papier fonctionne. C'est une sorte de conteneur nommé qui contient des informations utiles.
information. Habituellement, les fichiers papier et numériques sont nommés pour indiquer
ils contiennent. Sur les ordinateurs, il est courant de terminer un fichier avec un fichier `` .something``
suffixe. Habituellement, le "quelque chose" indique quel type de données est utilisé pour
représenter l'information. Par exemple, `` .txt`` indique un fichier texte,
`` .jpg`` une image JPEG et des données audio `` .mp3`` encodées au format MP3.

Certains systèmes de fichiers (tels que celui présent sur votre ordinateur portable ou votre PC) vous permettent de
Organisez vos fichiers dans des répertoires: des conteneurs nommés qui regroupent les fichiers associés.
et sous-répertoires ensemble. Cependant, * le système de fichiers fourni par MicroPython
est un système de fichiers à plat *. Un système de fichiers à plat n'a pas de répertoires - tous
vos fichiers sont simplement stockés au même endroit.

Le langage de programmation Python contient des moyens faciles à utiliser et puissants pour
travailler avec le système de fichiers d'un ordinateur. MicroPython sur les implémentations micro: bit
un sous-ensemble utile de ces fonctionnalités pour faciliter la lecture et l'écriture de fichiers sur
le périphérique, tout en assurant la cohérence avec les autres versions de Python.

.. Attention::

    Le clignotement de votre micro: bit détruira TOUTES VOS DONNEES car il réécrit tout
    la mémoire flash utilisée par l'appareil et le système de fichiers est stockée dans le
    mémoire flash.

    Cependant, si vous éteignez votre appareil, les données resteront intactes jusqu'à ce que
    soit vous le supprimez, soit le flash de l'appareil.

Sésame ouvre-toi
+++++++++++

La lecture et l’écriture d’un fichier sur le système de fichiers est réalisée par le paramètre `` open``
une fonction. Une fois qu'un fichier est ouvert, vous pouvez le faire jusqu'à ce que vous le fermiez.
(analogue à la façon dont nous utilisons les fichiers papier). Il est essentiel de fermer un fichier
alors MicroPython sait que vous en avez fini.

Le meilleur moyen de s'en assurer est d'utiliser l'instruction `` with`` comme ceci:

    avec open ('story.txt') en tant que mon_fichier:
        content = mon_fichier.read ()
    imprimer (contenu)

L’instruction `` with`` utilise la fonction `` open`` pour ouvrir un fichier et l’affecter.
à un objet. Dans l'exemple ci-dessus, la fonction `` open`` ouvre le fichier nommé
`` story.txt`` (évidemment un fichier texte contenant une histoire).
L'objet utilisé pour représenter le fichier dans le code Python est appelé
`` mon_fichier``. Par la suite, dans le bloc de code indenté sous le caractère `` with``
déclaration, l’objet `` my_file`` est utilisé pour `` read () `` le contenu de la
fichier et l'assigne à l'objet `` content``.

Voici le point important, * la prochaine ligne contenant l'instruction * `` print`` *
n'est pas en retrait *. Le bloc de code associé à l'instruction `` with`` est uniquement
la seule ligne qui lit le fichier. Une fois le bloc de code associé à la
`` avec`` est fermé, alors Python (et MicroPython) sera automatiquement
fermez le fichier pour vous. C'est ce qu'on appelle la gestion du contexte et le `` open``
function crée des objets qui sont des gestionnaires de contexte pour les fichiers.

En termes simples, la portée de votre interaction avec un fichier est définie par le code
bloc associé à l'instruction `` with`` qui ouvre le fichier.

Confus?

Ne sois pas. Je dis simplement que votre code devrait ressembler à ceci:

    avec open ('some_file') en tant que some_object:
        # Faites des choses avec some_object dans ce bloc de code
        # associé à l'instruction with.

    # Quand le bloc est fini, alors MicroPython
    # ferme automatiquement le fichier pour vous.

Comme un fichier papier, un fichier numérique est ouvert pour deux raisons: lire son
contenu (comme démontré ci-dessus) ou d'écrire quelque chose dans le fichier. Le défaut
mode est de lire le fichier. Si vous voulez écrire dans un fichier, vous devez en informer le
`` open`` fonctionne de la manière suivante ::

    avec open ('hello.txt', 'w') en tant que mon_fichier:
        my_file.write ("Hello, World!")

Notez que l'argument `` 'w'`` est utilisé pour définir l'objet `` mon_fichier`` en écriture
mode. Vous pouvez également passer un argument `` 'r'`` pour définir l'objet fichier à lire
mode, mais comme il s’agit du mode par défaut, il est souvent désactivé.

L'écriture de données dans le fichier se fait avec (vous l'avez deviné) `` write``
méthode qui prend la chaîne que vous voulez écrire dans le fichier en tant qu'argument. Dans
l'exemple ci-dessus, j'écris le texte "Hello, World!" dans un fichier appelé
"hello.txt".

Simple!

.. Remarque::

    Lorsque vous ouvrez un fichier et écrivez (peut-être plusieurs fois pendant que le fichier est
    dans un état ouvert) vous écrivez SUR le contenu du fichier si
    existe déjà.

    Si vous souhaitez ajouter des données à un fichier, vous devez d’abord le lire, enregistrez le
    contenu quelque part, fermez-le, ajoutez vos données au contenu puis ouvrez
    à écrire à nouveau avec le contenu révisé.

    Bien que ce soit le cas dans MicroPython, Python "normal" peut s'ouvrir
    fichiers à écrire en mode "append". Que nous ne pouvons pas faire cela sur le micro: le bit est
    résultat de la mise en œuvre simple du système de fichiers.

OS SOS
++++++

En plus de lire et d’écrire des fichiers, Python peut les manipuler. Vous
certainement besoin de savoir quels fichiers sont sur le système de fichiers et parfois
vous devez aussi les supprimer.

Sur un ordinateur classique, c’est le rôle du système d’exploitation (comme Windows,
OSX ou Linux) pour gérer cela au nom de Python. Cette fonctionnalité est faite
disponible en Python via un module appelé `` os``. Depuis MicroPython ** est ** le
système d'exploitation, nous avons décidé de garder les fonctions appropriées dans le `` os``
module de cohérence afin que vous sachiez où les trouver lorsque vous utilisez "régulière"
Python sur un appareil comme un ordinateur portable ou Raspberry Pi.

Pour l’essentiel, vous pouvez effectuer trois opérations liées au système de fichiers:
fichiers, supprimez un fichier et demandez la taille d’un fichier.

Pour lister les fichiers sur votre système de fichiers, utilisez la fonction `` listdir``. Il
renvoie une liste de chaînes indiquant les noms de fichier des fichiers du fichier
système::

    importation os
    mes_fichiers = os.listdir ()

Pour supprimer un fichier, utilisez la fonction `` remove``. Il faut une chaîne représentant
le nom du fichier que vous voulez supprimer en argument, comme ceci:

    importation os
    os.remove ('filename.txt')

Enfin, il est parfois utile de connaître la taille d’un fichier avant de le lire dans
il. Pour cela, utilisez la fonction `` size``. Comme la fonction `` remove``, elle
prend une chaîne représentant le nom du fichier dont vous voulez
savoir. Il retourne un entier (nombre entier) vous indiquant le nombre d'octets
fichier prend ::

    importation os
    taille_fichier = os.size ('a_big_file.txt')

C'est très bien d'avoir un système de fichiers, mais si on veut mettre ou obtenir
fichiers sur ou hors de l'appareil?

Il suffit d’utiliser l’utilitaire `` microfs``!

Transfert de fichier
++++++++++++++

Si vous avez installé Python sur l’ordinateur que vous utilisez pour programmer votre BBC
micro: bit, vous pouvez utiliser un utilitaire spécial appelé `` microfs`` (abrégé en
`` ufs`` lors de son utilisation en ligne de commande). Instructions complètes pour l'installation
et en utilisant toutes les fonctionnalités de microfs peuvent être trouvés
`dans sa documentation <https://microfs.readthedocs.io>` _.

Néanmoins, il est possible de faire la plupart des choses dont vous avez besoin avec seulement quatre
commandes simples ::

    $ ufs ls
    story.txt

La sous-commande `` ls`` répertorie les fichiers du système de fichiers (elle porte le nom suivant).
la commande Unix commune, `` ls``, qui remplit la même fonction).

::

    $ ufs get story.txt

La sous-commande `` get`` récupère un fichier du micro: bit connecté et l'enregistre
dans votre emplacement actuel sur votre ordinateur (il est nommé d'après le `` get``
commande qui fait partie du protocole de transfert de fichier commun [FTP] qui sert le
même fonction).

::

    $ ufs rm story.txt

La sous-commande `` rm`` supprime le fichier nommé du système de fichiers de la
connecté micro: bit (il tire son nom de la commande Unix commune, `` rm``, qui
remplit la même fonction).

::

    $ ufs a mis story2.txt

Enfin, la sous-commande `` put`` place un fichier de votre ordinateur sur le
périphérique connecté (il est nommé d'après la commande `` put`` qui fait partie de FTP qui
remplit la même fonction).

Principalement main.py
+++++++++++++++

Le système de fichiers a aussi une propriété intéressante: si vous venez de flasher le
MicroPython runtime sur le périphérique puis quand il démarre, il attend simplement
pour quelque chose à faire. Cependant, si vous copiez un fichier spécial appelé `` main.py``
sur le système de fichiers, au redémarrage du périphérique, MicroPython exécute le
contenu du fichier `` main.py``.

De plus, si vous copiez d’autres fichiers Python sur le système de fichiers, vous pouvez
`` import`` les comme tout autre module Python. Par exemple, si vous aviez
un fichier `` hello.py`` qui contenait le code simple suivant:

    def say_hello (name = "World"):
        retourne "Bonjour, {}!". format (nom)

... vous pouvez importer et utiliser la fonction `` say_hello`` comme ceci ::

    depuis l'affichage d'importation microbit
    de bonjour dire

    display.scroll (say_hello ())

Bien sûr, il en résulte le texte "Hello, World!" défiler à travers le
afficher. Le point important est qu’un tel exemple est divisé entre deux
Les modules Python et l'instruction `` import`` sont utilisés pour partager le code.

.. Remarque::
    Si vous avez flashé un script sur le périphérique en plus du MicroPython
    puis MicroPython ignorera `` main.py`` et lancera votre logiciel de gestion intégré.
    script à la place.

    Pour flasher uniquement le runtime de MicroPython, assurez-vous simplement que le script
    peut avoir écrit dans votre éditeur a zéro caractères. Une fois flashé
    vous pourrez copier un fichier `` main.py``.

.. footer :: L'image des fichiers papier est utilisée sous licence Creative Commons et est disponible ici: https://www.flickr.com/photos/jenkim/2270085025
