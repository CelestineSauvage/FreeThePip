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

## Specification

Une spécification exprime
- le changement opéré
- les pré-conditions
- les post-conditions
