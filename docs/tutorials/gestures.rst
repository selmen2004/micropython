Gestes
--------

L'effet collatéral le plus intéressant d'un accélèromètre est la détection des
gestes.

MicroPython est capable de reconnaître les gestes suivants:
- haut-> ``up``
- bas -> ``down``
- gauche -> ``left``
- droite -> ``right``
- face en haut -> ``face up``
- face en bas -> ``face down``
- chute libre ->  ``free fall``
- accélération correspondant à 3, 6 ou 8 fois celle de la chute libre -> ``3g``
,  ``6g`` ou ``8g``
- secousse -> ``shake``
Les gestes sont toujours représentés par des chaînes de caractères.

Pour obtenir le geste effectué, on utilise la méthode ``accelerometer.current_gesture``.
Son résultats est l'un des noms de gestes listés ci-dessus. Par exemple, ce
programme rendra votre appareil heureux seulement lorsque sa face est tournée
vers le haut ::

    from microbit import *

    while True:
        geste = accelerometer.current_gesture()
        if geste == "face up":
            display.show(Image.HAPPY)
        else:
            display.show(Image.ANGRY)

Encore une fois, puisque nous voulons que l'appareil réagisse à des circomstances
changeantes, nous utilisons une voucle ``while``. A l'intérieur du coprs de la
boucle, le geste est lu et stocké dans ``geste``. L'instruction conditionnelle
``if`` verifie si ``geste`` est égal à ``face up`` (Python utilise ``==`` pour
tester une égalité car un simple signe égal ``=`` est utilisé pour l'affectation -
tout comme nous affectons le geste lu à l'objet ``geste``). Si le geste est égal
à ``face up`` alors on utilise l'affichage pour montrer un visage heureux. Sinon,
l'appareil a l'air mécontent.

Magic-8
+++++++

Une balle Magic-8 est un jouet inventé dans les année 1950. L'idée est de lui poser
une question à laquelle on peut répondre oui ou non, de la secouer et d'attendre
qu'elle nous révèle la vérité. C'est plutôt facile à programmer::

    from microbit import *
    import random
    reponses = [
        "C'est certain",
        "C'est décidément ainsi",
         "Sans aucun doute",
         "Oui définitivement",
         "Vous pouvez compter dessus",
         "Comme je le vois, oui",
         "Probablement",
         "ça semble bien",
         "Oui",
         "Les signes pointent vers Oui",
         "Réponse brumeuse, essaye encore",
         "Demander à nouveau plus tard",
         "Mieux vaut ne pas te le dire maintenant",
         "Je ne peux pas prédire maintenant",
         "Concentre-toi et demande à nouveau",
         "Ne compte pas dessus"
         "Ma réponse est non",
         "Mes sources disent non",
         "ça ne semble pas si bon",
         "Très douteux",
    ]
    
    while True:
        display.show("8")
        if accelerometer.was_gesture("shake"):
            display.clear()
            sleep(1000)
            display.scroll(random.choice(reponses))

La plus grande partie du programme une liste nommée ``réponses``. Le jeu se
trouve dans la boucle ``while`` à la fin.

L'état  par défaut du jeu est l'affichage du caractère ``"8"``. Le programme doit
détecter si le micro:bit a été secoué. La méthode ``was_gesture`` utilise son
argument (dans ce cas ``shake`` puique l'on veut détecter une secousse) pour
retourner un ``True`` ou un ``False``. Si l'appareil a été secoué, l'instruction
``if`` exécutera le bloc de code dans lequel l'écran est effacé pendant une seconde
 (de façon à ce que l'appareil semble réfléchir à ta question) et affiche une
 réponse choisie au hasard.

Pourquoi ne pas lui demander si c'est le meilleurs programme jamais écrit ? Que
pourrais-tu faire pour "tricher" et faire en sorte que la réponse soit toujours
positive ou négative ? (Indice : utilise les boutons.)
