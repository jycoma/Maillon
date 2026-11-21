# Maillon — application Android

Projet Capacitor prêt à compiler. Il contient l'application `www/index.html`, le plugin Bluetooth LE et le projet Android déjà généré, avec les permissions Bluetooth.

## Méthode recommandée : GitHub fabrique l'APK pour toi

Aucun Android Studio nécessaire : GitHub compile l'application et te donne le fichier à installer.

1. Sur github.com, crée un nouveau dépôt (par exemple `maillon`), de préférence privé, vide (sans README).
2. Décompresse ce dossier, ouvre un terminal dedans et lance :
   ```
   git init -b main
   git add .
   git commit -m "Maillon Android"
   git remote add origin https://github.com/TON_COMPTE/maillon.git
   git push -u origin main
   ```
3. Dans l'onglet Actions du dépôt, le travail « Construire l'APK Maillon » démarre tout seul. Compte une dizaine de minutes la première fois. Tu peux aussi le relancer à la main avec « Run workflow ».
4. Quand il est terminé (coche verte), récupère l'APK :
   - dans la colonne Releases du dépôt, ouvre « Maillon (dernière version) » et télécharge `maillon.apk` ;
   - ou ouvre le travail terminé et télécharge l'artefact `maillon-apk` (un zip qui contient l'APK).
5. Sur le téléphone, ouvre la page Releases dans le navigateur (connecté à GitHub si le dépôt est privé), télécharge `maillon.apk`, ouvre-le et autorise l'installation depuis cette source.
6. À chaque modification de `www/index.html` : commit et push, et un nouvel APK est construit.

Si le travail échoue (croix rouge), ouvre-le, copie le message d'erreur de l'étape en rouge et envoie-le-moi.

## Autre méthode : compiler sur l'ordinateur

### Ce qu'il faut sur l'ordinateur

- Node.js 22 ou plus récent
- Android Studio récent (Capacitor 8 le demande, à ma connaissance Android Studio Otter 2025.2.1 ou plus)
- Un téléphone Android 7 ou plus avec Bluetooth LE

### Compiler et installer

1. Décompresse le dossier, par exemple dans `C:\Maillon`.
2. Ouvre un terminal dans ce dossier et lance :
   ```
   npm install
   npm run sync
   npx cap open android
   ```
3. Android Studio s'ouvre. Attends la fin de la synchronisation Gradle (longue la première fois, il télécharge ses outils).
4. Deux façons d'installer sur le téléphone :
   - **Branché en USB** : active les options pour les développeurs et le débogage USB sur le téléphone, choisis-le dans la liste des appareils en haut d'Android Studio, puis clique sur le triangle vert (Run).
   - **Par fichier APK** : menu Build > Build Bundle(s) / APK(s) > Build APK(s). Le fichier `app-debug.apk` est créé dans `android/app/build/outputs/apk/debug/`. Copie-le sur le téléphone, ouvre-le et autorise l'installation depuis cette source.

## Premier lancement de l'application

1. Ouvre l'application Maillon.
2. Dans Réglages, appuie sur « Connecter le capteur ». Android demande la permission « Appareils à proximité » : accepte.
3. Choisis « Maillon-01 » dans la liste.
4. Suis ensuite la procédure de calibrage de l'application (onglet Calibrage).

## Après une modification de `www/index.html`

```
npm run sync
```
puis relance l'application depuis Android Studio.

## Limites

Ce projet n'a pas été compilé ni essayé sur un téléphone : l'outil Android n'était pas accessible là où je l'ai préparé. La logique de l'application a été testée avec un Bluetooth simulé. Si une erreur apparaît à la compilation ou à la connexion, copie son message exact.
