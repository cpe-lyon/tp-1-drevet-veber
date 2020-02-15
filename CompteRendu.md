# TP1 - Compte-Rendu

## Exercice 2 - Prise en main de l’interpréteur de commandes

### Manuel

1. \> `man which`
<br>La commande `which` permet de "localiser" une commande : elle renvoie le chemin des fichiers qui seront exécutés si l'on entrait la commande.
<br>Par exemple : `which ping` renvoie `/usr/bin/ping`.

2. \> `man which`
\> `/option`
<br>Cela va surligner toutes les occurences de `option` dans la page de manuel.

3. Touche *q*.

4. \> `man 6 intro`
<br>La section 6 concerne les jeux et les "petits programmes amusants" du système.

### Navigation dans l'arborescence des fichiers

1. \> `cd /var/log`

2. \> `cd ..`

3. \> `cd`

4. \> `cd -`

5. \> `cd root`
<br>`Permision denied`
<br>Nous n'avons pas l'autorisation d'y accéder.

6. \> `sudo cd root`
<br>`sudo: cd: command not found`
<br>La commande `sudo cd` n'existe pas car `cd` est une commande interne, or, `sudo` ne fonctionne qu'avec des commandes externes.

7. \> `cd`
<br>\> `mkdir Dossier1 Dossier2`
<br>\> `cd Dossier1`
<br>\> `touch Fichier1`
<br>\> `cd ../Dossier2`
<br>\> `mkdir Dossier2.1 Dossier2.2`
<br>\> `cd Dossier2.2`
<br>\> `touch Fichier2 Fichier3`

8. \> `rm Dossier1/Fichier1`
<br>\> `rm Dossier1`
<br>`rm: cannot remove 'Dossier1': Is a directory`
<br>Dossier1 est considéré comme un dossier : on doit utiliser une autre commande pour le supprimer.

9. \> `rmdir Dossier1` (ou encore `rm -r Dossier1`)

10. \> `rmdir Dossier2`
<br>`rmdir: failed to remove 'Dossier2': Directory not empty`
<br>Pour le supprimer, il faut d'abord vider ce dossier.

11. \> `rm -r Dossier2`

### Commandes importantes

1. \> `date`
<br>`mardi 11 février 2020, 09:33:00 (UTC+0000)`
<br>La commande `time` va afficher le temps d'exécution d'une commande (par exemple `time date`).

2. \> `ls`
<br>*rien*
<br>\> `la`
<br>`.bash_history .bash_logout [...]`
<br>Ce sont des fichiers cachés.

3. \> `where ls`
<br>`usr/bin/ls`

4. \> `ll`
<br>*Droits, utilisateurs, heures de modification...*
<br>\> `man ll`
<br>`No manual entry for ll`
<br>En effet, `ll` est l'alias d'une commande.
<br>\> `alias ll`
<br>`alias ll='ls -alF'`
<br>Ainsi, si l'on veut savoir ce que fait `ll`, on ira voir le manuel de la commande `ls` au niveau des arguments `-a`, `-l` et `-F`.

5. \> `ls bin/`
<br>`[...]`

6. \> `ls ..`
<br>*Affiche les fichiers dans le dossier parent.*

7. \> `pwd`
<br>`/home/vebervi`

8. Cela va écrire *yo* dans le fichier *plop* - qui sera créé s'il n'existait pas. Le fichier sera écrasé à chaque fois que la commande sera exécutée : il n'y aura uniquement qu'un seul *yo* peu importe le nombe de fois que la commande aura été exécutée.

9. Cela va rajouter *yo* dans le fichier plop - qui sera créé s'il n'existait pas ou qui sera concaténé dans le fichier déjà existant. 
<br>Au final, on obtient trois *yo* dans notre fichier *plop* à la suite des quatre dernières commandes.

10. `file` indique le format du fichier passé en paramètre.
<br>\> `file plop`
<br>`plop: ASCII text`

11. \> `echo "Hello Toto !" > toto`
<br>\> `ln toto titi`
<br>\> `echo "Salut c'est Titi." >> toto`
<br>\> `cat titi`
<br>*On constate que titi et toto sont identiques.*
<br>\> `rm toto`
<br>*toto est bien supprimé et cela n'a aucune conséquence sur titi.*

12. \> `ln -s titi tutu`
<br>\> `echo "Salut c'est Tutu." >> titi`
<br>*On constate que tutu et titi sont identiques.*
<br>\> `echo "Salut c'est Titi." >> tutu`
<br>*On constate que tutu et titi sont encore identiques.*
<br>\> `rm titi`
<br>Cela rompt le lien entre les deux fichiers : \> `file tutu` retourne `broken symbolic link to titi`.

13. \> `cat /var/log/syslog`
<br>`[...]`
<br>*Ctrl+S* interrompt et *Ctrl+Q* reprend.

14. \> `head -5 /var/log/syslog`
<br>*5 premières lignes*
<br><br>
	\> `tail -15 /var/log/syslog`
<br>*15 dernières lignes*
<br><br>
	\> `sed -n "10, 20p" /var/log/syslog`
<br>ou encore
<br>\> `tail -10 /var/log/syslog | head -20 /var/log/syslog`
<br>*entre la 10e et la 20e ligne*

15. Cela permet d'afficher "page par page" (`| less`) les messages de log du noyau (`dmesg`).

16. \> `cat /etc/passwd`
<br>`[...]`
<br>C'est la liste des utilisateurs avec leur groupe et d'autres informations.
<br><br>
	\> `man 5 passwd`
<br>Le manuel est en fait la section 5.

17. \> `cut -d : -f 1 /etc/passwd | sort -r`
<br>`(cut) -d :` pour délimiter avec le `:`
<br>`(cut) -f 1` pour se limiter à la première occurence
<br>`| sort -r` pour trier par order alphabétique inverse

18. \> `wc -l /etc/passwd`
<br>`31 /etc/passwd`
<br>En calculant le nombre de lignes de *passwd*, on trouve le nombre d'utilisateurs ayant un compte sur cette machine.

19. \> `man -k conversion | wc -l`
<br>`4`
<br>En calculant le nombre de lignes que renvoie `man -k conversion`, on obtient le nombre de pages de manuel qui contiennent le mot *conversion*.

20. \> `sudo find -name "passwd"`
<br>`./usr/bin/passwd`
<br>`[...]`

21. \> `sudo find -name "passwd" > ~/list_passwd_files.txt`
<br>Permet de rediriger dans le fichier spécifié.

22. \> `grep -r "alias ll"`
<br>`.bashrc: alias ll='ls -alF'`

23. La commande `locate` n'est pas installée par défaut : il faut donc d'abord l'installer pour pouvoir l'utiliser.
<br>\> `sudo apt install mlocate`
<br>Enfin, on peut l'utiliser.
<br>\> `locate history.log`
<br>`/var/log/apt/history.log`

24. \> `touch testq24.txt`
<br>\> `locate testq24.txt`
<br>*rien n'est retourné*
<br><br>
	`locate` ne retrouve pas ce fichier car, contrairement à `find` qui cherche directement dans le système de fichiers, `locate` utilise une base de données pour retrouver un fichier.
<br>Or, cette base de données est mise à jour tous les jours à 7h30. On peut néanmoins la mettre à jour "à la main" grâce à la commande `sudo updatedb` - on pourra alors retrouver notre fichier qui vient juste d'être créer grâce à `locate`.

## Exercice 3 - Découverte de l’éditeur de texte nano

1. \> `cp /var/log/syslog ~/log.txt`
<br>\> `nano log.txt`

2. *ALT + R* (rechercher et remplacer, équivalent à CTRL + \\) - *kernel* - *noyau* - *A* (remplace tout)

3. *ALT + A* (pose un markeur pour sélectionner le texte à couper / coller) - *CTRL + K* (couper)
<br>*CTRL + _* puis *CTRL + V* (aller tout en bas du fichier)
<br>*CTRL + U* (coller)

4. *ALT + U* (Undid paste) - *ALT + U* (Undid line join) - *ALT + U* (Undid cut)

5. *CTRL + S* (sauvegarde le fichier) - *CTRL + X* (quitte Nano)

## Exercice 4 - Personnalisation du shell

1. \> `cp .bashrc .bashrc_bak`

3. \> `source .bashrc`
<br>Effectivement, le nom d'utilisateur et la machine passent en vert.

4. Dans ce fichier, la ligne définissant la couleur devient :
<br>`PS1='${debian_chroot:+($debian_chroot)}\[\033[35m\][\A] \[\033[00m\]]- \[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[36m\]\w\[\033[00m\]\$`
<br>où `\[\033[35m\][\A]` ajoute l'heure entre crochets en violet, ` \[\033[00m\]- ` affiche un tiret "normal" et `\[\033[36m\]\w` affiche le chemin du dossier courant en cyan
<br><br>
##### DREVET Yoann
##### VEBER Vincent
