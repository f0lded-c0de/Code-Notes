# Custom Functions :

## ft_put()

```C
void ft_putchar(char c);
```

^62035e

`ft_putchar()` affiche dans le **stdout** le `char c` spécifié.
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
`ft_putnbr()` affiche dans le **stdout** le `int i` spécifié. 
> [!declaration]- Declaration 1
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

> [!declaration]- Declaration 2
> ```C
> void    ft_putnbr(int nb)
> {
> 	if (nb < -9 || nb > 9)
> 	{
> 		ft_putnbr(nb / 10);
> 		if (nb > 0)
> 			ft_putnbr(nb % 10);
> 		else
> 			ft_putnbr((nb % -10) * -1);
> 	}
> 	else
> 	{
> 		if (nb < 0)
> 		{
> 			ft_putchar('-');
> 			nb *= -1;
> 		}
> 		ft_putchar(nb + 48);
> 	}
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
`ft_putstr()` affiche dans le **stdout** la **string** pointée par `*str`.
> [!declaration]-
> ```C
> void ft_putstr(char *str)
> {
> 	int i;
> 
> 	i = 0;
>     while (str[i] != '\0')
>         write(1, &str[i++], 1);
> }
> ```
> > [!list]- Fonctions utilisées
> > **Librairie** : [[C - Function List#<unistd.h >|<unistd.h>]] :
> > - [[C - Function List#^5a0e90|write()]]

<br>

## ft_str_manipulation()

```C
int ft_strlen(char *str)
```
`ft_strlen()` renvoie le nombre de caractères qui composent la **string** pointée par `str`.

> [!declaration]-
> ```C
> int	ft_strlen(char *str)
> {
> 	int	i;
> 
> 	i = 0;
> 	while (str[i] != 0)
> 		i++;
> 	return (i);
> }
> ```

<br>

```C
char *ft_strcpy(char *src, char *dest);
```
`ft_strcpy()` copie le contenu de la **string** pointée par `src` dans la **string** pointée par `dest`. 
- Si `*src` est plus petit que `*dest`, `ft_strcpy` n'agira que jusqu'au `\0` de `*src`.
- `ft_strcpy()` ne gère pas le cas où `*dest` serait plus petit que `*src`.

> [!declaration]-
> ```C
> char *ft_strcpy(char *src, char *dest)
> {
> 	int	i;
> 
> 	i = 0;
> 	while (src[i] != '\0')
> 		dest[i++] = src[i];
> 	dest[i] = '\0';
> 	return (dest);
> }
> ```

<br>

```C
char *ft_strncpy(char *src, char *dest, unsigned int n);
```
`ft_strcpy()` copie les `n` premiers caractères du contenu de la **string** pointée par `src` dans la **string** pointée par `dest`. 
- Si `*src` est plus petit que `n`, la fin de `*dest` sera remplie de `\0`.
- **Attention**! S'il n'y a pas de `\0` dans les `n` premiers caractères de `*src`, alors `*dest` n'en contiendra pas.

> [!declaration]-
> ```C
> char	*ft_strncpy(char *dest, char *src, unsigned int n)
> {
> 	int	i;
> 
> 	i = 0;
> 	while (src[i] != '\0' && i < n)
> 		dest[i++] = src[i];
> 	while (i < n)
> 		dest[i++] = '\0';
> 	return (dest);
> }
> ```

<br><br><br>

# Existing Libraries

Pour inclure une librairie spécifique : `#include <library.h>` en haut du fichier.

### \<unistd.h\>

^92b549

```C
write(int fd, truc, size_t count)
```

^5a0e90

`write` permet d'envoyer un `truc` de taille `count` au `fd` spécifié.
- `int fd` nous permet de choisir à quel [[C - Overview#File Descriptor (ou Descripteur)|File Descriptor]] renvoyer `truc`.
	- Si l'on veut simplement afficher `truc` à l'écran, comme un `printf()`, on doit donc choisir `1`, pour **stdout**.
- `truc` peut être différentes choses :
    - Une simple variable de type `char`, que l'on peut appeler avec `&truc`.
	    - On mettra donc bien `size_t` à 1.
    - Un chaine de caractères, que l'on écrit comme cela : `"truc"`.
	    - On mettra ici `size_t` égale au nombre de caractères de la chaine.
- `size_t count` est une **variable** de type `size_t`, qui correspond à la taille de ce que l'on souhaite afficher.



