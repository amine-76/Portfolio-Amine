---
title: Jeu Vidéo 2D avec Pygame, Pyscroll et Pytmx
publishDate: 2024-08-04 00:00:00
img: /assets/photo-pygamon.png
img_alt: Capture d'écran du jeu avec une carte en défilement
description: |
  Ce projet de jeu vidéo 2D est développé avec Python, utilisant les bibliothèques Pygame, Pyscroll, et Pytmx pour créer un environnement interactif immersif. Le jeu met en œuvre une carte en défilement, un système de contrôle du joueur, et une gestion fluide des animations.
tags:
  - Pygame
  - Pyscroll
  - Pytmx
  - Python
  - Jeu vidéo
---

## Présentation du Projet

Ce projet est un jeu vidéo 2D dynamique développé en Python, démontrant l'intégration de plusieurs bibliothèques puissantes pour créer une expérience de jeu immersive. Utilisant **Pygame** pour la gestion graphique et des événements, **Pyscroll** pour le rendu des cartes en défilement, et **Pytmx** pour le chargement et la gestion des cartes TMX, ce jeu offre une interface fluide et réactive.

### Fonctionnalités Clés

- **Rendu de Carte en Défilement** : Intégration de **Pyscroll** pour un rendu fluide des cartes en défilement orthographique. La carte est chargée à partir d'un fichier TMX, permettant des environnements de jeu étendus et interactifs.
- **Contrôles du Joueur** : Le joueur peut se déplacer dans l'environnement en utilisant les touches directionnelles du clavier. Les animations du personnage changent en fonction de la direction du mouvement, offrant une expérience de jeu réactive.
- **Interface et Graphisme** : La fenêtre du jeu est configurée avec **Pygame** pour afficher une interface graphique attrayante et gérer les interactions utilisateur. Le jeu est optimisé pour une expérience visuelle fluide avec un taux de rafraîchissement de 60 FPS.
- **Gestion des Événements** : Le jeu traite les événements de manière efficace pour répondre aux actions du joueur, garantissant une réactivité rapide aux commandes de déplacement et aux événements de fermeture de la fenêtre.

### Détails Techniques

- **Chargement de la Carte** : Le jeu utilise **Pytmx** pour charger des cartes TMX, transformant les données de carte en un format utilisable par **Pyscroll** pour le rendu dynamique.
- **Mise à Jour et Rendu** : La boucle principale du jeu gère les mises à jour des états du jeu et le rendu à l'écran, tout en maintenant une performance élevée grâce à la gestion du taux de rafraîchissement.
- **Contrôles Dynamiques** : Le système de contrôle permet de gérer les mouvements du joueur et les animations associées en temps réel, offrant une expérience de jeu engageante et interactive.

### Exemple de Code

Voici un extrait du code principal du jeu, montrant la gestion du rendu et des contrôles :

```python
import pygame
import pyscroll
import pytmx
from Player import Player

pygame.init()

class Game:
    def __init__(self):
        self.screen = pygame.display.set_mode((800, 800))
        pygame.display.set_caption("Mon Jeu")
        tmx_data = pytmx.util_pygame.load_pygame('carte.tmx')
        map_data = pyscroll.data.TiledMapData(tmx_data)
        map_layer = pyscroll.orthographic.BufferedRenderer(map_data, self.screen.get_size())
        map_layer.zoom = 1
        player_position = tmx_data.get_object_by_name('player')
        self.player = Player(player_position.x, player_position.y)
        self.group = pyscroll.PyscrollGroup(map_layer=map_layer, default_layer=3)
        self.group.add(self.player)

    def handle_input(self):
        pressed = pygame.key.get_pressed()
        if pressed[pygame.K_UP]:
            self.player.move_up()
            self.player.change_animation('up')
        elif pressed[pygame.K_DOWN]:
            self.player.move_down()
            self.player.change_animation('down')
        elif pressed[pygame.K_LEFT]:
            self.player.move_left()
            self.player.change_animation('left')
        elif pressed[pygame.K_RIGHT]:
            self.player.move_right()
            self.player.change_animation('right')

    def run(self):
        clock = pygame.time.Clock()
        running = True
        while running:
            self.handle_input()
            self.group.update()
            self.group.center(self.player.rect)
            self.group.draw(self.screen)
            pygame.display.flip()
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    running = False
            clock.tick(60)
        pygame.quit()
