```bash
git add [file]
```
Ajoute `[file]` à l'**index**<sub>[[Git - Overview#^543278|index]]</sub>. `[file]` peut être aussi bien un fichier qu'un répertoire.

<br>

```bash
git branch (option) (branch)
```
Effectue diverses actions en rapport avec les **branches**. Si aucun argument n'est donné, va simplement renvoyer une liste des **branches** présentes localement. Si `(branch)` est précisé, toujours sans autre arguments, créé la **branche**. Si elle existe, ne fait rien.
> [!arg]- Option
> - `-a` : Sans `(branch)` de précisé, liste aussi les **branches** distantes en plus des locales.
> - `-r` : Idem, sans les **branches** locales.
> - `--merged` : Ne liste que les **branches** qui ont été **merge** dans la **branche** actuelle.
> - `--no-merged` : Ne liste que les **branches** qui n'ont pas été **merge** dans la **branche** actuelle.
> - `-d` : Supprime `(branch)`, seulement si tous les changements ont déjà été **merge** dans d'autres **branches**.
> - `-D` : Supprime `(branch)` même si tous les changements n'ont pas été **merge** dans d'autres **branches**.
> - `-m [old_name] [new_name]` : Renomme la **branche** `[old_name]` en `[new_name]`.

<br>

```bash
git checkout (option) (branch)/(commit)
```
Permet de se déplacer sur la **branche** `(branch)`, ou le **commit** `(commit)`.
> [!arg]- Option
> - `-b` : Créé `(branch)` puis se déplace dessus. Revient à faire `git branch (branch)` puis `git checkout (branch)`.

```bash
git commit (option)
```
Créé un nouveau **commit** incorporant tous les changements contenu dans l'**index**. Ce **commit** descendra directement du **commit** *HEAD* (**commit** sur lequel nous étions au moment de créer le nouveau/à partir duquel on créé le nouveau). HEAD descendra donc sur le nouveau **commit**, et la **branche** (si l'on est dans une **branche**) se déplacera pour pointer sur ce nouveau **commit**. Associer un "message de **commit**" est fortement recommandé. En l'absence d'options spécifiques modifiant le comportement de la commande par rapport au message de **commit**, `git commit` ouvrira un éditeur de texte dans lequel on pourra l'écrire.
> [!arg]- Option
> - `-a` : Effectue l'équivalent d'un `git add` pour tous les fichiers modifiés ou supprimés. N'ajoutera pas de fichiers n'étant pas encore suivis par git, mais en dehors de ça, permet de simplifier le processus de **commit** en réunissant l'étape d'ajout des changements à l'**index** et l'étape de création d'un **commit** pour ces changements en une seule ligne de commande.
> - `--amend` : Permet de modifier le dernier **commit** effectué. À utiliser avec parcimonie : cela remplace le **commit** par un nouveau, changeant notamment le **commit hash**. Permet d'intégrer les changements ajouté à l'**index** au **commit** en question, ainsi que de modifier le message de **commit**.
> - `-m "[commit message]"` : Permet d'écrire le message de **commit** directement dans la ligne de commande. Permet moins de flxibilité quand à la structure du message, mais pour des message simple/court, cette manière de fonctionner est elle-même plus simple et courte que normalement.
> - `-e` : Ouvre un éditeur pour écrire le message de **commit** (fonctionnement de base de la commande).

<br>

```bash
git fetch
```
Met à jour la **remote-tracking branch**<sub>[[Git - Overview#Remote-tracking branch|remote-tracking branch]]</sub> avec les dernières modifications du **dépôt distant**, sans les appliquer sur notre **branche** locale.

<br>

```bash
git init
```
Initialise un répertoire git, transformant le répertoire courant.

<br>

```bash
git log (option)
```
Affiche le registre des **commits**.
> [!arg]- Option
> - `-n [number]` : N'affiche que les `[number]` derniers **commits**. `-[number]` fonctionne aussi.
> - `--skip=[number]` : Ignore les `[number]` dernier **commits**.
> - `--since=[date]` : Affiche uniquement les **commits** plus récents que `[date]`.
> - `--until=[date]` : Idem, mais pour les **commits** plus vieux que `[date]`.
> - `--grep=[pattern]` : N'affiche que les **commits** dont le message match `[pattern]`. (**regex**)
> 	- Si plusieurs `--grep=[pattern]`, tout **commit** dont le message match au moins 1 `[pattern]` sera affiché.
> 	- `--all-match` annule ça. Les **commits** doivent match tous les `[pattern]` pour être affiché.
> 	- `--invert-grep` : Affiche tous les **commit** qui ne matchent PAS avec `[pattern]`. (Exclue les **commits** qui matchent.)
> - `--pretty=[format]` : Permet de spécifier le `[format]` dans lequel on va afficher les **commits**.
> 	- Les `[formats]` prédéfinis :
> 		- `oneline` : **Id** et titre du **commit**, en une ligne.
> 		- `short` : **Id**, auteur, et titre du **commit**.
> 		- `medium` : **Id**, auteur, date, titre, et message complet du **commit**.
> 		- `reference` : **Id** abrégé, titre et date du **commit**. Format utilisé pour se référer a un autre **commit** dans un message de **commit**.
> 		- `email` : Format adapté aux mails.
> 	- On peut aussi donner une **string** en `[format]`, en utilisant ces raccourcis dans la **string** :
> 		- `%n` : Newline
> 		- `%H` : **Id** du **commit** (`%h` : **id** abrégé)
> 		- `%T` : **Id** de l'arbre (`%t` : **id** abrégé)
> 		- `%P` : **Id** du parent (`%p` : **id** abrégé)
> 		- `%a[]` :
> 			- `an` : Nom de l'auteur
> 			- `ae` : Email de l'auteur
> 			- `ad` : Date de l'auteur (du **commit**)
> 		- `%s` : Titre du **commit**
> 		- `%b` : Message du **commit**

<br>

```bash
git ls-files (option)
```
Affiche la liste des fichiers du répertoire git.
> [!arg]- Option
> - `-io --exclude-standard` : Permet d'afficher la liste des fichiers ignorés par git.
> - `--exclude-standard` : **Exclude pattern** standard de git. L'**exclude pattern** est la liste de règles qui vont définir quels fichiers sont ignorés. Ici, `--exclude-standard` désignant les règles de bases, ce sont les règles spécifiés dans le .gitignore.
> - `-i` : Utilise l'**exclude pattern** spécifié afin d'afficher spécifiquement les fichiers exclus par ce pattern.
> - `-o` : Permet de chercher dans les fichiers "non-suivis" par git, ce qui est nécessaire afin de trouver les fichiers ignorés.

<br>

```bash
git merge [source_branch]
```
Incorpore les changements qui ont été effectués sur la **branche** `[source_branch]` depuis le dernier **commit** en commun entre la **branche** actuelle et la **branche** `[source_branch]` à la **branche actuelle**. Créé un **commit** de **merge** possédant 2 **commits** parents.

<br>

```bash
git pull
```
Combine un `git fetch` et un `git merge`. Applique directement les modifications que `fetch` rapporte.

<br>

```bash
git push (option) (remote) (branch)
```
Applique sur la **branche** `branch` du **dépôt** distant `remote`, tous les changements effectués en local sur `branch`. `remote` ne devient optionnel que si cela a été configuré auparavant, par exemple avec `-u`. Si `branch` n'est pas spécifié, Git prendra la **branche** courante par défaut.
> [!arg]- Option
> - `--all` : Push toutes les **branches** au lieu de seulement celle spécifiée.
> - `-u` : Configure un lien entre `branch` locale et `branch` sur `remote`. Après cela, on peut push `branch` sur `remote` en étant dessus et en tapant just "git push".

<br>

```bash
git remote (action)
```
Permet de gérer le (ou les) **dépôt(s) git** distants associés à notre **dépôt git** local. En général il y en a un seul : **origin**, qui est le **dépôt** central de référence pour tous les développeurs travaillant sur le projet. Si aucune action n'est spécifié dans la commande, elle renverra simplement une liste des **dépôts** distants auquel notre **dépôt** local est associé.
> [!arg]- Action
> - `add [name] [url]` : Associe le **dépôt** distant correspondant à `[url]` au **dépôt** local. On attribue le nom `[name]` à ce **dépôt** distant dans le cadre du **dépôt** local.
> - `rename [old_name] [new_name]` : Renomme le **dépôt** distant auparavant nommé `[old_name]` en `[new_name]`.
> - `remove [name]` : Supprime le **dépôt** distant `[name]` de la liste des **dépôts** distants associés au **dépôt** local.
> - `get-url [name]` : Renvoie l'**url** du **dépôt** distant `[name]`.
> - `show [name]` : Renvoie une liste d'informations sur le **dépôt** distant `[name]`.

<br>

```bash
git restore (option) (file)
```
Restaure `(file)` à sa version dans le dernier commit. Par défaut, ne restaure que le fichier dans le **répertoire de travail**, mais ne touche pas à l'**index**.
> [!arg]- Option
> - `--staged` : Inverse le comportement par défaut : ne restaurera le fichier que dans l'**index**. Cela annulera les modifications enregistrée dans l'**index** qui auraient été incluses dans le prochain **commit**, mais ne touche pas au fichier dans le **répertoire de travail**.
> - `--worktree` : À utiliser avec `--staged` si on veut restaurer le fichier à la fois dans l'**index** et à la fois dans le **répertoire de travail**.
> - `-s (commit)/(branch)` : Utilise la version de `(file)` du **commit** `(commit)` ou de la **branche** `(branch)` au lieu d'utiliser le dernier **commit** comme réference. (`--source=(commit)/(branch)`)

<br>

```bash
git rm (option) [file]
```
Supprime `[file]` du répertoire de travail et ajoute la suppression de `[file]` à l'**index** (revient à faire `rm [file]` puis `git add [file]`).
> [!arg]- Option
> - `--cached` : N'ajoute que la suppression dans l'**index**, `[file]` reste intact dans le répertoire de travail. Si la suppression est confirmée par un **commit**, le fichier sera toujours présent sur le répertoire de travail local, mais sera vu par Git comme un fichier non-suivi, comme si le fichier venait d'être créé et n'avait pas encore été ajouté à Git.

<br>

```bash
git status
```
Affiche l'état du répertoire de travail.
- Affiche les fichiers/repertoires qui sont différents entre l'**index** et le **commit** HEAD courant.
- Affiche les fichiers/repertoires qui sont différents entre le répertoire de travail et l'**index**.
- Affiche les fichiers/repertoires qui ne sont pas suivis par Git (et qui ne sont pas ignorés par .gitignore).







