
# Liens symboliques / Liens physiques (Symbolic link / Hard link)

Sous Unix, le nom d'un fichier et son contenu sont stockés différemment. Le contenu se voit attribuer un numéro **Inode**, le nom du fichier sera associé à cet **Inode**.

- On a un _File1_ associé à un numéro **Inode** x, et l'on veut créer un lien _File2_.
	- Si c'est un lien physique, _File2_ sera lui aussi associé au numéro **Inode** x. _File1_ et _File2_ sont donc 2 fichiers égaux qui partagent le même contenu. Si l'on en ouvre un pour le modifier, l'autre sera tout autant modifié. Si l'on supprime _File1_, _File2_ sera toujours présent et renverra toujours au même **Inode**, et donc contenu. Il faut supprimer tous les noms de fichiers renvoyant à un même **Inode** pour que celui-ci et son contenu soit supprimé.
		- Dans un `ls -l`, le nombre qui suit les droits utilisateurs est le nombre de noms de fichiers se partageant le même **Inode**.
	- Si c'est un lien symbolique, _File2_ renverra non pas à un **Inode**, mais au nom de fichier _File1_ lui-même. En ouvrant _File2_, on ouvre en fait _File1_, qui va nous renvoyer à son **Inode**. Si l'on supprime _File1_, _File2_ devient un "lien mort", ne renvoyant plus à rien.


# stdin, stdout, stderr :

**Stdin**  est l'entrée standard d'une commande (en général, ce que l'on aura tapé nous même). **Stdout** est sa sortie standard de cette commande, et **stderr** la sortie standard des erreurs.

- On peut brancher le **stdout** d'une commande avec le **stdin** d'une autre, en utilisant :  ` | `.
- On peut rediriger un _stdout_ vers un fichier, en utilisant **>** pour remplacer le contenu, et **>>** pour rajouter le contenu.
- On peut rediriger le _stderr_ vers un fichier de la même manière, mais en utilisant un 2 avant les **>** et **>>**.