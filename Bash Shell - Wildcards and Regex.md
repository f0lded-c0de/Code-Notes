# Wildcards (métacaractères) :

- `*` : Correspond à 0 ou plus d'occurences de n'importe quel caractères ou pattern.
- `?` : Correspond à 1 occurence de n'importe quel caractère.
- `[]` : Correspond à 1 occurence de n'importe quel caractère mentionné entre les `[]`.
	- `[a-z]` : Pour spécifier une plage de caractères (ici de `a` à `z`).
	- `[!abc]` : Pour exclure les pattern correspondant au lieu de les inclure (ici correspond à 1 occurence de n'importe quel caractère excepté `a`, `b`, ou `c`).
		- Cherche tout de même 1 occurence d'un caractère. 
		> [!example]-
		> Prenons 3 fichier `file.txt`, `filea.txt`, et `fileb.txt`.
		> ```bash
		> ls file[!a].txt
		> ``` 
		> Ceci excluera certes `filea.txt`, mais aussi `file.txt` car `[!a]` correspond à 1 caractère, il exclue juste dans la recherche les caractères spécifiés.
	- `{}` à la place de `[]` : Permet de spécifier une liste/plage de caractères/patterns séparés par des virgules.
- `+` : Correspond à 1 ou plus d'occurences du caractère/pattern précedent le "`+`".
- `\` : Permet d'échapper le caractère suivant le "`\`". Cela signifie que même si le caractère en question est aussi un **métacaractère**, alors il sera quand même traité comme le caractère normal.

<br>

# Extended Regular Expression (ERE, regexp) :

Expressions courantes :
- `.` : Correspond à 1 occurence de n'importe quel caractère.
- `[]` : Correspond à 1 occurence de n'importe quel caracère mentionné entre les `[]`.
	- `[a-z]` : Pour spécifier une plage de caractères (ici de `a` à `z`).
	- `[^abc]` : Pour exclure les pattern correspondant au lieu de les inclure (ici correspond à 1 occurence de n'importe quel caractère excepté `a`, `b`, ou `c`).
- `^` : Correspond au début de la **string** ou de la ligne.
- `$` : Correspond à la fin de la **string** ou de la ligne.
	- Astuce : Si l'on cherche une ligne ou une **string** vide, le pattern `^$` fonctionne, puisque qu'il cherche une ligne ou une **string** dont le début et la fin sont collés, sans caractères entre les 2.
- `|` : Représente l'opérateur "**OU**" logique, pour désigner soit un pattern, soit un autre.
> [!example]-
> `abc|def` : Correspond soit à `abc`, soit à `def`.
- `()` : Permet de grouper/capturer une expression, par exemple pour mettre un **ou** à l'intérieur d'un pattern, ou pour appliquer les quantificateurs (voir ci-dessous) sur une expression de plusieurs caractères plutôt que sur un simple caractère.
> [!example]-
> - `a(bc|de)f` : Correspond soit à `abcf`, soit à `adef`.
> - `(abc)+` : Correspond à 1 ou plus d'occurences de l'expression `abc`. (Par exemple `abcabcabc`).

On peut aussi y ajouter des **quantificateurs**, qui nous permettent de préciser combien on cherche du caractère précédent directement le **quantificateur** :
- `*` : Correspond à 0 ou plus d'occurences du caractère précédent.
- `+` : Correspond à 1 ou plus d'occurences du caractère précédent.
- `?` : Correspond à 0 ou 1 occurence du caractère précédent.
- `{n}` : Correspond à `n` occurences du caractère précédent.
> [!example]-
> - `a{2}` : Correspond à 2 occurences de `a`.
> - `a{1,10}` : Correspond à entre 1 et 10 occurences de `a`.
> - `a{,10}` : Correspond à jusqu'à 10 occurences de `a` (de 0 à 10).
> - `a{6,}` : Correspond à au moins 6 occurences de `a` (de 6 à l'infini).

