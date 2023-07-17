```bash
basename [file] (suffix)
```
Affiche le nom de `[file]` en retirant le **path** et `(suffix)` (si précisé).

<br>

```bash
bc (file)
```
Permet d'effectuer des calculs. Si un `(file)` est précisé, alors `bc` rentrera en **mode interactif**, lira, et effectuera le calcul contenu dans celui-ci. Si aucun `(file)` n'est précisé, il lira et effectuera le calcul fourni par **stdin** sans rentrer dans le **mode interactif**. Si **stdin** ne fourni aucun **input** non plus, alors `bc` rentrera en `mode interactif`.
- `bc` peut lire une ou plusieurs opérations à la suite, séparées soit par un `;`, soit par un retour à la ligne. Une opération peut aussi bien correspondre à un calcul qu'à un assignement de valeur à une **variable**. Il renverra le résultat de chaque calcul suivi d'un retour à la ligne.
- En **mode interactif**, si `bc` n'a pas d'**input** à traiter (ou plus, s'il a fini de traiter les **inputs** fournis par `(file)`), il attendra que l'utilisateur lui en donne par le biais du **prompt**. Pour quitter le **mode interactif**, il suffit de lui envoyer `quit`.
- 4 **variables** existent par défauts dans `bc`.
	- `scale` : égal à 0 par défaut. Définit le nombre de chiffres après la virgule qui seront traités/affichée.
	- `ibase` : égal à 10 par défaut. Définit la base numérique dans laquelle il lira l'**input**.
	- `obase` : égal à 10 par défaut. Définit la base numérique dans laquelle il renverra le résultat dans l'**output**.
	- `last` : égal à 0 par défaut. Est égal à la dernière valeur affichée par `bc`.
- La syntaxe des opérations que lit `bc` correspond de manière générale à une syntaxe mathématique classique. Pour en vérifier les spécificités, aller voir la section `EXPRESSIONS` du `man bc`.

<br>

```bash
cat [file]
```
Affiche le contenu de `[file]`. 
- `-e` : Affiche les retour à la ligne (`$`).
- `-n` : Affiche les numéros de lignes.

<br>

```bash
cd [path]
```
Change le répertoire courant pour le répertoire désigné par `[path]`. On peut dire qu'on se "déplace" dans le répertoire `[path]`.

<br>

```bash
chmod [permissions] [file]
```
Change les droits de `[file]`.
- Il y a trois entités différentes qui possèdent des droits :
	- `u` pour user (l'utilisateur)
	- `g` pour group (tous les utilisateurs du groupe)
	- `o` pour other (tous les utilisateurs tout court)
- Et pour chacun il y a trois droits :
	- `r` pour read (lire le fichier)
	- `w` pour written (modifier le fichier)
	- `x` pour execute (exécuter le fichier, si c'est possible).
- Sur un `ls -l`, ça se présente comme ça :
	- `-rwxrwxrwx`
	- Les trois premiers correspondant à `u`, les trois suivant à `g`, et les trois derniers à `o`.
	- Un droit inactif affichera `-` à la place de la lettre.
- On peut rajouter un droit à un groupe avec `groupe+droit`, ou en retirer un avec `groupe-droit` :
>[!example]- 
>Pour donner le droit d'exécuter `[file]` à `o` :
>```bash
>chmod o+x [file]
>```
>Pour retirer le droit de modifier `[file]` à `g` :
>```bash
>chmod g-w [file]
>```
- La méthode la plus optimale reste de convertir `rwx` | `rwx` | `rwx` (respectivement `u` | `g` | `o`) en _421_ | _421_ | _421_ (chaque lettre correspondant à un chiffre).
	- Si un droit n'est pas actif, son chiffre respectif sera _0_.
	- On va ensuite additionner pour chacune des 3 entités les 3 chiffres correspondants aux 3 droits. Ce qui va nous donner un nombre à 3 chiffre.
	>[!example]-
	>Si l'on veut que les droits soient tel que `rwxr-xr--`, cela donnera le nombre _754_ :
	>
	>`rwx` | `r-x` | `r--`
	> -- | -- | --
	>_421_  | _401_ | _400_
	>_7_    |    _5_  |    _4_
	>
	>On peut ensuite établir ces droits sur un fichier `[file]` comme suit :
	>```bash
	>chmod 754 [file]
	>```

<br>

```bash
cp (options) [source] [destination]
```
Copie `[source]` dans `[destination]`.
> [!arg]- Options
> - `-r` : Permet de copier récursivement un dossier (sans cela l'on ne peut copier de dossier).
> - `-n` : Si `[destination]` existe déjà, ne l'écrase pas.
> - `-i` : Si `[destination]` existe déjà, demande avant de l'écraser.
> 
> Si `[destination]` existe déjà et que ni `-i` ni `-n` ne sont utilisés, écrase le fichier en question.

> [!arg]- Source
> Il faut au moins 1 `[source]`, mais l'on peut copier autant de `[source]` que l'on veut. On peut préciser un nouveau nom pour le fichier résultant de la copie si l'on ne copie qu'une seule `[source]`.
> 
> `[source]` peut s'écrire sous 2 formes :
> - Juste le nom du fichier à copier si celui ci est dans le répertoire courant.
> - Le **path** y menant si ce n'est pas le cas, avec le nom du fichier à la fin du **path**.

> [!arg]- Destination
> `[destination]` peut s'écrire sous 3 formes :
> - Juste le nom qu'on veut donner au fichier qui résultera de la copie, auquel cas la copie sera effectuée dans le répertoire courant(nécessite une unique `[source]`). 
> - Juste le **path** menant au répertoire dans lequel la copie sera effectuée, auquel cas le nom restera le même que `[source]` (forcément le cas si on copie plusieurs `[source]` à la fois). 
> - Les 2, (avec le nom au bout du **path**) auquel cas la copie sera effectué dans le répertoire spécifié, et le nom du fichier créé sera celui spécifié (nécessite une unique `[source]`).

<br>

```bash
cut [option] [list] [file]
```
Affiche des sections spécifiques de chaques lignes d'un fichier.
> [!arg]- Option
> - `-b` : La `[list]` correspondra à des **octets**. (`--bytes=[list]`)
> - `-c` : La `[list]` correspondra à des caractères. (`--characters=[list]`)
> - `-f` : La `[list]` correspondra à des champs délimités par `[delim]`. (`--fields=[list]`)
> 	- `-d[delim]` : Spécifie le séparateur qu'utilisera `-f` pour délimiter les différents champs. (`--delimiter=[delim]`)

> [!arg]- List
> On précise dans `list` le numéro des **octets**/caractères/champs qu'on veut afficher.
> - On peut donner un numéro précis.
> 	> [!example]-
> 	> Pour afficher le 2e caractère de chaque ligne :
> 	> ```bash
> 	> cut -c 2
> 	> ```
> - On peut aussi donner une plage de numéros, en séparant le premier et le dernier d'un tiret (**-**).
> 	> [!example]-
> 	> Pour afficher le 2e, 3e, et 4e champ de chaque ligne, en délimitant les champs par le séparateur ":" :
> 	> ```bash
> 	> cut -d: -f 2-4
> 	> ```
> - On peut donner plusieurs numéros et/ou plages de numéros en les séparant d'une virgule. 
> 	> [!example]-
> 	> Pour afficher le 2e, 4e, 5e, 6e, 7e, et 11e **octet** de chaque ligne :
> 	> ```bash
> 	> cut -o 2,4-7,11
> 	> ``` 

<br>

```bash
diff (option) [file1] [file2]
```

^2629f6

Affiche un rapport des différences lignes par lignes entre `[file1]` et `[file2]`. Cela sert surtout pour comparer 2 versions différentes d'un même fichier. `[file1]` étant le fichier original et `[file2]` le fichier modifié.
> [!arg]- Options
> - `-s` : Précise quand les fichiers sont identiques (au lieu de ne rien faire, par défaut).
> - `-y` : Présente les différences sous forme de 2 colonnes.

<br>

```bash
echo (option) [string]
```
Affiche une `[string]`.
> [!arg]- Option
> - **-n** : Ne rajoute pas le caractère **\n** (newline), correspondant à un saut à la ligne, à la fin de **[string]**.
> - **-e** : Interprète les backslash
> 	- **\n** : _Newline_
> 	- **\b** : _Backspace_
> 	- **\e** : _Escape_
> 	- **\t** : _Horizontal tab_
> 	- **\v** : _Vertical tab_

<br>

```bash
find (path) (test) (action)
```
Cherche un/des fichiers dans le dossier désigné par `(path)` (si aucun `(path)` n'est spécifié, le dossier par défaut sera le repertoire courant `.`) selon les `(test)` (si aucun `(test)` n'est spécifié, alors tous les fichiers seront concernés), et peut réaliser des `(action)` sur ces derniers (si aucune `(action)` n'est spécifié, une simple liste des fichiers trouvés sera renvoyée en **output**).
> [!arg]- Tests
> - `-type [type]` : Spécifie un type de fichier à rechercher parmi les suivants :
> 	- `d` : Répertoire (directory)
> 	- `f` : Fichier régulier
> 	- `l` : Liens symboliques
> - `-empty` : Le fichier est vide, que ce soit un fichier régulier ou un répertoire. 
> - `-name [name]` : Le nom correspond au pattern shell `[name]`. (`-iname` pour que ce soit insensible à la casse) 
> - `-regex [name]` : Le nom correspond au pattern **regex**<sub>[[Bash Shell - Wildcards and Regex#Extended Regular Expression (ERE, regexp)|more]]</sub> `[name]`. (`-iregex` pour que ce soit insensible à la casse) 
> - `-path [path]` : Le chemin correspond au pattern shell `[path]`. (`-ipath` pour que ce soit insensible à la casse)
> 
> On peut aussi cumuler des tests en utilisant des opérateurs :
> > [!arg]- Opérateurs
> > - `-not [test]` : Inverse le test de `[test]` (`[test]` pouvant être n'importe lequel des tests au dessus). Il ne renvoie **true** que si `[test]` renvoie **false**. 
> > On peux aussi l'écrire simplement `!`.
> > > [!example]-
> > > `-name [name]` va trouver seulement les fichiers dont le nom correspond à `[name]`
> > > 
> > > `-not -name [name]` va trouver seulement les fichiers dont le nom ne correspond PAS à `[name]`.
> > 
> > - `[test1] -a [test2]` : Revient à écrire `[test1] [test2]`. Ne renvoie **true** que si les 2 tests renvoient **true**.
> > - `[test 1] -o [test2]` : Inverse de `-a`. Renvoie **true** si au moins un des 2 tests renvoie **true**.
> > 
> > > [!goodprac]- Bonne Pratique
> > > Il est recommandé d'utiliser des parenthèses autour des tests qu'on veut combiner avec des opérateurs, surtout si l'on souhaite leur appliquer des actions spécifiques, afin de clarifier les priorités de ceux-ci.

> [!arg]- Actions
> - `-print` : Affiche la liste des fichiers trouvés.
> - `-delete` : Efface les fichiers trouvés.
> - `-exec [command] {} \;` : Exécute n'importe quelle `[command]` Shell sur les fichiers trouvés.
> 	- `{}` est un **placeholder** qui sera remplacé par tous les résultats de `find`. (`find` exécutera une fois `[command]` pour chaque résultat) (A utiliser en fonction du synopsis de `[command]`)
> 	- `;` délimite la fin de `[command]` pour `find`, mais il a besoin d'être **échappé** par un `\`.
> - `-prune` : Si le fichier est un répertoire, find ne descendra pas dedans.

<br>

```bash
export (name)
```
Exporte la variable ou fonction `(name)` dans l'environnement. On peut si on le souhaite déclarer la valeur de la variable dans `(name)` (`export (name)=(value)`). Si `(name)` nest pas précisé, renverra une liste des variables et fonctions déjà exportées dans l'environnement.

<br>

```bash
grep (option) [pattern] [file]
```
Cherche dans `[file]` le pattern `[pattern]` en **regex**<sub>[[Bash Shell - Wildcards and Regex#Extended Regular Expression (ERE, regexp)|more]]</sub>, et affiche toutes les lignes où il le trouve.
> [!arg]- Option
> - `-v` : Inverse la recherche, et ne affiche que les lignes ne contenant pas le pattern.
> - `-o` : N'affiche que la partie correspondante au pattern au lieu d'afficher toute la ligne.
> - `-E` : Utilise la version étendue des patterns **regex**.

<br>

```bash
head (option) [file]
```
Affiche les 10 premières lignes de `[file]`.
> [!arg]- Option
> - `-n` : Définir le nombre de lignes à afficher.
> - `-c` : N'affiche que le nombre spécifié de caractères en partant du début.

<br>

```bash
id (option) (login)
```
Affiche les **id** d'utilisateur et de groupes associés à `(login)`. (si `(login)` non précisé, utilisera le `login` de l'utilisateur actuel)
> [!arg]- Option
> - `-g` : Affiche uniquement l'**id** du groupe en chiffres.
> - `-G` : Affiche les **id** de tous les groupes en chiffres.
> - `-u` : Affiche l'**id** de l'utilisateur en chiffres.
> - `-n` : Utilisé avec `-guG` (au moins un), affiche un nom au lieu d'un nombre. 

<br>

```bash
less
```
Affiche le contenu d'un fichier par pages, comme un `man`.

<br>

```bash
ln (option) [target file] [link]
```
Crée un lien `[link]` qui pointe sur `[target file]`.
> [!arg]- Option
> - `-s` : Crée un lien symbolique (**symbolic link**) au lieu d'un lien physique (**hard link**).
> - `-f` : Fait de `[link]` un lien même si le fichier existe déjà.

<br>

```bash
ls (option)
```
Affiche la liste des fichiers et répertoires dans le répertoire actuel. 
> [!arg]- Option
> - `-a` : Montrer aussi les fichiers cachés.
> - `-l` : Affiche la liste des fichiers avec des informations concernant le fichier lui même (droit utilisateurs, date de modification, type de fichier, etc...) .
> - `-m` : Sépare les fichiers listés par des virgules.
> - `-t` : Trie par ordre de dernière modification.
> - `-U` : Utilisé avec `-t`, trie par ordre de création au lieu de modification.
> - `-r` : Inverse l'ordre de la liste.
> - `-R` : Liste les sous-dossier récursivement.
> - `-p` : Rajoute un / à la fin des répertoires. 

<br>

```bash
man (option) [command]
```
Affiche le manuel de `[command]`. 
> [!arg]- Option
> - `-f` : Affiche une courte description de la commande en question.

<br>

```bash
mkdir (option) [name]
```
Crée un ou des dossier nommé `[name]`.
> [!arg]- Option
> - `-p` : permet de créer des sous-dossier.
> > [!example]- 
> > Afin de créer le dossier *test1*, puis le dossier *test2* à l'intérieur de ce dernier :
> > ```bash
> > mkdir -p test1/test2
> > ```
> > Sans le `-p` cette commande ne marcherait que si le dossier *test1* existait déjà dans le répertoire courant).

<br>

```bash
mv (option) [source] [destination]
```
Déplace **[source]** vers **[destination]** et/ou renomme **[source]** en **[destination]**.
> [!arg]- Option
> - `-n` : Si `[destination]` existe déjà, ne l'écrase pas.
> - `-i` : Si `[destination]` existe déjà, demande avant de l'écraser.
> - Si `[destination]` existe déjà et que ni `-i` ni `-n` ne sont utilisés, écrase le fichier en question.

> [!arg]- Source
> Il faut au moins 1 `[source]`, mais l'on peut déplacer autant de `[source]` que l'on veut. On peut renommer le fichier déplacé si l'on ne déplace qu'une seule `[source]`.
> 
> `[source]` peut s'écrire sous 2 formes :
> - Juste le nom du fichier à déplacer/renommer si celui ci est dans le répertoire courant.
> - Le **path** y menant si ce n'est pas le cas, avec le nom du fichier à la fin du **path**.

> [!arg]- Destination
> `[destination]` peut s'écrire sous 3 formes :
> - Si l'on souhaite juste renommer `[source]`, on peut écrire juste le nouveau nom qu'on veut donner à `[source]`, auquel cas le fichier ne sera pas déplacé.
> - Juste le **path** menant au répertoire dans lequel on souhaite déplacer `[source]`, auquel cas le nom restera le même que `[source]` (forcément le cas si on déplace plusieurs `[source]` à la fois). 
> - Les 2, (avec le nom au bout du **path**) auquel cas la `[source]` sera déplacée dans le répertoire spécifié et renommée en `[destination]` (nécessite une unique `[source]`).

<br>

```bash
patch (option) [file] [patch_file]
```
Utilise un `[patch_file]` (qu'on obtient avec la commande `diff`<sub>[[Bash Shell - Command List#^2629f6|more]]</sub>) pour appliquer les changements sur `[file]`. (On peut aussi connecter le **stdout** de `diff` directement à `patch` avec `|`, `[patch_file]` n'est donc plus nécessaire)
> [!arg]- Option
> - `-b` : Crée un **backup** de `[file]` avant qu'il soit `patch`.
> - `-R` : Dans le cas ou le `[patch_file]` a été crée en inversant le fichier original et le fichier modifié. Permet d'appliquer les changements a `[file]` même si celui-ci est techniquement le fichier modifié dans le `[patch_file]`. 

<br>

```bash
pwd
```
Affiche le **path** complet du répertoire courant.

<br>

```bash
rev
```
Inverse l'ordre des caractères de chaque ligne.
    

<br>

```bash
rm (option) [file]
```
Supprime `[file]`.
> [!arg]- Option
> - `-i` : Demande confirmation pour chaque élément à supprimer.
> - `-f` : Force la suppression de tout, même s'il peut y avoir un problème.
> - `-v` : **Output** chaque élément qui est supprimé, en direct.
> - `-d` : Permet de supprimer un répertoire vide.
> - `-r` : Permet de supprimer un répertoire, même s'il n'est pas vide. 

<br>

```bash
rmdir (option) [directory]
```
Supprime le répertoire `[directory]` seulement s'il est vide.
> [!arg]- Option
> - `-p` : Supprime non seulement le dossier, mais tous ses ancêtres spécifiés dans le chemin écrit.

<br>

```bash
sed (option) [action] [file]
```
Transforme de multiples façons différentes le contenu de `[file]`. `sed` fonctionne ligne par ligne.
> [!walkthrough]- Fonctionnement Général
> 1. `sed` prend une ligne dans le **pattern space**^[**Pattern space** : dans le cadre de la commande `sed`, le **pattern space** est en quelques sorte la variable temporaire dans laquelle `sed` va stocker le texte sur lequel il travaille. Puisqu'il travaille ligne par ligne, c'est dans le **pattern space** qu'il stock la ligne à laquelle il est rendu.] 
> 2. `sed` réalise les actions demandées dessus.  
> 3. `sed` passe à la ligne suivante. (il remplace la ligne actuelle dans **pattern space** par la ligne suivante)
> 4. 
> Dès que `sed` va passer à la ligne suivante, il affichera automatiquement la ligne sur laquelle il travaillait. C'est le cas qu'il passe à la ligne suivante automatiquement parce qu'il est arrivé à la fin du cycle d'action, ou qu'il le fasse manuellement parce l'action `n` était précisé. Ce n'est pas le cas si la ligne actuelle est supprimée par l'action `d`, et que `sed` passe alors par la force des choses à la ligne suivante.(Ce comportement est annulé si l'option `-n` est précisé)
> 
> > [!example]- Example 1 
> > On a un fichier `test.txt`, qui contient le texte suivant :
> > ```
> > C'est la 1ere ligne. Test.
> > C'est la 2eme ligne. Test.
> > C'est la 3eme ligne. Test.
> > C'est la 4eme ligne. Test.
> > C'est la 5eme ligne. Test.
> > ```
> > Si j'utilise la commande :
> > ```bash
> > sed 'n;d' test.txt
> > ```
> > J'obtiendrais le résultat suivant :
> > ```
> > C'est la 1ere ligne. Test.
> > C'est la 3eme ligne. Test.
> > C'est la 5eme ligne. Test.
> > ```
> > > [!walkthrough]-
> > > 1. `sed` prend dans son **pattern space** la 1ère ligne : "*C'est la 1ere ligne. Test.*".
> > > 2. Il réalise la première action : `n`. Il va donc passer à la ligne suivante. Cela implique d'abord d'afficher automatiquement la ligne actuelle (la 1ère), puisque `-n` n'est pas précisé.
> > > 3. Il continue l'action `n`, il remplace la 1ère ligne dans le **pattern space** par la 2ème : "*C'est la 2eme ligne. Test.*".
> > > 4. Ayant finit la première action, il passe à la deuxième : `d`. Il va donc supprimer la ligne actuelle du **pattern space**. Celui-ci est donc désormais vide.
> > > 5. Ayant finit la deuxième et dernière action du cycle, il va passer à la ligne suivante et reprendre le cycle au début. Cela implique d'abord d'afficher automatiquement la ligne actuelle, puisque `-n` n'est pas précisé. Mais le **pattern space** étant vide, il n'y a pas de ligne à afficher. La 2e ligne ne sera donc jamais affiché.
> > > 6. Il prend alors la 3ème ligne dans son **pattern space** : "*C'est la 3eme ligne. Test.*".
> > > 7. Il reprend à l'étape 2 avec la ligne actuelle.
> 
> > [!example]- Example 2
> > On a un fichier `test.txt`, qui contient le texte suivant :
> > ```
> > C'est la 1ere ligne. Test.
> > C'est la 2eme ligne. Test.
> > C'est la 3eme ligne. Test.
> > C'est la 4eme ligne. Test.
> > C'est la 5eme ligne. Test.
> > ```
> > Si j'utilise la commande :
> > ```bash
> > sed '2,5{s/Test/zebi/}' test.txt
> > ```
> > J'obtiendrais le résultat suivant :
> > ```
> > C'est la 1ere ligne. Test.
> > C'est la 2eme ligne. zebi.
> > C'est la 3eme ligne. zebi.
> > C'est la 4eme ligne. zebi.
> > C'est la 5eme ligne. zebi.
> > ```
> > > [!walkthrough]-
> > > 1. `sed` prend dans son **pattern space** la 1ère ligne : "*C'est la 1ere ligne. Test.*".
> > > 2. Il n'a pas d'action à effectuer pour la première ligne, il va passer à la ligne suivante, en commençant par afficher la ligne actuelle.
> > > 3. Il remplace la 1ère ligne dans le **pattern space** par la 2ème : "*C'est la 2eme ligne. Test.*".
> > > 4. On est dans le périmètre d'action précisé, il va donc pouvoir réaliser l'action : il va chercher s'il trouve une **string** correspondant au pattern "Test" qu'on lui a donné. Celle-ci se trouve à la fin de la ligne.
> > > 5. Il remplace la string "Test" trouvée par la string "zebi".
> > > 6. N'ayant plus d'action, il va passer à la ligne suivante, en commençant par afficher la ligne actuelle.
> > > 7. Il remplace la 2ère ligne dans le **pattern space** par la 3ème : "*C'est la 3eme ligne. Test.*".
> > > 8. Il reprend à l'étape 4 avec la ligne actuelle.

> [!arg]- Option
> - `-n` : De base, `sed` affiche automatiquement la ligne actuellement présente dans le **pattern space** avant chaque changement de ligne, soit-il causé par l'arrivée à la fin du cycle d'actions, ou par la présence de l'action `n` qui provoque un changement manuel de ligne. Si `-n` est précisé, ce comportement est annulé.
> > [!example]-
> > ```bash
> > sed 'n;d'
> > ```
> > > [!walkthrough]-
> > > 1. Ici, `sed` va afficher automatiquement la 1e ligne et va passer manuellement à la 2e (`n`).
> > > 2. Puis va supprimer la 2e ligne (`d`).
> > > 3. Puis ne va pas afficher automatiquement la 2e ligne (le **pattern space** est vide, il n'y a rien à afficher), mais va quand même passer automatiquement à la ligne 3e (le cycle d'action est terminé).
> > > 4. Puis va afficher automatiquement la 3e ligne et passer manuellement à la 4e (`n`).
> > > 5. Puis va supprimer la 4e (`d`)
> > > 6. Etc...
> > 
> > ```bash
> > sed -n 'p;n'
> > ```
> > > [!walkthrough]-
> > > 1. Ici, `sed` va afficher manuellement la 1e ligne (`p`).
> > > 2. Puis ne va pas afficher automatiquement la 1e (`-n`), mais va passer manuellement à la 2e (`n`) .
> > > 3. Puis ne va pas afficher automatiquement la 2e ligne (`-n`), mais va passer automatiquement à la ligne 3e (le cycle d'action est terminé) .
> > > 4. Puis va afficher manuellement la 3e (`p`).
> > > 5. Puis ne va pas afficher automatiquement la 3e (`-n`), mais va passer manuellement à la 4e (`n`).
> > > 6. Puis ne va pas afficher automatiquement la 4e ligne (`-n`) mais va passer automatiquement à la 5e (le cycle d'action est terminé).
> > > 7. Etc...
> > 
> > - Les 2 exemple font la même chose : ils affichent une ligne sur deux d'un texte, en commençant par la 1e.
> > - Utiliser `p` sans préciser `-n` résultera en l'affichage en double des lignes sur lesquels `p` s'appliquera.
> 
> - `-i(suffix)` : Applique les modifications directement sur le fichier source, au lieu de simplement print le résultat dans **stdout**. Si un `(suffix)` est précisé, un fichier backup est créé avec le suffixe précisé ajouté au nom. (Le `(suffix)` peut être directement collé à `-i` sans syntaxe particulière).
> - `-e [action]` : Permet d'appliquer plusieurs actions différentes. Revient au même que de séparer les différentes actions avec `;`.

> [!arg]- Action
> `sed` peut réaliser des actions, soit sur toutes les lignes (l'une après l'autre), ou sur des parties spécifiques de celles-ci. En mettant juste des actions parmi celles qui suivent entre `'` et séparées par des `;`, `sed` appliquera toutes les actions l'une après l'autre à chacune des lignes l'une après l'autre.
> - `d` (delete) supprime la ligne en question (ne l'envoie donc pas dans **stdout**).
> - `n` (newline) passe à la ligne suivante sans réaliser d'action particulière, excepté l'impression automatique si `-n` n'a pas été précisé.
> - `p` (print) affiche la ligne en question.
> 
> `sed` peut aussi appliquer une action à une partie spécifique de la ligne, en utilisant un pattern **regex**<sub>[[Bash Shell - Wildcards and Regex#Extended Regular Expression (ERE, regexp)|more]</sub>.
> - Avec la syntaxe suivante, on peut réaliser des `[action]` sur les parties des lignes correspondant au pattern `[regexp]`.
> 	```bash
> 	sed '/[regexp]/[action]'
> 	```
> 	- Les `[action]` possibles sont celles citées au dessus : `d`, `n`, et `p`.
> 
> - On peut aussi remplacer le pattern **regex** trouvé avec l'action `s`, en utilisant la syntaxe suivante :
> 	```bash
> 	sed 's/[regexp]/[replacement]/(g)'
> 	```
> 	- De base, la commande `s` s'effectue uniquement sur la première occurrence de `[regexp]` de chaque ligne. Sauf si `(g)` est précisé, auquel cas il s'effectuera sur toutes les occurrences de `[regexp]`.
> 
> On peut spécifier un périmètre d'action spécifique à una action en précisant des numéros de lignes devant la l'action (à l'interieur des `'`) :
> - En mettant un chiffre, l'action ne se réalisera que sur cette ligne.
> - En mettant 2 chiffres séparés de `,`, l'action ne se réalisera que sur les lignes comprises entre les 2 chiffres (ces derniers inclus).
> - Si l'action se réalise sur un pattern **regex**, et que donc sa syntaxe est celle-ci : `'/[regexp]/[action]'`, il est necessaire d'englober l'action entre `{}`, comme cela :
> 	```bash
> 	sed '[range]{/[regexp]/[action]}'
> 	```
> 	- Ce n'est pas nécessaire pour `s`, la syntaxe commençant par le `s` et non un `/`.
> > [!example]-
> > Pour n'afficher que la 6e ligne de `[file]` :
> > ```bash
> > sed -n '6p' [file]
> > ```
> > Pour afficher une ligne sur deux  de `[file]` en commençant par la 3e et en finissant par la 7e (donc les lignes 3,5, et 7) :
> > ```bash
> > sed '3,7n;d' [file]
> > ``` 
> > 
> > Pour supprimer toutes les lignes de `[file]` qui sont comprise entre la 3e et la 6e, et qui contiennent `[pattern]`. Avec la commande `d`, il est nécessaire d'utiliser des `{}` pour donner un périmètre à `sed` :
> > ```bash
> > sed '3,6{/[pattern]/d}' [file]
> > ```

<br>

```bash
sort (option) [file]
```
Trie les ligne du contenu de `[file]` par ordre alphabétique.
> [!arg]- Option
> - `-r` : Inverse le résultat.
> - `-R` : Mélange les lignes aléatoirement au lieu de les trier.
> - `-n` : Trie les lignes qui commencent par un nombre par ordre numérique croissant. Les lignes ne commençant pas par un nombre sont triées par ordre alphabétique et placées en premières.

<br>

```bash
tail (option) [file]
```
Affiche les 10 dernières lignes d'un fichier. 
> [!arg]- Option
> - `-n` : Définir le nombre de lignes à afficher.
> - `-c` : N'affiche que le nombre spécifié de caractères en partant de la fin.

<br>

```bash
touch (option) [file]
```
Actualise la date de dernière modification et la date d'accès de `[file]`. Si `[file]` n'existe pas encore, il le créera. Peut donc servir à créer des fichiers vides. 
> [!arg]- Option
> - `-a` : Change uniquement la date d'accès.
> - `-m` : Change uniquement la date de modification.
> - `-t [AAAAMMLLLhhmm]` : Attribue la date spécifiée au lieu de la date actuelle.
> - `-c` : Ne créé pas de fichier.
> - `-h` : Affecte les liens symboliques au lieu des fichiers spécifiés.

<br>

```bash
tr (option) [set1] (set2)
```
Remplace le ou les caractères `[set1]` par le ou les caractères respectif `(set2)`. Lit la source dans **stdin** et renvoie le résultat dans **stdout**
> [!example]-
> Pour remplacer *a* par *1*, *b* par *2*, et *c* par *3* :
> ```bash
> tr 'abc' '123'
> ``` 

> [!arg]- Option
> `-d` : Supprime le ou les caractères `[set1]`.

<br>

```bash
wc (option) [file]
```
Compte le nombre de lignes, mots, et **octets** de `[file]`, et les affiche.
> [!arg]- Option
> - `-l` : Ne compte que les lignes.
> - `-w` : Ne compte que les mots.
> - `-m` : Ne compte que les charactères.
> - `-c` : Ne compte que les octets. 

<br>

```bash
xargs [command]
```
Permet d'éxécuter `[command]` qui ne lit normalement pas **stdin** comme argument, en prenant quand même **stdin** comme argument. 
Exemples de commande ne lisant pas **stdin** en arguments par défaut :
- `echo`, `rm`, `cp`, `mv`, `mkdir`, `touch`, `chmod`, `grep`, `sed`, `awk`, etc...

Si un argument est aussi tout de même précisé dans **[command]**, **xargs** va rajouter **stdin** APRÈS l'argument précisé, en les séparant d'un espace.
> [!example]-
> `file` contient la **string** "bonjour" : 
> ```bash
> cat file | xargs echo 'test'
> ```
> Le résultat renvoyé sera "test bonjour"

<br>
