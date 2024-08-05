---
title: Jeu d'Aventure 2D avec Pygame
publishDate: 2024-08-04 00:00:00
img: /assets/photo-monstre.png
img_alt: Capture d'écran du jeu montrant un joueur, des monstres et des projectiles
description: |
  Ce projet est un jeu vidéo 2D développé en Python avec Pygame. Le jeu propose un environnement dynamique où le joueur peut se déplacer, lancer des projectiles, et affronter des monstres. Le gameplay intègre des éléments tels que la gestion de la santé du joueur et des ennemis, ainsi que des mécanismes de collision et de détection de projetiles.
tags:
  - Pygame
  - Python
  - Jeu vidéo
  - Développement de jeux
---

## Présentation du Projet

Ce jeu d'aventure 2D est conçu pour offrir une expérience interactive en utilisant **Pygame**. Les principales mécaniques de jeu incluent le déplacement du joueur, le lancement de projectiles, et la gestion des collisions avec des monstres. Le jeu est structuré en plusieurs classes pour gérer les différents aspects du gameplay et des éléments visuels.

### Fonctionnalités Clés

- **Déplacement du Joueur** : Le joueur peut se déplacer à gauche et à droite, et la barre de vie du joueur est affichée à l'écran pour indiquer l'état de santé actuel.
- **Lancement de Projectiles** : Le joueur peut lancer des projectiles pour attaquer les monstres. Les projectiles sont animés et tournent lorsqu'ils se déplacent.
- **Gestion des Monstres** : Les monstres apparaissent à des positions aléatoires et se déplacent automatiquement vers le joueur. Ils ont une barre de vie qui est mise à jour en fonction des dégâts reçus.
- **Détection de Collisions** : Le jeu utilise des mécanismes de collision pour gérer les interactions entre le joueur, les monstres, et les projectiles. Les collisions déclenchent des réactions appropriées, telles que l'infligement de dégâts et la réinitialisation des monstres.

### Détails Techniques

- **Classes Principales** :
    - **Player** : Gère les actions du joueur, y compris le déplacement et le lancement de projectiles. Affiche également la barre de vie du joueur.
    - **Monster** : Gère les comportements des monstres, y compris leur déplacement et leur barre de vie.
    - **Projectile** : Représente les projectiles lancés par le joueur, avec des fonctionnalités de mouvement et de rotation.

- **Chargement des Ressources** : Le jeu utilise des images pour représenter le joueur, les monstres, et les projectiles. Les images sont chargées et affichées à l'écran pour créer une interface visuelle attrayante.

- **Gestion des Événements** : Le jeu réagit aux événements du clavier pour permettre le déplacement du joueur et le lancement de projectiles. La boucle principale du jeu assure la mise à jour continue des éléments à l'écran.

### Extrait de Code

Voici un extrait du code principal, montrant comment le jeu est structuré :

```python
import pygame
from player import Player
from monster import Monster

pygame.init()

class Game:

    def __init__(self):
        self.is_playing = False
        self.all_players = pygame.sprite.Group()
        self.player = Player(self)
        self.all_players.add(self.player)
        self.all_monster = pygame.sprite.Group()
        self.pressed = {}
        self.spawn_monster()
        self.spawn_monster()

    def spawn_monster(self):
        monster = Monster(self)
        self.all_monster.add(monster)

    def check_collision(self, sprite, group):
        return pygame.sprite.spritecollide(sprite, group, False, pygame.sprite.collide_mask)
