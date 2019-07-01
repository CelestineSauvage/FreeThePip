# Syscalls

## Interface

Une interface est un ensemble d'opérations définies par
leur signature / type.

Ces opérations sont exécutées pas un composant extérieur.

-> Il doit être possible d'exprimer les appels système de Pip comme une interface.

## Program

Un programme est une fonction monadique qui utilise une interface.

## Component

Un composant:
- propose une interface
- a un état
- utilise une interface

## Semantic

Une sémantique modélise un système qui présente une interface.

Pour modéliser un composant qui n'utilise pas d'interface (il y a bien
un composant de départ...) on peut utiliser une interface vide.

Pip sera un composant. Il faudra réussir à exprimer l'API de Pip dans
une interface et l'état de la mémoire dans l'état du composant.

=> /!\ Comment mettre en relation interface et état ?
	   En effet, le comportement d'un appel système dépend directement
	   de l'état du système.

## Specification

Une spécification exprime
- le changement opéré
- les pré-conditions
- les post-conditions

## Questions

- Chaque composant a un état. Lorsque l'on réfléchit sur Pip et/ou
  une architecture utilisant Pip, on rélféchit sur un état global
  (l'état de la mémoire). Comment mettre en relation les états
  des différents composants avec l'état global du système?
