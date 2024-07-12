# Custom Functions :

```C
void ft_putchar(char c);
```

^62035e

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

```C
void ft_putnbr(int i);
```
`ft_putnbr` affiche dans le **stdout** le `int i` spécifié. 
> [!declaration]-
> ```C
> void ft_putnbr(int nb)
> {
> 	if (nb > 9 || nb < -9)
> 	{
> 		if (nb < 0)
> 		{
> 			ft_putchar('-');
> 			ft_putnbr((nb / 10) * -1);
> 			ft_putnbr((nb % 10) * -1);
> 		}
> 		else
> 		{
> 			ft_putnbr(nb / 10);
> 			ft_putnbr(nb % 10);
> 		}
> 	}
> 	else if (nb < 0)
> 	{
> 		ft_putchar('-');
> 		ft_putchar((nb * -1) + 48);
> 	}
> 	else
> 		ft_putchar(nb + 48);
> }
> ```
> > [!list]- Fonctions utilisées
> > **Custom** :
> > - [[C - Function List#^62035e|ft_putchar()]]
> > 
> > **Librairie** : [[C - Function List#<unistd.h >|<unistd.h>]] :
> > - [[C - Function List#^5a0e90|write()]]

<br>

```C
void ft_putstr(char *str);
```
`ft_putstr` affiche dans le **stdout** la **string** dont le premier charactère est pointée par `char *str`.
> [!declaration]-
> ```C
> void ft_putstr(char *str)
> {
> 	int i;
> 
> 	i = 0;
>     while (str[i] != '\0')
>     {
>         write(1, &str[i], 1);
>         i++;
>     }
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
- `int fd` nous permet de choisir à quel [[C - Overview#File Descriptor (ou Descripteur)|File Descriptor]] renvoyer `truc`.
	- Si l'on veut simplement afficher `truc` à l'écran, comme un `printf()`, on doit donc choisir `1`, pour **stdout**.
- `truc` peut être différentes choses :
    - Une simple variable de type `char`, que l'on peut appeler avec `&truc`.
	    - On mettra donc bien `size_t` à 1.
    - Un chaine de caractères, que l'on écrit comme cela : `"truc"`.
	    - On mettra ici `size_t` égale au nombre de caractères de la chaine.
- `size_t count` est une **variable** de type `size_t`, qui correspond à la taille de ce que l'on souhaite afficher.



