---
title: Exercices en plus (TP4)
---

!!! info "Objectifs pédagogiques"

    À l’issue de ce TP, l’étudiant sera capable de :
    
    - Renforcer la maîtrise des redirections et tubes dans le shell.
    - Utiliser les filtres textuels classiques (`grep`, `sort`, `cut`, `uniq`, `tr`, `head`, `tail`, etc.).
    - Enchaîner plusieurs commandes avec des redirections et des tubes.
    - Appliquer des filtres sur des fichiers textuels en combinant des options.
    - Manipuler efficacement les entrées/sorties dans des scénarios concrets.
    - Approfondir l’utilisation de `grep` pour rechercher dans des arborescences de fichiers.
    - Apprendre à extraire des informations spécifiques de fichiers système (`/etc`, `/usr/include`, etc.).


!!! info "Indications"
    Les exercices suivants sont des exercices supplémentaires pour vous entraîner et voir d'autres utilisations des tubes et des redirections. 

!!! tip "Barème d’interprétation des exercices"

    > 📚 = Facile, 📚📚 = Moyenne, 📚📚📚 = Élevée 

!!! tip "Filtres textuels"
    Les *filtres textuel* sont des commandes qui lisent ou peuvent lire depuis leur entrée standard et écrivent des données modifiées sur leur sortie standard. 

    En voici quelques-uns parmi les plus courants :

     - `head` : affiche les premières lignes de son entrée ;
     - `tail` : affiche les dernières lignes de son entrée. Avec l’option -f (pour follow, continuer à afficher la fin du fichier quand il est mis à jour) c’est l’une des commandes préférées des administrateurs systèmes ;
     - `grep` : une des commandes les plus connues, affiche des lignes correspondant à une chaîne, ou plus généralement une expression rationnelle dans son entrée ;
     - `cut` : sélectionne des champs ou des caractères dans chaque ligne de l’entrée standard ;
     - `sort` : trie son entrée standard suivant des critères.
     - `tr` : remplace des caractères dans son entrée standard.
     - `uniq` : supprime les lignes consécutives identiques dans son entrée standard.
  
  ---

### Exercice 1 : Frère Jacques 📚

1. Créer un fichier `fj` contenant ces lignes :
    ```bash
    Frère Jaques, 
    Frère Jacques,                    
    Dormez-vous,
    Dormez-vous,
    Sonnez les matines,
    Sonnez les matines !
    Ding !
    Ding ! 
    Dong !
    ```
    avec la commande `echo` (**le caractère `<newline>` correspond à la touche entrée de votre clavier**):
    ```bash
    $ echo 'Frère Jaques,<newline> 
    > Frère Jacques,<newline>                     
    > Dormez-vous,<newline> 
    > Dormez-vous,<newline> 
    > Sonnez les matines,<newline> 
    > Sonnez les matines !<newline> 
    > Ding !<newline> 
    > Ding !<newline> 
    > Dong !' > fj
    ```
2. Testez ensuite les commandes suivantes et observez leur résultats:
    ```bash
    $ cat fj 
    $ head fj
    $ tail fj
    $ head -n 2 fj
    $ tail -n 3 fj
    $ grep "Dormez" fj
    $ grep -v "Dormez" fj
    $ grep "dormez" fj
    $ grep -i "dormez" fj
    $ sort fj 
    $ uniq fj
    $ cut -c 1 fj
    $ cut -c 2 fj
    $ cut -c 1-3 fj
    $ cut -d ' ' -f 1 fj
    $ cut -d ' ' -f 1,2 fj
    ```
    - Où sont affichés les résultats ?
    - À quoi servent les options `-n` de `head` et `tail` ? 
    - À quoi sert l'option `-v` de `grep` ? À quoi sert l'option `-i` de `grep` ?
    - À quoi servent les options `-c` et `-d` de `cut` ?


### Exercice 2 : Trier les fichiers 📚📚📚

!!! tip "Nom de base"
    Le nom de base d'un fichier est le nom du fichier sans son extension. Par exemple le nom de base du fichier `/usr/include/stdio.h` est `stdio`.

Dans cet exercice, nous voudrions afficher sur le terminal le nom de base des 10 fichiers les plus légers (en taille en octets) parmi les fichier `.h ` du répertoire `/usr/include`.

En utilisant les commandes `wc`, `sort`, `cut`, `head` (ou éventuellement `tail`), et les redirections par tube, écrivez une commande qui affiche le nom de base des 10 fichiers les plus légers parmi les fichiers `.h` du répertoire `/usr/include`.

!!! info "Indication"

    - L'option `-c` de `wc` vous donne le nombre d'octets d'un fichier.
    - L'option `-n` de `sort` vous permet de trier les lignes d'un fichier par ordre numérique.
    - L'option `-d` de `tr` supprime les caractères reçus en premiers argument au lieu de les remplacer.

Si vous avez installé `gcc`, vous devriez avoir :
```bash
pool
wait
syslog
syscall
lastlog
termio
stab
memory
re_comp
alloca
```
### Exercice 3 : Plus sur `grep` 📚📚

!!! tip "Passer un répertoire en argument de `grep`"
    
    - L'option `-r` de `grep` permet de passer un répertoire en argument. Et lui demande de chercher dans tous les fichiers de ce répertoire.
    - L'option `-l` de `grep` permet de n'afficher que le nom des fichiers qui contiennent la chaîne recherchée.

En utilisant `grep` et éventuellement d'autres commandes, trouvez une ligne de commande qui permet de:

1. Afficher la valeur de `RAND_MAX` (c'est une constante de la librairie standard de C). 
2. Afficher le chemin absolu des fichiers qui contiennent de la chaîne `127.0.0.1` dans les fichiers de `/etc`.
3. Afficher uniquement le nom des fichiers qui contiennent de la chaîne `127.0.0.1` dans les fichiers de `/etc`. (indice : il existe une commande qui s'appelle `rev`).
4. Affiche le chemin du répertoire personnel de l'utilisateur `games`.