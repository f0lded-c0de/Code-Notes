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
cp [source] [destination]
```
Copie `[source]` dans `[destination]`.
- Il faut au moins 1 `[source]`, mais l'on peut copier autant de `[source]` que l'on veut. On peut préciser un nouveau nom pour le fichier résultant de la copie si l'on ne copie qu'une seule `[source]`.
- `[source]` peut s'écrire sous 2 formes :
	- Juste le nom du fichier à copier si celui ci est dans le répertoire courant
	- Le **path** y menant si ce n'est pas le cas, avec le nom du fichier à la fin du **path**.
- `[destination]` peut s'écrire sous 3 formes :
	- Juste le nom qu'on veut donner au fichier qui résultera de la copie, auquel cas la copie sera effectuée dans le répertoire courant(nécessite une unique `[source]`). 
	- Juste le **path** menant au répertoire dans lequel la copie sera effectuée, auquel cas le nom restera le même que `[source]` (forcément le cas si on copie plusieurs `[source]` à la fois). 
	- Les 2, (avec le nom au bout du **path**) auquel cas la copie sera effectué dans le répertoire spécifié, et le nom du fichier créé sera celui spécifié (nécessite une unique `[source]`).
- `-r` : Permet de copier récursivement un dossier (sans cela l'on ne peut copier de dossier).
- `-n` : Si `[destination]` existe déjà, ne l'écrase pas.
- `-i` : Si `[destination]` existe déjà, demande avant de l'écraser.
- Si `[destination]` existe déjà et que ni `-i` ni `-n` ne sont utilisés, écrase le fichier en question.

<br>

```bash
cut [option] [list] [file]
```
Affiche des sections spécifiques de chaques lignes d'un fichier.
    

- **[option]** :
    

- **-b[list]** : La **[list]** correspondra à des _octets_. (**--bytes=[list]**)
    
- **-c[list]** : La **[list]** correspondra à des caractères. (**--characters=[list]**)
    
- **-f[list]** : La **[list]** correspondra à des champs délimités par **[delim]**. (**--fields=[list]**)
    

- **-d[delim]** : Spécifie le séparateur qu'utilisera **-f** pour délimiter les différents champs. (**--delimiter=[delim]**)
    

- **[list]** : Précise le numéro des octes/caractères/champs qu'on veut afficher.
    

- On peut donner un numéro précis. (**cut -c 2** va afficher le 2e caractère de chaque ligne)
    
- On peut aussi donner une plage de numéros, en séparant le premier et le dernier d'un tiret (**-**). (**cut -c 2-4** va afficher le 2e, 3e, et 4e caractère de chaque ligne.)
    
- On peut donner plusieurs numéros et/ou plages de numéros en les séparant d'une virgule. (**cut -c 2,4-7,11** va afficher le 2e, 4e, 5e, 6e, 7e, et 11e caractère de chaque ligne)
    

<br>

```bash
diff [file1] [file2]
```
Affiche un rapport des différences lignes par lignes entre **[file1]** et **[file2]**. Cela sert surtout pour comparer 2 versions différentes d'un même fichier. **[file1]** étant le fichier original et **[file2]** le fichier modifié.
    

- **-s** : Précise quand les fichiers sont identiques (au lieu de ne rien faire, par défaut).
    
- **-y** : Présente les différences sous forme de 2 colonnes.
    

<br>

```bash
echo [string]
```
Affiche une [**string]**.
    

- **-n** : Ne rajoute pas le caractère **\n** (newline), correspondant à un saut à la ligne, à la fin de **[string]**.
    
- **-e** : Interprète les backslash
    

- **\n** : _Newline_
    
- **\b** : _Backspace_
    
- **\e** : _Escape_
    
- **\t** : _Horizontal tab_
    
- **\v** : _Vertical tab_
    

<br>

```bash
find
```
Cherche un/des fichiers dans le dossier spécifié, et peut réaliser des actions sur ces derniers.
    

- Tests :
    

- **-type** : Spécifie un type de fichier à rechercher :
    

- **d** : Répertoire (directory)
    
- **f** : Fichier régulier
    
- **l** : Liens symboliques
    

- **-empty** : Le fichier est vide, que ce soit un fichier régulier ou un répertoire.
    
- **-name [name]** : Le nom correspond au pattern shell **[name]**. (**-iname** pour que ce soit insensible à la casse)
    
- **-regex [name]** : Le nom correspond au pattern _regex_ **[name]**. (**-iregex** pour que ce soit insensible à la casse)
    
- **-path [path]** : Le chemin correspond au pattern shell **[path]**. (**-ipath** pour que ce soit insensible à la casse)
    

- Opérateurs :
    

- **-not** **[test]** : Inverse le test de **[test]** (**[test]** pouvant être n'importe lequel des tests au dessus) (renvoie _true_ seulement si **[test]** renvoie _false_). Exemple :
    

- "**-name [name]**" va trouver seulement les fichiers dont le nom correspond à **[name]**
    
- "**-not -name [name]**" va trouver seulement les fichiers dont le nom ne correspond PAS à **[name]**.
    

- **[test1] -a [test2]** : Revient à écrire **[test1] [test2]**. Ne renvoie _true_ que si les 2 tests renvoient _true_.
    
- **[test 1] -o [test2]** : Inverse de **-a**. Renvoie _true_ si au moins un des 2 tests renvoie _true_.
    

- Actions :
    

- **-print** : Affiche la liste des fichiers trouvés.
    
- **-delete** : Efface les fichiers trouvés.
    
- **-exec [command] {} \;** : Exécute n'importe quelle **[command]** Shell sur les fichiers trouvés.
    

- **{}** est un _placeholder_ qui sera remplacé par tous les résultats de **find**. (**find** exécutera une fois **[command]** pour chaque résultat) (A utiliser en fonction du synopsis de **[command]**)
    
- **;** délimite la fin de **command]** pour **find**, mais il a besoin d'être _échapé_ par un **\**.
    

- **-prune** : Si le fichier est un répertoire, find ne descendra pas dedans.
    

<br>

```bash
export (name)
```
Exporte la variable ou fonction **(name)** dans l'environnement. On peut si on le souhaite déclarer la valeur de la variable dans **(name)**. Si **(name)** nest pas précisé, renverra une liste des variables et fonctions déjà exportées dans l'environnement.
    

<br>

```bash
grep [pattern] [file]
```
Cherche dans **[file]** le pattern **[pattern]** en _regex_, et affiche toutes les lignes où il le trouve.
    

- **-v** : Inverse la recherche, et ne affiche que les lignes ne contenant pas le pattern.
    
- **-o** : N'affiche que la partie correspondante au pattern au lieu d'afficher toute la ligne.
    
- **-E** : Utilise la version étendue des patterns _regex_.
    

<br>

```bash
head
```
Affiche les 10 premières lignes d'un fichier. 
    

- **-n** : Définir le nombre de lignes à afficher.
    
- **-c** : N'affiche que le nombre spécifié de caractères en partant du début.
    

<br>

```bash
id (login)
```
Affiche les _id_ d'utilisateur et de groupes _effectifs_ et _réels_ associés à **(login)**. (si **(login)** non précisé, utilisera le _login_ de l'utilisateur actuel)
    

- **-g** : Affiche uniquement l'_id_ du groupe _effectif_ en chiffres.
    
- **-G** : Affiche les _id_ de tous les groupes en chiffres.
    
- **-u** : Affiche l'_id_ de l'utilisateur _effectif_ en chiffres.
    
- **-n** : Utilisé avec **-guG** (au moins un), affiche un nom au lieu d'un nombre.
    

<br>

```bash
less
```
Affiche le contenu d'un fichier par pages, comme un **man**. 
    

<br>

```bash
ln [target file] [link]
```
Crée un lien **[link]** qui pointe sur **[target file]**.
    

- **-s** : Crée un lien symbolique (_symbolic link_) au lieu d'un lien physique (_hard link_).
    
- **-f** : Fait de **[link]** un lien même si le fichier existe déjà.
    

<br>

```bash
ls
```
Affiche la liste des fichiers et répertoires dans le répertoire actuel. 
    

- **-a** : Montrer aussi les fichiers cachés.
    
- **-l** : Affiche la liste des fichiers avec des informations concernant le fichier lui même (droit utilisateurs, date de modification, type de fichier, etc...) .
    
- **-m** : Sépare les fichiers listés par des virgules.
    
- **-t** : Trie par ordre de dernière modification.
    
- **-U** : Utilisé avec **-t**, trie par ordre de création au lieu de modification.
    
- **-r** : Inverse l'ordre de la liste.
    
- **-R** : Liste les sous-dossier récursivement.
    
- **-p** : Rajoute un / à la fin des répertoires.
    

<br>

```bash
man [command]
```
Affiche le manuel de **[command]**. 
    

- **-f** : Affiche une courte description de la commande en question.
    

<br>

```bash
mkdir [name]
```
Crée un ou des dossier nommé **[name]**.
    

- **-p** : permet de créer des sous-dossier (> **mkdir -p test1/test2** va créer le dossier test1, puis le dossier test2 à l'intérieur de ce dernier. Sans le **-p** cette commande ne marcherait que si le dossier test1 existait déjà dans le répertoire courant).
    

<br>

```bash
mv [source] [destination]
```
Déplace **[source]** vers **[destination]** et/ou renomme **[source]** en **[destination]**.
    

- **[source]** peut être simplement le nom du fichier à déplacer/renommer si celui ci est dans le répertoire courant, ou aussi inclure  le _path_ y menant si ce n'est pas le cas.
    

- Il faut au moins 1 **[source]**, mais l'on peut déplacer autant de **[source]** que l'on veut. On ne peut par contre renommer qu'une seule **[source]**.
    

- **[destination]** peut être simplement le nom qu'on veut donner à **[source]** si l'on souhaite uniquement le renommer, auquel cas celui-ci ne sera pas déplacé (nécessite une unique **[source]**). Ça peut aussi être simplement le _path_ menant au répertoire dans lequel on veut déplacer **[source]**, auquel cas le nom restera le même que **[source]** (forcémment le cas si on déplace plusieurs **[source]** à la fois). Ça peut aussi être les 2, auquel cas la **[source]** sera déplacée dans le répertoire spécifié et renommée en **[destination]** (nécessite une unique **[source]**).
    
- **-n** : Si **[destination]** existe déjà, ne l'écrase pas.
    
- **-i** : Si **[destination]** existe déjà, demande avant de l'écraser.
    
- Si **[destination]** existe déjà et que ni **-i** ni **-n** ne sont utilisés, écrase le fichier en question.
    

<br>

```bash
patch [file] [patch_file]
```
Utilise un **[patch_file]** (qu'on obtient avec la commande **diff**) pour appliquer les changements sur **[file]**. (On peut aussi connecter le _stdout_ de **diff** directement à **patch** avec **|**, **[patch_file]** n'est donc plus nécessaire)
    

- **-b** : Crée un _backup_ de **[file]** avant qu'il soit **patch**.
    
- **-R** : Dans le cas ou le **[patch_file]** a été crée en inversant le fichier original et le fichier modifié. Permet d'appliquer les changements a **[file]** même si celui-ci est techniquement le fichier modifié dans le **[patch_file]**.
    

<br>

```bash
pwd
```


<br>

```bash
rev
```
Inverse l'ordre des caractères de chaque ligne.
    

<br>

```bash
rm [file]
```
Supprime **[file]**.
    

- **-i** : Demande confirmation pour chaque élément à supprimer.
    
- **-f** : Force la suppression de tout, même s'il peut y avoir un problème.
    
- **-v** : _Output_ chaque élément qui est supprimé, en direct.
    
- **-d** : Permet de supprimer un répertoire vide.
    
- **-r** : Permet de supprimer un répertoire, même s'il n'est pas vide.
    

<br>

```bash
rmdir [directory]
```
Supprime le répertoire **[directory]** seulement s'il est vide.
    

- **-p** : supprime non seulement le dossier, mais tous ses ancêtres spécifiés dans le chemin écrit.
    

<br>

```bash
sed [command] [file]
```
Transforme de multiples façons différentes du texte. **sed** fonctionne ligne par ligne.
    

- Fonctionnement général de **sed** :
    

- **sed** va lire la première ligne, réaliser des actions dessus, et l'afficher si **-n** n'est pas précisé, avant de passer à la prochaine ligne et répéter.
    

- **sed** va lire la première ligne dans le _pattern space_, qui est en quelque sorte la variable temporaire dans laquelle **sed** va stocker le texte sur lequel il travaille sur le moment (ligne par ligne donc).
    
- Il va ensuite réaliser des actions dessus. Si **d** est effectué, la ligne actuellement lue dans le _pattern space_ sera supprimée avant l'affichage automatique, la ligne ne sera donc pas affichée automatiquement. Si **n** est effectué, il va remplacer le texte actuellement dans le pattern space par la ligne suivante. Mais ne la supprimant pas, si l'affichage automatique est censé avoir lieu après la commande **n**, **n** va afficher lui même manuellement le _pattern space_ avant de le remplacer (le remplacement empêchant l'affichage automatique de la première ligne, celle-ci n'étant plus dans le _pattern space_ après l'action de **n**).
    
- La commande **sed -n 'p;p;p;n'** va procéder comme suit :
    

1. Lecture de la premiere ligne dans le _pattern space_.
    
2. Réalisation des actions : ici on affiche 3 fois la première ligne (**p;p;p**), puis on passe à la ligne suivante, soit la deuxième ligne dans le _pattern space_ (**n**).
    
3. Fin du cycle d'action, pas d'affichage automatique **-n** étant précisé, on passe donc à la ligne suivante, lecture de la troisièmee ligne dans le _pattern space_.
    
4. Répétition depuis la 2e étape.
    

- La commande afficher une ligne sur deux 3 fois de suite, en commençant par la première.
    
- Si **-n** n'avait pas été précisé, **n** aurait affiché le _pattern space_ avant de le remplacer (à l'étape 2), et à l'étape 3 le _pattern space_ aurait été automatiquement affiché avant de passer à la ligne suivante.
    

- Sans lui donner de pattern, **sed** peut effectuer des actions sur chaques lignes l'une après l'autre, avec des lettres correspondant à une action spécifique.
    

- **d** (delete) supprime la ligne en question (ne l'envoie donc pas dans _stdout_).
    
- **n** (newline) passe à la ligne suivante sans réaliser d'action particulière, excepté l'impression automatique qui arrive en fin de cycle si **-n** n'a pas été précisé.
    
- **p** (print) affiche la ligne en question.
    

- **sed** peut aussi appliquer une action à une partie spécifique de la ligne, en utilisant un pattern _regex_.
    

- **s/[regexp]/[replacement]/(g)** : Remplace ce qui correspond en _regex_ à **[regexp]** par **[replacement]**.
    

- De base, la commande **s** s'effectue sur la première occurrence de **[regexp]** de chaque ligne, et ne s'effectuera pas sur les occurrence suivante d'une même ligne. Sauf si **(g)** est précisé, auqel cas il s'effectuera sur toutes les occurrences de **[regexp]**.
    

- **/[regexp]/[action]** : Applique **[action]** à ce qui correspond en _regex_ à **[regexp]**. **[action]** pouvant être n'importe laquelle des actions spécifiée au dessus.
    

- **sed** a plusieurs options :
    

- **-n** : **sed** affiche automatiquement dans _stdout_ chaque ligne en plus de réaliser l'action demandée, sauf si l'option **-n** est précisée.
    

- e.g. **sed** **'n;d'** va afficher la 1e ligne automatiquement et passer à la suivante (**n**), puis supprimer la 2e ligne (**d**), puis laisser **sed** afficher la 3e en passant à la suivante (**n)**, puis supprimer la 4e (**d**)...
    
- e.g. **sed -n 'p;n'** ne va rien afficher de base (**-n**). Il va ensuite afficher la 1e ligne (**p**), puis passer la 2e (**n**), puis afficher la 3e (**p**), puis passer la quatrième (**n**).
    
- Les 2 exemple font la même chose : ils affichent une ligne sur deux d'un texte, en commençant par la 1e.
    
- Utiliser **p** sans préciser **-n** résultera en l'affichage en double des lignes sur lesquels **p** s'appliquera.
    

- **-i(suffix)** : Applique les modifications directement sur le fichier source, au lieu de simplement print le résultat dans _stdout_. Si un **(suffix)** est précisé, un fichier backup est créé avec le suffixe précisé ajouté au nom. (Le **(suffix)** peut être directement collé à **-i** sans syntaxe particulière).
    
- **-e [command]** : Permet d'appliquer plusieurs commandes differentes. Revient au même que de séparer les différentes commandes avec **;**.
    
- On peut spécifier un périmètre d'action spécifique à **sed** en précisant des numéros de lignes devant la commande **sed** :
    

- **sed '3,7n;d' [file]** va afficher une ligne sur deux en commençant par la 3e et en finissant par la 7e (donc les lignes 3,5, et 7).
    
- **sed '6p' [file]** ne va print que la 6e ligne.
    
- **sed '3,6{/[pattern]/d}' [file]** va supprimer toutes les lignes comprise entre la 3e et la 6e, et qui contiennent **[pattern]**. Avec la commande **d**, il est nécessaire d'utiliser des **{}** pour donner un périmètre à **sed**.
    

<br>

```bash
sort
```
Trie les ligne d'un fichier texte par ordre alphabétique.
    

- **-r** : Inverse le résultat.
    
- **-R** : Mélange les lignes aléatoirement au lieu de les trier.
    
- **-n** : Trie les lignes qui commencent par un nombre par ordre numérique croissant. Les lignes ne commençant pas par un nombre sont triées par ordre alphabétique et placées en premières.
    

<br>

```bash
tail
```
Affiche les 10 dernières lignes d'un fichier. 
    

- **-n** : Définir le nombre de lignes à afficher.
    
- **-c** : N'affiche que le nombre spécifié de caractères en partant de la fin.
    

<br>

```bash
touch [file]
```
Actualise la date de dernière modification et la date d'accès de **[file]**. Si **[file]** n'existe pas encore, il le créera. Peut donc servir à créer des fichiers vides. 
    

- **-a** : Change uniquement la date d'accès.
    
- **-m** : Change uniquement la date de modification.
    
- **-t [AAAAMMLLLhhmm]** : Utilise la date spécifiée au lieu de la date actuelle.
    
- **-c** : Ne créé pas de fichier.
    
- **-h** : Affecte les liens symboliques au lieu des fichiers spécifiés.
    

<br>

```bash
tr [set1] (set2)
```
Remplace le ou les caractères **[set1]** par le ou les caractères respectif **(set2)**.
    

- Exemple :
    

- **tr 'abcde' '12345'** remplacera **a** par **1**, **b** par **2**, et **c** par **3**.
    

- **-d** : Supprime le ou les caractères **[set1]**.
    

<br>

```bash
wc [file]
```
Compte le nombre de lignes, mots, et octets de **[file]**, et les affiche.
    

- **-l** : Ne compte que les lignes.
    
- **-w** : Ne compte que les mots.
    
- **-m** : Ne compte que les charactères.
    
- **-c** : Ne compte que les octets.
    

<br>

```bash
xargs [command]
```
Permet d'éxécuter **[command]** qui ne lit normalement pas _stdin_ comme argument, en prenant quand même _stdin_ comme argument. Exemples de commande ne lisant pas _stdin_ en arguments par défaut :
    

- **echo**, **rm**, **cp**, **mv**, **mkdir**, **touch**, **chmod**, **grep**, **sed**, **awk**, etc...
    
- Si un argument est aussi tout de même précisé dans **[command]**, **xargs** va rajouter _stdin_ APRÈS l'argument précisé, en les séparant d'un espace. Exemple :
    

- Si **file** contient la _string_ "bonjour", alors **cat file | xargs echo 'test'** renverra "test bonjour"

<br>
