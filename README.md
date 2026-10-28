# 🏴‍☠️ La chasse au trésor d'Alicia

Petite web app statique pour une chasse au trésor d'anniversaire : un pirate révèle
un indice en vidéo à chaque étape, et il faut saisir le bon code pour passer à la suivante.

**En ligne :** https://gregfontaine.github.io/treasure-hunt/

## Déroulé

| Étape | Vidéo | Après la vidéo |
|------:|-------|----------------|
| 1 | `videos/etape1.mp4` | bouton **Démarrer !** |
| 2 à 6 | `videos/etape2.mp4` … `etape6.mp4` | champ de saisie du code |
| 7 | `videos/etape7.mp4` | fin, confettis 🎉 |

- Mauvais code → animation de squelette 💀
- Bon code → vidéo suivante en lecture automatique
- La progression est mémorisée dans le navigateur (`localStorage`) : un rechargement ne fait pas repartir de zéro.
  Pour repartir du début : lien « Recommencer » en bas de page, ou ouvrir `index.html?reset`.

## Modifier les codes

Les codes ne sont pas en clair dans `index.html` : on y stocke le SHA-256 de `alicia-<code>`.
Pour en générer un nouveau :

```bash
node -e "console.log(require('crypto').createHash('sha256').update('alicia-1234').digest('hex'))"
```

puis remplacer le `hash` de l'étape concernée dans le tableau `STEPS` de `index.html`.

## Tester en local

```bash
npx serve .
```

(la validation des codes utilise `crypto.subtle`, qui exige `https://` ou `localhost`, pas `file://`).
