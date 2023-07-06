# Les variables :

Les **variables** sont des espaces qui nous permettent de stocker des valeurs. 
	Celles-ci les stockent en bits (en binaire) et ont un espace de stockage limité (1, 2, ou encore 4 octets). 

Il y'a différents types de **variables**, et chaque type, pour être affiché dans un `printf()` correspond à un `%`,  :
- **`char`** : caractère. 
	- `%c`
- `int` : entier. 
	- `%d`
- `float` : nombres en virgule flottante. 
	- `%f`
	- `%.xf` : précise que l'on veut `x` chiffres après la virgule. 
- `string` : chaîne de caractères. 
	- `%s`

Pour déclarer une **variable** : 
- `int nom (= valeur)` 
    - On déclare une **variable** `int` (donc en l'occurrence un entier), qui s'appellera `nom`. On peut ensuite lui assigner une `valeur` immédiatement si on le souhaite, ou on peut le faire plus tard.
- `const int NOM = valeur` 
    - Si l'on souhaite déclarer une **variable** qui sera constante, c'est à dire qu'on ne pourra plus la changer dans la suite du programme. 
    - Par norme, on écrit le nom d'une **variable** constante en majuscule. 
- `int nom = (int)autreVar`
    - On peut aussi convertir des types de variables. Ici, mettons que nous ayons une **variable** `autreVar` `float`.
    - Avec cette ligne de commande, on a declare une nouvelle **variable** `nom`, qui sera la conversion en `int` (entier) du `float`.

Les _variables_ peuvent etre `signed`, ou `unsigned`. On prendra ici l'exemple d'une variable `char`.
- `unsigned char` pourra prendre une valeur uniquement positive, de 0 a 255.
- `signed char` pourra prendre une valeur positive ou negative, allant donc de -128 a 127. Le premier bit, au lieu de correspondre a 128, indiquera donc si la suite sera en negatif ou en positif.
Les **variables** stockent des valeurs. Le `char` stock une valeur, mais lorsqu'on l'affiche, il va renvoyer le caractère correspondant dans l **table  ASCII**.

<br>

# File Descriptor (ou Descripteur) :

Le **file descriptor**, ou "`fd`" est un `int` qui renvoie a un fichier. Les trois premiers correspondent aux **std** du shell.
- `0` = **stdin**
- `1` = **stdout**
- `2` = **stderr**

> [!example]-
> La fonction `write` s'écrit comme suit :
> ```C
> write(int fd, const void *buf, size_t count)
> ```
> Seulement le 1er paramètre nous intéresse, c'est justement `int fd`.
> Ils nous demandent donc à quel fichier `fd` devra renvoyer le résultat de `write`.
> Ainsi, si l'on met `1` dans ce paramètre, `write` va donc renvoyer son résultat à l'équivalent de **stdout** dans le shell, il l'affichera donc.

Le `fd` peut aussi renvoyer a des fichiers, si l'on va au dessus de `2`.

<br>

# Les opérateurs :

On va pouvoir utiliser 5 **opérateurs** de base en C :
- `+` : Addition
- `-` : Soustraction
- `*` : Multiplication
- `/` : Division
- `%` : Modulo
	- Le reste d'une division euclidienne.
	> [!example]-
	> 5 % 2 = 1

Il existe des raccourcis pour réaliser ces opérations lorsqu'on les affecte à des **variables** :
- Lorsqu'on souhaite faire n'importe quelle opération sur une **variable** :
    - `var = var + 1`
	    - `var += 1`
    - `var = var * 7`
	    - `var *= 7`
    - `var1 = var1 % var2`
	    - `var1 %= var2`
- Lorsqu'on souhaite incrémenter (+ 1) ou décrémenter (- 1) une **variable** :
- `var += 1`
    - `var++`
    - `++var`
- `var -= 1`
    - `var--`
    - `--var`
    

Il existe aussi des **opérateurs de comparaison** :
- `==` : Égal
- `!=` : Différent
- `<` : Strictement inférieur
- `<=` : Inférieur ou égal
- `>` : Strictement supérieur
- `>=` : Supérieur ou égal
- Et l'on peut combiner des comparaisons :
    - `&&` : Et
    - `||` : Ou
    - `!` : Not

On peut aussi noter l'**opérateur d'affectation** :
- `=` : Il ne représente pas une égalité, ce n'est pas le "égal" mathématique (c'est bien `==` qui rempli ce rôle). Il affecte la valeur à sa droite à ce qui se trouve à sa gauche.
	- Donc si l'on veut assigner une valeur à une **variable**, on est obligé de mettre la **variable** à gauche et la valeur à droite, l'inverse ne voudrait rien dire.

<br>

# Les conditions :

Les **conditions** permettent de réaliser des actions si une ou des conditions sont validées.

`if() {code}` va tester la condition se trouvant entre les `()`, en utilisant les **opérateurs de comparaisons**, et réaliser tout ce qui se trouve entre les `{}`, soit `{code}` si celle ci est vraie.
> [!example]-
> `if(var <= 7)` va tester si la **variable** `var` est inférieure ou égale à 7.

> [!example]-
>  `if(var < 18 && var > 11)` va tester si la **variable** **var** est comprise entre 11 et 18 non inclus.

> [!example]-
> On peut aussi faire un test **boléen**, où 1 correspond à **true**, et 0 à **false**.
> - `if(var)` teste si `var` est égal à 1 (donc **true**).
> - `if(!var)` teste si `var` est égal à 0 (donc **false**) (pas égal à 1).

- On peut rajouter en dessous un `else {}`, qui revient à un "sinon", qu'on utilisera exactement de la même façon que le `if` (sans les parenthèses puisqu'il ne teste rien), et l'on pourra donc écrire entre les `{}` ce qu'il faut réaliser si le test renvoie **false**.
	- On peut même imbriquer des `if` sur des `else` immédiatement avec `else if`.

	> [!example]-
	> ```C
	> if(var <= 5)
	> 	{
	> 		[action1]
	> 	} 
	> 	else
	> 	{
	> 		[action2]
	> 	}
	> 	
	> ```
	> Ici, si `var` est inférieur ou égale à 5, on réalisera `[action1]`, sinon, si `var` est supérieur à 5, on réalisera `[action2]`.


Le **ternaire** permet de faire plus ou moins la même chose que `if` mais sur une seule ligne.
- `(var < 43) ? printf("machin") : printf("truc")`
    - Si (`if`) var est inférieur à 43, cela va `print` "machin", sinon (`else`) cela va `print` "truc".
- `var1 = (var2 > 13) ? 1 : 0`
    - Si (`if`) var2 est supérieur à 13, on va assigner la valeur 1 à var1, sinon (`else`) on va lui assigner 0.

<br>

# Les boucles :

Les **boucles** permettent de répéter une action un certain nombre de fois.
    

`while() {code}` va répéter `{code}` tant que la condition entre les `()` est vraie.
- Fonctionne globalement comme le **if**, excepté qu'il répète tant que la condition est vraie, et qu'il n'y a pas de **else**.

`do {code} while()` permet à peu près la même chose, sauf qu'il réalise `{code}` au moins une fois, puisque qu'il effectue son test après.

`for (1, 2,  3) {code}` permet de répéter `{code}` selon des conditions particulières.
- Dans `1`, on va initialiser une **variable** (qu'on aura déclaré au préalable).
    - `i` = 0
- Dans `2`, on va établir une condition.
    - `i` <= 5
- Dans `3`, on va incrémenter ou décrémenter notre **variable**.
    - `i`++
- Ici, `for` réalisera donc `{code}` 5 fois.

<br>

# Les fonctions :

- Les _fonctions_ sont des sortes de "bout de code", que l'on peut appeler dans un programme où même dans une autre _fonction_, pour effectuer des actions. On peut aussi leur donner des _paramètres_.
    
- Une fonction se déclare en trois partie :
    

- **void    ft_putchar(char a)** 
    
- Ici **void** déclare le type de la _fonction_. C'est le type de la _variable_ qu'elle devra retourner.
    

- Une _fonction_ peut retourner une _variable_, c'est à dire que quand on l'appellera, elle renverra à la place de là où on l'a appelée une _variable_.
    
- Ici cette fonction ne retournera rien : elle exécutera son code avant de retourner **void**, soit rien.
    
- Si l'on doit retourner une variable, on écrira en dernière ligne de notre fonction "**return (var);**", avec var étant soit le nom de la variable, soit une valeur directement.
    

- **ft_putchar** est le nom de notre _fonction_. Lorsqu'on l'appellera, c'est ce nom qu'on utilisera.
    
- **(char a)** est le _paramètre_ que notre _fonction_ prend. On aurait pu lui donner plusieurs _paramètres_, toujours à l'intérieur des parenthèses, séparés par '**,** ' :
    

- Un _paramètre_ est une _variable_ que l'on peut envoyer à la _fonction_ pour soit agir dessus, soit s'en servir pour agir.
    
- Lorsqu'on envoie une _variable_ en _paramètre_ à une _fonction_, elle va créer une copie de cette _variable_, dans laquelle elle va stocker la même valeur.
    

- On ne peut donc pas agir directement sur une _variable_ avec une _fonction_, pour cela il faut utiliser des _pointeurs_.
    

- Lorsqu'on déclare une _fonction_, il faut déclarer le type de _variable_ qu'on devra mettre en _paramètre_.

<br>

# Les pointeurs :

- Pour comprendre les _pointeurs_, il faut comprendre le stockage des _variables_ :
    

- Les _variables_ stockent leurs valeurs dans des cases de la mémoire, correspondant à un numéro.
    
- Si on initialise un **int i** à 465, 465 sera stocké sur une case de la mémoire correspondant à un numéro spécifique, qui permet de la retrouver.
    
- On appelle ce numéro spécifique _l'adresse_ de **i**.
    

- Un _pointeur_ est une variable qui stockera comme valeur l'_adresse_ d'une autre variable. C'est donc une _variable_ qui va "pointer" sur une autre _variable_.
    

- Un _pointeur_ se déclare et s'utilise selon  une syntaxe particulière.
    
- Si l'on veut déclarer un _pointeur_, il faudra le déclarer comme suit :
    

- **int *p_i;**
    
- C'est un type **int**, puisqu'il stocke une _adresse_, donc un nombre. Mais ce n'est pas un simple type **int**, avec l'"*****", on indique que c'est un _pointeur_ vers une _variable_.
    
- Pour lui assigner l'_adresse_ d'une _variable_, on utilise **&**. **&i** correspond à l'_adresse_ à laquelle est stockée la valeur de **i**. Donc ici, on pourra lui assigner cela comme suit : **p_i = &i;**.
    
- Ensuite, si l'on manipule **p_i**, on manipule l'_adresse_ qu'il stock. pour manipuler la _variable_ pointée par **p_i**, on utilisera ***p_i**.
    

- Un _pointeur_ servira notamment à modifier des variables qu'on enverra dans des _fonctions_. En effet, puisque celle-ci utilisent une copie de la _variable_ qu'on lui donne et la supprime à la fin, si on lui envoie un _pointeur_, et qu'il manipule la _variable_ pointée par le _pointeur_ donné en paramètre, cela nous permettra de modifier cette _variable_. Puisque même si l'on fait une copie du _pointeur_, celle ci pointera vers la même _adresse_, ainsi modifiera la vraie _variable_ tout de même.