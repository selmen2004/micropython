Réseau
-------

Il est possible de connecter des appareil pour qu'ils s'envoyent et recevoivent
des messages l'un de l'autre.

Travailler en réseau est difficile et c'est ce que montre le programme décrit
plus bas. Cependant, le bon côté de ce projet est qu'il contient tous les aspects
classique de la programmation en réseau que tu as besoin de connaître. Il est
aussi remarquablement simple et amusant.

Mais d'abord, décrivons le cadre...

connexion
++++++++++

Imagine un réseau comme une série de couches. Tout en bas il y a les aspect les
plus fondamentaux de la communication: il doit y avoir des sortes de chemins pour
qu'un signal se rende d'un appareil à un autre. Parfois ceci est obtenu par des
connexion radio, mais dans cet exemple nous allons simplement utiliser deux câbles.

.. image:: network.png

C'est sur cette base solide que nous allons construire toutes les autres couches
de notre *pile réseau*.

Comme le schéma le montre, les micro:bits bleu et rouge sont connectés par des
pinces crocodile. Ils utilisent tous les deux le pin 1 pour la sortie et le pin 2
pour l'entrée. La sortie de l'un des deux appareils est connectée à l'entrée de
l'autre. C'est un peu comme savoir dans quel sens tenir un combiné de téléphone -
un côté a un microphone (l'entrée) et l'autre un haut-parleur (la sortie).
L'enregistrement de ta voix par ton microphone est retransmise par le haut-parleur
de ton interlocuteur. Si tu tiens le téléphone à l'envers, tu obtiendra un
résultat bizarre!

C'est exactement la même chose dans cet exemple : tu dois connecter les câbles
correctement!

Signal
++++++

La couche suivante de notre *pile réseau* est le signal. Souvent elle dépendra
des caractéristiques de la connexion. Dans notre exemple il s'agit simplement de
signaux digitaux on et off envoyés au travers des câbles par les pins d'E/S.

Si tu te rappelles bien, il est possible d'utiliser les pins d'E/S comme ça::

    pin1.write_digital(1)  # bascule le signal sur on
    pin1.write_digital(0)  # bascule le signal sur off
    input = pin2.read_digital()  # lit la valeur du signal (soit 1 soit 0)

L'étape suivante implique la description de la façon de gérer un signal. Pour cela
nous avons besoin d'un...

Protocole
+++++++++

Si tu rencontres la Reine un jour, il y a des attentes sur le comportement que tu
devras adopter. Par exemple, lorsqu'elle arrive tu dois faire une révérence, si
elle te tend la main, serre la poliement, adresse-toi à elle en disant "votre
majesté" et après "madame" et ainsi de suite. Cet ensemble de règle s'appelle le
protocole royal. Un protocole explique comment se comporter dans une situation
particulière (comme celle de ta rencontre avec la Reine). Un protocole est
pré-défini pour s'assurer que tout le monde comprend ce qu'il se passe avant
qu'une situation donnée ne survienne.

.. image:: queen.jpg

C’est pour cette raison que nous définissons et utilisons des protocoles de communication
pour les messages au travers d'un réseau informatique. Les ordinateurs doivent
s'entendre avant de savoir comment envoyer et recevoir des messages. Le
protocole le plus connu est peut-être le protocole de transfert hypertexte (HTTP)
utilisé par le World Wide Web.

Un autre protocole célèbre pour l’envoi de messages (qui précède les ordinateurs)
est le code Morse. Il définit comment envoyer des messages basés sur des
caractères via des signaux on / off de longues ou courtes durées. Souvent, ces
signaux sont joués comme des bips. Les longues durées sont appelées des tirets
(`` -``) alors que les durées courtes sont des points (`` .``).
En combinant des tirets et des points, Morse définit un moyen d'envoyer des
caractères.Par exemple, voici comment est défini l'alphabet Morse standard:

    .-    A     .---  J     ...   S     .----  1      ----.  9
    -...  B     -.-   K     -     T     ..---  2      -----  0
    -.-.  C     .-..  L     ..-   U     ...--  3
    -..   D     --    M     ...-  V     ....-  4
    .     E     -.    N     .--   W     .....  5
    ..-.  F     ---   O     -..-  X     -....  6
    --.   G     .--.  P     -.--  Y     --...  7
    ....  H     --.-  Q     --..  Z     ---..  8
    ..    I     .-.   R

Compte tenu du tableau ci-dessus, pour envoyer le caractère "H" le signal est
allumé quatre fois pendant une courte durée, indiquant quatre points (`` .... ``).
Pour la lettre "L" le signal est également allumé quatre fois, mais le deuxième
signal a un durée plus longue (`` .- .. ``).

Evidemment, le timing du signal est important: il faut pouvoir distinguer un point
d'un tiret. C'est un autre point d'un protocole, se mettre d'accord sur de
telles choses afin que toutes les mises en œuvre du protocole fonctionnent avec
tout le monde. Dans cet exemple nous allons juste dire que:

* Un signal d'une durée inférieure à 250 millisecondes est un point.
* Un signal d'une durée de 250 millisecondes à moins de 500 millisecondes est un tiret.
* Toute autre durée de signal est ignorée.
* Une pause / trou supérieure à 500 millisecondes dans le signal indique la fin d’un caractère.

De cette manière, l’envoi d’une lettre "H" est défini comme quatre signaux "on"
pas plus long que  250 millisecondes chacun, suivi d'une pause supérieure à
500 millisecondes (indiquant la fin du caractère).

Message
+++++++

Nous sommes enfin à un stade où nous pouvons construire un message - un message
qui signifie quelque chose pour nous les humains. C'est la couche supérieure de
notre *pile réseau*

En utilisant le protocole défini ci-dessus, je peux envoyer la séquence de
signaux suivante au travers du câble physique à l'autre micro:bit ::

    ...././.-../.-../---/.--/---/.-./.-../-..

Peux-tu trouver ce qu'il dit ?

Application
+++++++++++

C'est très bien d'avoir une pile réseau, mais vous avez également besoin d'un
moyen d'interagir avec elle - une forme d'application pour envoyer et recevoir
des messages. Bien que HTTP soit intéressant * la plupart des gens * ne le
savent pas et laissent leur navigateur Web le gèrer - la *pile réseau *
sous-jacente du World Wide Web est cachée (comme il se doit).

Alors, quelle sorte d'application devrions-nous écrire pour le micro BBC: bit?
Comment devrait-elle fonctionner, du point de vue de l'utilisateur?

De toute évidence, pour envoyer un message, vous devez pouvoir saisir des points
et des tirets (nous pouvons utiliser le bouton A pour cela). Si nous voulons
voir le message que nous avons envoyé ou reçu, nous devrions être en mesure de
déclencher le défilement de l'affichage (nous pouvons utilisez le bouton B pour
cela). Enfin, ceci étant du code Morse, si un haut-parleur est raccordé, nous
devrions être en mesure de jouer les bips comme une forme de rétroaction sonore
pendant que l'utilisateur entre son message.

Le Résultat Final
+++++++++++++++++

Voici le programme, dans toute sa splendeur et annoté avec plein de commentaires
pour que vous puissiez voir ce qui se passe ::

    from microbit import *
    import music

    # Une table de correspondance du code Morse.
    MORSE_CODE_LOOKUP = {
        ".-": "A",
        "-...": "B",
        "-.-.": "C",
        "-..": "D",
        ".": "E",
        "..-.": "F",
        "--.": "G",
        "....": "H",
        "..": "I",
        ".---": "J",
        "-.-": "K",
        ".-..": "L",
        "--": "M",
        "-.": "N",
        "---": "O",
        ".--.": "P",
        "--.-": "Q",
        ".-.": "R",
        "...": "S",
        "-": "T",
        "..-": "U",
        "...-": "V",
        ".--": "W",
        "-..-": "X",
        "-.--": "Y",
        "--..": "Z",
        ".----": "1",
        "..---": "2",
        "...--": "3",
        "....-": "4",
        ".....": "5",
        "-....": "6",
        "--...": "7",
        "---..": "8",
        "----.": "9",
        "-----": "0"
    }


    def decode(buffer):
        # Essaie d'obtenir une correspondance entre le contenu du buffer et le
        # code Morse. Si il n'y en a pas, renvoie juste un point.
        return CODE_MORSE_CORRESPONDANCE.get(buffer, '.')


    # Image correspondant à un POINT.
    POINT = Image("00000:"
                "00000:"
                "00900:"
                "00000:"
                "00000:")


    # Image correspondant à un TIRET.
    TIRET = Image("00000:"
                 "00000:"
                 "09990:"
                 "00000:"
                 "00000:")


    # Pour créer un POINT tu dois maintenir le bouton pendant moins de 250ms
    SEUIL_POINT = 250
    # Pour créer un TIRET tu dois maintenir le bouton pendant moins de 500ms
    SEUIL_TIRET = 500


    # Contient le signal Morse entrant.
    buffer = ''
    # Contient le Morse traduit en caractères.
    message = ''
    # Le temps depuis lequel l'appareil a ttendu le prochain appui sur une touche.
    debut_attente = running_time()


    # Met l'appareil dans une boucle pour attendre et réagir aux appuis sur un
    # bouton
    while True:
        # Work out how long the device has been attente for a keypress.
        # Détermine le temps que l'appareil a attendu l'appui
        attente = running_time() - debut_attente
        # Réinitialise l'horodatage de temp_presse
        temps_touche_presse = None
        # Si le bouton A est mainteu appuyeé alors...
        while button_a.is_pressed():
            # Emet un bip - c'est du code Morse tu sais ;-)
            music.pitch(880, 10)
            # Met le pin1 (sortie) sur "on"
            pin1.write_digital(1)
            # ...et si il n'y a pas encor de  temps_touche_presse alors on le met maintenant!
            if not temps_touche_presse:
                temps_touche_presse = running_time()
        # Alternativment, si le pin2 (input) reçoit un signal, on fait comme  si
        # c'était un appui sur le bouton A
        while pin2.read_digital():
            if not temps_touche_presse:
                temps_touche_presse = running_time()
        # On récupère l'heure actuelle et on l'appelle temps_touche_haute
        temps_touche_haute = running_time()
        # Met le pin1 (sortie) sur "off"
        pin1.write_digital(0)
        # Si il y a un temps_touche_presse (créé lorsque le bouton A a été pressé
        # la  première fois).
        if temps_touche_presse:
            # ...détermine depuis combien de temps il est appuyé
            duree = temps_touche_haute - temps_touche_presse
            # Si la durée est inférieur à la durée maximale d'un DOT...
            if duree < SEUIL_POINT:
                # ... alors ajoute un point au buffer contenant le code Morse entrant
                # et montre un point sur l'affichage..
                buffer += '.'
                display.show(POINT)
            # Sinon, si la durée  est inférieur à la durée maximale d'un TIRET...
            # (mais plus longue que celle d'un POINT ~qui a été géré avant)
            elif duree < SEUIL_TIRET:
                # ... alors ajoute un tiret au buffer contenant le code Morse entrant
                # et affiche-le.
                buffer += '-'
                display.show(TIRET)
            # Sinon, toutes les autres durée d'appui sont ignorées (ce n'est pass
            # nécessaire mais on le met pour la compréhension)
            else:
                pass
            # L'appui sur le bouton a été géré, on peut réinitialiser le temps
            # d'attente pour le prochain appui.
            debut_attente = running_time()

        # Sinon, il n'y a pas eu d'appui pendant ce cycle de la boucle, donc il
        # faut vérifier qu'il n'y a pas eu de pause indiquant la fin du
        # code Morse du caractère entrant. La pause doit être plus longue que
        # la durée du code d'un TIRET.
        elif len(buffer) > 0 and attente > SEUIL_TIRET:
            # Le buffer n'est pas vide et on a atteitn la fin du code donc...
            # il faut décoder le buffer entrant.
            character = decode(buffer)
            # Puis réinitialiser le buffer
            buffer = ''
            # Afficher le caractère décodé
            display.show(character)
            # et ajouter le caractère au message.
            message += character
        # Enfin, si le bouton B a été appuyé pendant tout ce temps là...
        if button_b.was_pressed():
            # ... affiche le message,
            display.scroll(message)
            # et réinitialise-le  (prêt pour un nuoveau message).
            message = ''

Comment l'améliorerais-tu? Peux-tu changer la définition d'un point et d'un tiret
pour que utilisateurs rapides de code Morse puissent l'utiliser? Que se
passe-t-il si les deux appareils envoient en même temps? Que pourriez-vous faire
pour gérer cette situation?

.. footer:: The image of Queen Elizabeth II is licensed as per the details here: https://commons.wikimedia.org/wiki/File:Queen_Elizabeth_II_March_2015.jpg
