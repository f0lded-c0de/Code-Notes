Git est un logiciel de gestions de versions de projet décentralisé. Il permet de conserver l'historique des différentes versions/modifications d'un projet. Il permet aussi avec son système de **branches** de travailler sur différentes parties spécifiques d'un projet de manière isolée pour éviter toute sortes de conflits.

# "Décentralisé" ou fonctionnement des dépôts Git :

La structure de Git repose autour d'un **dépôt git** (ou **git repository**), qui représente l'ensemble du code du projet, et surtout l'ensemble de l'historique des versions de celui-ci. Il inclut l'état actuel du projet dans son intégralité, ainsi que l'intégralité de toutes les versions précedentes. Et ce pour chaques branches : la totalité de "l'arbre" est enregistré sur ce **dépôt**.

La notion de "décentralisé" fait référence à l'organisation du travail des différents développeurs sur le projet. En effet, contrairement à ce que "décentralisé" pourrait laisser entendre, Git fonctionne avec un **dépôt** central, généralement géré sur un serveur distant, accessible par tous les développeurs qui travaillent sur le projet. Ce **dépôt** est une sorte de référence commune, la version officielle du projet. C'est comme ça que fonctionne la plupart des systèmes de gestion de versions. La différence entre Git (en tant que système "décentralisé") par rapport à des systèmes dit "centralisés" se situe au niveau du rapport des développeurs à ce **dépôt** central :
- Dans un système dit **centralisé**, les développeurs travaillent toujours directement sur ce **dépôt** central. Le terme central n'est même plus réellement pertinent, puisque c'est le seul **dépôt** existant.  Cela amène quelques avantages par rapport à un système décentralisé, dont en voici une liste non-exhaustive :
	- Simplicité d'utilisation : La navigation, l'utilisation, et la compréhension générale des processus, est largement simplifié dans un système centralisé. Il n'y a qu'un seul **dépôt** à gérer.
	- État Cohérent : Étant donné que les développeurs travaillent directement sur le dépôt central, tout le monde est toujours synchronisé avec la dernière version du code. Il n'est pas nécessaire de gérer les complexités de la synchronisation et de la fusion des modifications provenant de différentes branches ou dépôts.
	- Collaboration Simplifiée : Avec un système centralisé, la collaboration entre les membres de l'équipe peut être facilitée. Les développeurs peuvent partager et accéder facilement aux dernières modifications, ce qui simplifie la coordination et le suivi de l'évolution du projet.
- Dans un système dit **décentralisé**, les développeurs travaillent sur une copie local du **dépôt** central. On parlera alors de "**dépôt distant**" ("**remote repository**") pour désigner le **dépôt** central, officiel, commun, et de "**dépôt local**" ("**local repository**") pour désigner un clone local. Chaque développeur travaille ainsi sur sa propre copie locale du **dépôt distant**. Cela amène beaucoup d'avantages par rapport à un système dit centralisé, dont en voici une liste non-exhaustive :
    - Tolérance aux pannes : Chaque développeur dispose d'une copie complète du dépôt, ce qui évite les points de défaillance uniques. Si le serveur central devient indisponible, les développeurs peuvent continuer à travailler sur leurs dépôts locaux. Le dépôt peut également être restauré à partir de la copie locale de n'importe quel développeur, chaque **dépôt local** représentant en quelque sorte un **backup** indépendant du **dépôt distant**.
    - Opérations plus rapides : La plupart des opérations Git sont effectuées localement, sans nécessité d'accès au réseau. Cela permet d'effectuer rapidement et efficacement des opérations telles que la validation, la création de branches, la fusion et la visualisation de l'historique.
    - Flexibilité et autonomie : Les développeurs ont un plus grand contrôle sur leurs propres dépôts. Ils peuvent expérimenter, créer des branches, tester de nouvelles fonctionnalités et facilement annuler des modifications si nécessaire. Chaque développeur peut choisir quand et comment incorporer les modifications apportées par les autres, offrant ainsi plus d'autonomie dans le processus de développement.

<br>

# Commit :

## Historique des commits :

Un **dépôt** git se structure en ce que l'on va appeler une "chaîne de **commits**".

- Un **commit** est une version à un point donné du projet, qui pointe sur le(s) **commit(s)** sur lesquels il est basé (ou **commit parent**). 
	- Concrètement, on travaille sur un **commit** spécifique (*commit a*) (généralement le plus récent). Lorsqu'on va effectuer des modifications sur le projet à partir de ce *commit a*, on va ensuite créer un nouveau **commit** pour enregistrer ces modifications, (*commit b*). Le *commit b* va donc pointer sur le *commit a*, son **commit parent**. Cela va créer une chaine de **commit**, représentant l'historique de toutes les modifications remontant jusqu'au **commit** initial, première version enregistrée du projet. On peut donc remonter cet historique et revenir à n'importe quelle version antérieur du projet.
    - Un **commit** peut avoir plusieurs **commits parents**, mais cela est le résultat d'une opération plus spécifique, **git merge**, qui sera traité plus tard.
- **Commit Hash** :
    - Lorsqu'on crée un **commit**, Git va enregistrer toutes les modifications inclues dans celui-ci, et y associer un ID unique. Cet ID identifie : les changements eux-même, la date de ces changements, et leur créateur. On appelle cet ID le **commit hash**. C'est ce **hash** qui permet d'accéder à un **commit**, et donc de naviguer entre les **commits**. Quand on dit que quelque chose (autre **commit**, **branche**, etc) pointe vers un **commit**, il pointe en fait vers le **hash** de celui-ci.
- **HEAD** :
    - Le **commit HEAD** est le commit actuel, celui sur lequel on travaille actuellement.

## Faire un commit :

Il y a 2 étapes quand on veut faire un **commit**, qui peuvent être représentée par les 2 commandes qui permettent de les réaliser.

- `git add` : Ajoute toutes les modifications qu'on veut inclure dans le **commit** à l'**index**. ^543278
	- L'**index** est la "zone de préparation au **commit**. C'est là que sont stockée toutes les modifications qui seront inclues dans le prochain **commit**. Toute modification n'étant pas dans l'**index** ne fera pas parti du prochain **commit**.
- `git commit` : Créé un nouveau **commit** incorporant tous les changements contenu dans l'**index**.

<br>

# Branches :

Les **branches** permettent de travailler sur différentes parties du projets sans que celles-ci rentrent en conflit. On peut voir les branches comme des lignes de développements séparées. C'est, de manière plus générale, le système qui nous permet de naviguer entre les commits.

- On va avoir une **branche** centrale, (généralement **master**), qui va représenter l'état actuel global "officiel" du projet, et son historique. De cette **branche master** découleront différentes **branches**, concentrées sur une partie spécifique du projet.
	- Les différentes **branches** sont toutes constituées d'une copie complète du projet, pas seulement des parties pertinente à la fonctionnalité en question. C'est pour organiser le travail qui sera effectué sur ces différentes fonctionnalités qu'on utilise les **branches**, pas pour diviser le contenu du projet lui même.
	- Cela donne une structure en arbre, avec un "tronc commun", la **branche master**, et ensuite une structure d'arbres. Les **branches** partent d'un **commit** spécifique.
		- En principe, dans l'idéal, les branches partent du **commit** le plus récent de la **branche** **parent**.
	- Lorsqu'une fonctionnalité est terminée, on va l'incorporer à la **branche master**. On utilisera un processus appelé **merge**, qu'on traitera plus en détail plus tard. Mais revenons sur son fonctionnement de base :
		- On va appeler la **branche** depuis laquelle on effectue le **merge** "**branche source**", et la **branche** sur laquelle on effectue le **merge** (ici **master**) "**branche de destination**".
		- L'action du **merge** rajoutera un nouveau **commit** à l'historique de la **branche de destination**, appelé **commit de merge**. Ce **commit** deviendra par définition le dernier de l'historique de la **branche de destination**. Ce **commit** repertorie toutes les modifications faites sur la **branche source** depuis le **commit** dont celle-ci part.
		- Il a 2 **commits parents** :
			- Le dernier **commit** de la **branche de destination**, par définition antérieur aux modifications effectuées sur la **branche source**
			- Le dernier **commit** de la **branche source**, par définition incluant toutes les modifications effectuées sur cette **branche source**.
    

Les **branches** qui étaient déjà en cours, qui partaient donc d'un **commit** antérieur à l'ajout de cette fonctionnalité, vont devoir s'actualiser pour pouvoir à terme s'incorporer elles aussi à **master**. Ici aussi on utilisera **merge**. Cela permettra de rattacher la **branche** à la version la plus récente du projet, tout en conservant l'historique de **commits** de la **branche**, en créant ici aussi un **commit de merge** qui aura pour parents à la fois le dernier **commit** de **master**, ainsi que le dernier **commit** de la branche, antérieur au **merge**.

Tout cela nous permet aussi bien d'organiser notre travail sur un projet personnel, afin de ne pas se mélanger entre les différentes fonctionnalités sur lesquels ont travaille en même temps, mais cela permet aussi et surtout de travailler à plusieurs sur un même projet, répartissant les tâches entre chaques développeurs, ces derniers travaillant chacun sur leur(s) **branches** afin de ne pas interferer avec le travail des autres tant que l'objet du travail personnel d'un développeur n'est pas terminé.

> [!example]- 
> Prenons en exemple un projet de jeu vidéo sur lequel plusieurs développeur travaillent ensemble :
> - On a un prototype du projet, représenté par le **commit** le plus récent de la *branch master* (qu'on va appeler *commit x*).
> - Un développeur veut rajouter une nouvelle fonctionnalité : créer une **IA** pour les ennemis. Il va donc créer une **branche** qu'il va appeler *branch a* pour travailler sur cette fonctionnalité, qui part du *commit x*. Cela va créer un *commit a* initial pointant vers le *commit x*.
> - En même temps, un autre développeur qui travaille sur le jeu veut lui créer une fonctionnalité permettant de générer procéduralement des cartes. Il va donc créer une *branch b* à partir du *commit x*, créant lui aussi un *commit b* initial pointant sur le *commit x*.
> - Les 2 développeurs avancent chacun sur leur fonctionnalités, créants chacun plusieurs _commits_ (*commit a1*, *a2*, *a3*, etc...; *commit b1*, *b2*, *b3*, etc...) sur leurs **branches** réspectives.
> - Le développeur travaillant sur la *branch b* finit sa fonctionnalité, il a réussit a créer une génération procédurale de map fonctionnelle.
> 	- Il en est arrivé à un *commit b7*.
> 	- Il va donc **merge** la *branch b* sur la *branch master*_._
> 	- Cela va créer un **commit de merge** qu'on va nommer *commit b7_x*. Celui-ci aura pour parents le *commit x* et le *commit b7*. Ce sera dès lors le **commit** le plus récent de *master*.
> 	- Cela permet notamment de pouvoir voir l'historique des différentes fonctionnalités ajoutées/modifiées en suivant l'historique de *master*, mais aussi de pouvoir remonter l'historique spécifique à un ajout/modification de fonctionnalité, puisque les 2 parents sont connectés au **commit de merge**.
> - Le développeur travaillant sur la *branch a* va donc devoir actualiser sa **branche**, pour continuer à travailler sur la version à jour du projet.
> 	- Il en est arrivé à un *commit a5*.
> 	- Il va donc **merge** la *branch master* sur la *branch a*_._
> 	- Cela va créer un **commit de merge** qu'on va nommer *commit (b7_x)_a5*. Celui-ci aura pour parents le *commit b7_x* et le *commit a5*. Ce sera dès lors le **commit** le plus récent de la *branch a*.
> 	- Cela lui permettra notamment de continuer à travailler sur sa fonctionnalité à partir de là où il en était (*a5*), tout en étant à jour sur la version commune la plus récente du projet (*b7_x*), incorporant notamment la génération procédurale de map (*b7*).
> 
> PS : Les noms de _commits_ ici sont inutilement compliqués dans le contexte d'un réel projet et ne prennent jamais cette forme, mais servent dans notre exemple à mieux illustrer comment interagissent les différents historiques des différentes _branches_.  

Intéressons nous au fonctionnement des **branches** sur le plan technique. Bien qu'il ne soit pas nécessaire de comprendre cela pour utiliser Git, cela peut aider à avoir une compréhension plus globale et donc plus solide du système de **branches**. Si l'explication qui suit n'est pas assez claire, trop compliquée à comprendre, trop fouillie, il est intutile de s'attarder dessus : ce n'est absolument pas essentiel.
- Fondamentalement, une **branche** est un **pointeur** déplaçable qui pointe sur le **hash** du dernier **commit** de la ligne de développement. Il va se déplacer à chaque création de **commit** dans la ligne de développement pour toujours pointer sur le dernier **commit** en date. On va appeler couramment cette ligne de développement du nom de la **branche** qui pointe sur le dernier **commit** de la-dite ligne de développement.
	> [!example]-
	> Reprenons l'exemple du jeu vidéo dans le paragraphe précédent :
	> 
	> - *master* est un pointeur qui, au début de l'exemple, pointe sur le **hash** du *commit x*.
	> - Quand le premier développeur créé la *branch a*, il créé en fait juste 2 choses :
	> 	- Le *commit a* initial, dont le parent direct est le *commit x*
	> 	- Un pointeur "*branch a*" qui pointe sur le *commit a*.
	> - Au fur et à mesure qu'il avance et créé des *commits a1*, *a2*, *a3*, etc..., *branch a* se déplace pour pointer sur le plus récent.
	> - Situation identique pour la *branch b*.
	> - Quand le deuxième développeur finit sa fonctionnalité, *branch b* pointe donc sur le *commit b7*, *branch a* sur le *commit a5*, et *master* toujours sur le *commit x*.
	> - En **mergeant** la *branch b* sur *master*, on créé le **commit de merge** *b7_x*.
	> - *master* va donc se déplacer pour pointer sur le *commit b7_x*.
	> - De même, en **mergeant** ensuite la *branch master* sur la *branch a*, on créé le **commit de merge** *(b7_x)_a5*.
	> - *branch a* va donc se déplacer pour pointer sur le *commit (b7_x)_a5*.

Puisque chaque **commit** pointe déjà par définition sur ses **commits parents**, il n'est nécessaire pour répertorier et naviguer entre les différentes **branches** et leur historique que de pointer sur le dernier **commit** en date de la **branche** en question. Tous les **commits** antérieurs seront par définition accessible depuis le dernier **commit**.