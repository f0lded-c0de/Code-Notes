# Custom Functions :

```C
void ft_putchar(char c);
```
`ft_putchar` affiche dans le **stdout** le `char c` spécifié.
> [!declaration]-
> ```C
> void ft_putchar(char c)
> {
> 	write(1, &c, 1);
> }
> ```
> > [!list]- Fonctions utilisées
> > **Librairie** : [[C - Function List#<unistd.h >|<unistd.h>]] :
> > - [[C - Function List#^5a0e90|write()]]

<br>

# Existing Libraries
## \<unistd.h\>

^92b549

```C
write(int fd, truc, size_t count)
```

^5a0e90

`wite` permet d'envoyer un `truc` de taille `count` au `fd` spécifié.
- `int fd` nous permet de choisir à quel **File Descriptor**<sub>[[C - Overview#File Descriptor (ou Descripteur)|more]]</sub> renvoyer `truc`.
	- Si l'on veut simplement afficher `truc` à l'écran, comme un `printf()`, on doit donc choisir `1`, pour **stdout**.
- `truc` peut être différentes choses :
    - Une simple variable de type `char`, que l'on peut appeler avec `&truc`.
	    - On mettra donc bien `size_t` à 1.
    - Un chaine de caractères, que l'on écrit comme cela : `"truc"`.
	    - On mettra ici `size_t` égale au nombre de caractères de la chaine.
- `size_t count` est une **variable** de type `size_t`, qui correspond à la taille de ce que l'on souhaite afficher.



