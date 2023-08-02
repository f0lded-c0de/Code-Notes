# Les fonctions :

Les **fonctions** sont des sortes de "bloc de code", qui vont avoir pour but de réaliser une (ou des) actions spécifiques. C'est le cœur de la programmation en C : tout le code sera dans différentes **fonctions**. On peut ensuite appeler les **fonctions** qu'on a déjà déclaré et défini dans d'autres **fonctions**. En gardant des **fonctions** courtes avec des objectifs spécifiques, cela permet de segmenter le code en différents blocs logiques.

## Fonction 'main' :

Avant de parler des **fonctions** en général, il faut parler de la **fonction** `main`. C'est la **fonction** principale, ce qu'on appelle le "**point d'entrée**" du **programme**. Lorsqu'on exécutera un **programme** en C, il commencera toujours par la **fonction** `main`, et s'arrêtera une fois qu'il aura atteint le `return 0;` de celle-ci. Elle s'écrit comme suit :
```C
int main(void) 
	{
	//[actual code]
	return 0;
	}
```
- `int` indique que la **fonction** va retourner un **entier**. En effet, en C, on attend que le **programme** retourne `0` si tout s'est bien passé.
- `main()` est le nom de la **fonction**.
- `void` indique que la **fonction** n'attend pas d'argument. Elle est juste censée être appelée pour lancer le **programme**.
- `//[actual code]` sera le code du **programme** lui-même.
- `return 0;` marque la fin du code. Le **programme** se ferme, en retournant la valeur `0` pour indiquer qu'il a bien atteint la fin du code sans soucis.

## Déclaration de fonctions :

On peut maintenant voir la déclaration des autres **fonctions** :
```C
type ft_name(par1_type par1, par2_type par2, etc...) {}
```
- `type` correspond au type de valeur que la **fonction** va retourner. Cela veut dire que lorsqu'on appellera cette **fonction**, si elle retourne une valeur, celle-ci remplacera la **fonction** à l'endroit du code ou elle est appelée.
	- Cela peut être un `int` (comme la fonction `main` par exemple), un `char`, etc... 
	- La **fonction** peut aussi ne rien avoir à retourner, auquel cas on utilisera le type `void`.
- `ft_name` correspond au nom de la **fonction**. C'est celui-ci qu'on utilisera pour l'appeler plus tard.
- `()` : On trouve entre les parenthèses les **paramètres** que prendra la **fonction** lorsqu'elle sera appelée. Les **paramètres** sont des **variables** qui sont déclarées entre ces `()` et auxquelles ont affecte une valeur lorsqu'on appelle la **fonction**, en remplaçant leur nom dans `()` par la valeur que l'on souhaite qu'elle prennent.
	- `par1_type` est le type de **variable** que sera ce **paramètre**.
	- `par1` est le nom de la **variable** qu'on utilisera dans la **fonction**.
	- On peut déclarer plusieurs **paramètres** en les séparant de `, `.
	- Si la **fonction** ne prend pas de paramètres, on écrira `(void)` (comme la fonction `main`).
	- `{}` délimite le **scope** de la **fonction**.
		- Tout le code de la **fonction** se trouvera entre ces accolades.
		- Toute **variable** déclarée dans la **fonction** (y compris les **paramètres**) seront limitées à ce **scope**. C'est à dire qu'elle n'existeront qu'à l'intérieur de celui-ci. Concrètement, la **variable** sera créée au moment ou la **fonction** sera appelée, et elle sera détruite au moment ou la **fonction** se terminera.

## Inclusion et appel de fonctions :

Pour appeler une **fonction** qu'on a déclaré, à moins qu'elle ne soit déclaré dans le même fichier plus haut, il faudra faire savoir au programme que cette **fonction** existe. Pour cela on utilisera un **prototype**, qu'on placera tout en haut du fichier.

Le **prototype** est quasiment identique à la déclaration de la **fonction**, à l'exception qu'au lieu d'ouvrir le **scope** de la fonction à la fin de la ligne, on va juste mettre un `;`, et les **paramètres** ne nécessiteront que le type de **variable**, pas le nom.

> [!example]-
> Si on a déclaré une **fonction** `ftputchar` comme suit :
> ```C
> void ft_putchar(char a) {
> 	//Code of the function
> 	}
> ```
> 
> Et qu'on veut l'utiliser dans un autre fichier ou elle n'est pas déclaré, on va devoir mettre ce prototype tout en haut du fichier :
> ```C
> void ft_putchar(char);
> ```

On pourra ensuite l'appeler avec son nom et ses paramètres normalement.

> [!example]-
> En reprenant l'exemple plus haut, on pourra utiliser `ft_putchar` comme suit :
> ```C
> void ft_putchar(char);
> 
> int main(void)
> 	{
> 	ft_putchar("b");
> 	
> 	return 0
> 	}
> ```
> 
> Le programme exécutera la `ft_putchar` avec comme paramètre le `char` "b".

> [!info]-
> Si l'on souhaite appeler une **fonction** qui ne prend pas de paramètres, (déclarée et prototypée avec `void`), on doit tout de même inclure les `()` à la fin, même si elles sont vide.

<br>

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

# Les pointeurs :

- Pour comprendre les **pointeurs**, il faut comprendre le stockage des **variables** :
    - Les **variables** stockent leurs valeurs dans des cases de la mémoire, correspondant à un numéro.
    - Si on initialise un `int i` à 465, 465 sera stocké sur une case de la mémoire correspondant à un numéro spécifique, qui permet de la retrouver.
    - On appelle ce numéro spécifique l'**adresse** de `i`.
- Un **pointeur** est une variable qui stockera comme valeur l'**adresse** d'une autre variable. C'est donc une **variable** qui va "pointer" sur une autre **variable**.
	- Un **pointeur** se déclare et s'utilise selon  une syntaxe particulière.
	- Si l'on veut déclarer un **pointeur**, il faudra le déclarer comme suit :
		- `int *p_i;`
		- C'est un type `int`, puisqu'il stocke une **adresse**, donc un nombre. Mais ce n'est pas un simple type `int`, avec l'"`*`", on indique que c'est un **pointeur** vers une **variable**.
		- Pour lui assigner l'**adresse** d'une **variable**, on utilise `&`. `&i` correspond à l'**adresse** à laquelle est stockée la valeur de `i`. Donc ici, on pourra lui assigner cela comme suit : `p_i = &i;`.
		- Ensuite, si l'on manipule `p_i`, on manipule l'**adresse** qu'il stock. pour manipuler la **variable** pointée par `p_i`, on utilisera `*p_i`.
- Un **pointeur** servira notamment à modifier des variables qu'on enverra dans des **fonctions**. En effet, puisque celle-ci utilisent une copie de la **variable** qu'on lui donne et la supprime à la fin, si on lui envoie un **pointeur**, et qu'il manipule la **variable** pointée par le **pointeur** donné en paramètre, cela nous permettra de modifier cette **variable**. Puisque même si l'on fait une copie du **pointeur**, celle ci pointera vers la même **adresse**, ainsi modifiera la vraie **variable** tout de même.

<br>

# To-do (sujets à aborder ici) :

- `static`
- `const`