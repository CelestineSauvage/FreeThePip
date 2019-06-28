# Utiliser FreeSpec pour vérifier une partition

## L'exemple de l'allocateur de page

Il faut être capable de parler de la façon dont la partition
gère ses pages mémoires. En effet, en plus de pouvoir lire ou
écrire dedans, certaines pages peuvent également devenir inaccessible
à la partition lorqu'elle les donne à ses filles.

On peut vouloir gérer cela de différents façons :

Comme avoir un allocateur de pages sous la forme d'un groupe de
fonctions d'initialisation, d'allocation et de libération
qui communiquent entre elles par le biais de variables
globales dans la mémoire de la partition.

On pourrait aussi vouloir passer comme argument à chaque
fonction qui en a besoin les coordonnés des pages qu'elle
peut utiliser si besoin est, et que les fonctions
retournent les coordonnées des pages non utilisées.

## La mémoire de la partition

Mais dans ces deux cas il faut toujours prouver que les
fonctions ne consomment pas de pages qui ne leurs
appartiennent pas.

La seule façon de s'assurer dès le départ (sans rentrer
dans la fonction pour montrer qu'elle est correcte)
qu'elle ne consomme pas les mauvaises pages, serait
d'avoir une partition parent qui jouerai le rôle
d'allocateur de page. Mais un tel dispositif serait
trop lourd pour une opération aussi simple.

On aurai donc besoin d'avoir un composant dont une
interface jouerai le rôle de la mémoire de la partition,
en gardant les valeurs des addresses accessibles et
également la mémoire de quelles adresses sont accessibles,
afin de faire des preuves sur son utilisation par la
partition.

## Pip et les autres partitions

En supposant que notre partition soit représentée par un
ou plusieurs composants et qu'il communique avec un
composant Pip qui aurait pour interface les appels systèmes,
on voit que Pip doit pouvoir influencer la mémoire de
la partition, en lui retirant des pages pour se les
réserver.

On pourrait vouloir représenté Pip comme un ou un ensemble
de composants modifiant une mémoire globale de l'ordinateur.
Il faudrait alors que le composant mémoire de la partition
aille chercher ou écrire les valeurs dans cette mémoire
globale. Cela signifierait que le fonctionnement et donc
l'état abstrait du composant mémoire locale dépendrait
de l'état du composant mémoire globale.

Par ailleurs si on veut représenter la partition parent
de celle étudiée autrement que par un gros composant
"Pip+parent", ce qui serait contraire au principe de FreeSpec,
il faut que Pip puisse décrire l'effet de ses appels système
en fonction du parent. En effet c'est par les appels système
que l'enfant peut communiquer avec la parent.

## Le besoin

Il serait alors nécessaire de pouvoir définir l'état abstrait
d'un composant en fonctions de son environnement, c'est-à-dire
de l'état des composants avec lesquels il interagit via leurs
interfaces (ce qui peut donc éventuellement comprendre l'état
d'autres composants encore auxquels le premier composant
n'a pas directement accés, mais que ses composants d'interfaces
peuvent eux appeler).

Si ce genre de construction n'est pas encore possible avec FreeSpec,
comme j'ai cru le comprendre en lisant le code, il
faudrait alors peut-être l'étendre.
