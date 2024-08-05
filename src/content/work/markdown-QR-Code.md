---
title: Générateur de QR Code
publishDate: 2020-03-02 00:00:00
img: /assets/qr.jpeg
img_alt: QR Code Generator
description: |
  Projet de génération de QR codes à partir d'un texte ou d'une URL.
tags:
  - JavaScript
  - API
  - QR Code
---

## Générateur de QR Code

**Description du Projet :**  
J'ai développé une application web simple permettant aux utilisateurs de générer des QR codes à partir d'un texte ou d'une URL. L'application utilise l'API de QR Code Generator pour créer des codes QR dynamiques, offrant une interface conviviale et intuitive.

### Fonctionnalités :
- **Saisie de Texte :** Les utilisateurs peuvent entrer un mot-clé ou une URL dans un champ de saisie.
- **Génération Dynamique :** Un QR code est généré en temps réel dès que l'utilisateur clique sur le bouton "Generate code".
- **Affichage du QR Code :** Le QR code est affiché sous le champ de saisie, permettant aux utilisateurs de le scanner facilement.

### Technologies Utilisées :
- **HTML/CSS** pour la structure et le style de l'application.
- **JavaScript** pour la logique de génération du QR code et l'interaction utilisateur.
- **API QR Code** pour la création des QR codes.

### Exemple de Code :
Un extrait du code JavaScript illustrant la génération du QR code :

```javascript
document.addEventListener("DOMContentLoaded", function() {
    let qrImage = document.getElementById("qrImage");
    let qrText = document.getElementById("qrText");

    function generateQrCode() {
        qrImage.src = "https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=" + qrText.value;
    }

    let generateButton = document.querySelector("button");
    generateButton.addEventListener("click", generateQrCode);
});
