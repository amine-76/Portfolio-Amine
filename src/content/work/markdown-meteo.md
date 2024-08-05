---
title: Application Météo
publishDate: 2020-03-02 00:00:00
img: /assets/meteo.jpeg
img_alt: Application Météo
description: |
  Application web interactive pour consulter les conditions météorologiques d'une ville en France.
tags:
  - JavaScript
  - API
  - Météo
---

## Application Météo

**Description du Projet :**  
Cette application web permet aux utilisateurs de consulter les conditions météorologiques actuelles d'une ville en France. En utilisant l'API Visual Crossing Weather, les utilisateurs peuvent entrer le nom d'une ville pour obtenir des informations détaillées telles que la température, les conditions météorologiques et l'humidité.

### Fonctionnalités :
- **Saisie de Ville :** Les utilisateurs peuvent entrer le nom d'une ville dans un champ de saisie.
- **Recherche par Touche Entrée :** La recherche des données météorologiques se déclenche lorsque l'utilisateur appuie sur la touche "Entrée".
- **Affichage Dynamique :** Les conditions météorologiques sont affichées en temps réel, avec des informations claires et précises.
- **Gestion des Erreurs :** Des messages d'erreur s'affichent si la ville saisie est invalide ou si une erreur se produit lors de la requête API.

### Technologies Utilisées :
- **HTML/CSS** pour la structure et le style de l'application.
- **JavaScript** pour la logique de recherche et l'interaction avec l'utilisateur.
- **API Visual Crossing Weather** pour l'accès aux données météorologiques en temps réel.

### Exemple de Code :
Un extrait du code JavaScript illustrant la recherche de la météo :

```javascript
function rechercherMeteo(ville) {
    if (ville.trim() === "") {
        resultatMeteoDiv.innerHTML = "Veuillez entrer une ville valide.";
        return;
    }

    fetch(`https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/${ville}?unitGroup=metric&key=MDQWKGGSA7KSP4WLAJD5R8AG4&contentType=json`)
        .then(response => {
            if (response.ok) {
                return response.json();
            } else {
                throw new Error('La requête a échoué');
            }
        })
        .then(data => {
            resultatMeteoDiv.innerHTML = `
                <h3>Météo pour ${ville}</h3>
                <p>Température actuelle: ${data.currentConditions.temp}°C</p>
                <p>Conditions: ${data.currentConditions.conditions}</p>
                <p>Humidité: ${data.currentConditions.humidity}%</p>
            `;
        })
        .catch(err => {
            console.error(err);
            resultatMeteoDiv.innerHTML = "Une erreur s'est produite lors de la recherche de la météo.";
        });
}
