
# Liens symboliques / Liens physiques (Symbolic link / Hard link)

Sous Unix, le nom d'un fichier et son contenu sont stockés différemment. Le contenu se voit attribuer un numéro **Inode**, le nom du fichier sera associé à cet **Inode**.

- On a un _File1_ associé à un numéro **Inode** x, et l'on veut créer un lien _File2_.
	- Si c'est un lien physique, _File2_ sera lui aussi associé au numéro **Inode** x. _File1_ et _File2_ sont donc 2 fichiers égaux qui partagent le même contenu. Si l'on en ouvre un pour le modifier, l'autre sera tout autant modifié. Si l'on supprime _File1_, _File2_ sera toujours présent et renverra toujours au même **Inode**, et donc contenu. Il faut supprimer tous les noms de fichiers renvoyant à un même **Inode** pour que celui-ci et son contenu soit supprimé.
		- Dans un `ls -l`, le nombre qui suit les droits utilisateurs est le nombre de noms de fichiers se partageant le même **Inode**.
	- Si c'est un lien symbolique, _File2_ renverra non pas à un **Inode**, mais au nom de fichier _File1_ lui-même. En ouvrant _File2_, on ouvre en fait _File1_, qui va nous renvoyer à son **Inode**. Si l'on supprime _File1_, _File2_ devient un "lien mort", ne renvoyant plus à rien.

<br>

# stdin, stdout, stderr :

**Stdin**  est l'entrée standard d'une commande (en général, ce que l'on aura tapé nous même). **Stdout** est sa sortie standard de cette commande, et **stderr** la sortie standard des erreurs.

<br>

On peut brancher le **stdout** d'une commande avec le **stdin** d'une autre, en utilisant `|` :
```bash
cat file | wc -l
```
> [!walkthrough]-
> Ici `cat` va renvoyer dans **stdout** le contenu de `file`, `|` va le prendre et le redonner au **stdin** de `wc`, qui va compter en compter les lignes, en renvoyer le résultat à nouveau dans **stdout**.

<br>

On peut rediriger le **stdout** ou le **stderr** vers un fichier :

- Pour rediriger le **stdout** vers un fichier, en utilisant `>` pour remplacer le contenu, et `>>` pour rajouter le contenu :
	```bash
	cat file >> output.txt
	```

- Pour rediriger le **stderr** vers un fichier de la même manière, mais avec `2>` et `2>>` :
	```bash
	cat file 2>> error.txt
	```

- Pour rediriger les 2 en même temps :
	```bash
	cat file >> output.txt 2>> error.txt
	```

<br>

Sans redirection vers une commande ou un fichier, le **stdout** et le **stderr** seront affichés dans l'**interface de commande en ligne**.

<br>

# Variables et Environnement :

Une **variable** est une valeur ou des données associées à un nom, qu'on peut réutiliser plus tard grace à ce nom.

<br>

On peut déclarer n'importe quelle **variable** dans le shell, en tapant simplement : `variable=valeur`. 
- Si je tape juste :
	```bash
	zebi=truc
	```
- J'ai créé la **variable** *zebi* et lui ai attribué la valeur *truc*.

<br>

Je peux ensuite l'utiliser dans des commandes, mais il est nécessaire de préciser qu'on désigne une **variable** en mettant `$` devant le nom de celle-ci. 
- Si je tape :
	```bash
	echo zebi
	```
- `echo` me renverra simplement "zebi", pensant que je lui parle de la **string** "zebi". Pour que echo me renvoie la **string** "truc", je dois taper :
	```bash
	echo $zebi
	```
- Ici, echo comprendra avec le `$` que l'on parle d'une **variable** *zebi*, et renverra donc son contenu : "truc".

<br>

Cependant, la **variable** est pour le moment locale, ce qui la rend inutilisable par des scripts/programmes ainsi que dans des sous-shell. Pour changer cela, il faut l'exporter dans l'**environnement**^[**Environnement** : c'est une sorte d'ensemble de **variables** et de **fonctions** qui sont "globale" par rapport au **shell** en question. Toute **variable** exportée dans l'**environnement** sera accessible par n'importe quel processus exécuté au sein de ce **shell** ou de n'importe quel **sous-shell** découlant de ce **shell**.].
- On peut exporter n'importe quelle **variable** (ou **fonction**) dans l'**environnement** en tapant :
	```bash
	export zebi
	```
- J'ajoute la **variable** *zebi* à l'**environnement**. *zebi* est désormais une **variable globale** (contrairement à une **variable locale** avant d'être exportée). Elle est ainsi accessible depuis n'importe quel **sous-shell** ou par n'importe quel processus.

<br>

On peut accéder à la liste de toutes les **variables** présentes dans l'**environnement** avec la commande `env`, ou seulement à la liste des **variables** qui ont été exportées dans l'**environnement** (et non pas des **variables** d'**environnement** système par exemple) avec la commande `export` sans arguments.


