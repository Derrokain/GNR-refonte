# GNR — Des opérations connectées

Refonte du site GNR en français et en anglais. Sources, contenus, médias locaux et version statique prête à servir.

Version importée depuis le Site : `7ae988af6657e79774c580cf6daf0455d42b6a5a`.

## Démarrer

Site HTML/CSS/JavaScript statique, sans framework. Three.js est fourni localement pour la mascotte de l’accueil.

```sh
git clone https://github.com/Derrokain/GNR-refonte.git
cd GNR-refonte
python3 build.py
python3 check.py
python3 -m http.server 8000 --directory dist
```

Ouvrir http://localhost:8000. Les liens commencent à la racine : servir le dossier `dist`, ne pas ouvrir les fichiers avec `file://`.

## Structure

- `content/services.json` : contenu FR/EN des six expertises, extrait des données du ZIP.
- `content/sectors.json` : contenu FR/EN des six secteurs, extrait du ZIP.
- `build.py` : gabarits, accueil, pages détaillées, à propos, contact, mentions légales et 404.
- `src/style.css` : nouvelle direction artistique et responsive.
- `src/app.js` : menu accessible, galerie horizontale, schéma, manifeste et préparation d'un courriel.
- `src/robot.js` : mascotte 3D interactive issue du fichier utilisateur, intégrée sur l’accueil FR/EN.
- `assets/vendor` : Three.js r128 et sa licence MIT, servis localement.
- `assets/video` : vidéo de fond du hero fournie par l’utilisateur, encodée en WebM et MP4 sans piste audio. Chargée au premier survol, elle apparaît dans un large halo circulaire aux bords diffus qui suit la souris. Apparition sur 1,6 s, disparition sur 2,2 s ; la lecture s’arrête après le fondu ou immédiatement hors écran. Les appareils sans survol et la préférence de réduction des animations gardent le fond statique.
- `docs/robot-integration.md` : interactions, accessibilité et limites de vérification de la mascotte.
- `assets/fonts` : police variable locale conservée comme ressource technique, utilisée avec une nouvelle hiérarchie typographique.
- `dist` : 38 pages générées et ressources prêtes à héberger.
- `check.py` : validation des liens, ancres, ressources, H1 et langues.
- `docs/REFONTE.md` : référence, transposition, provenance et limites.

`npm run build` et `npm run check` sont aussi disponibles ; aucune installation npm n'est nécessaire.

## Publication

La publication utilise le dossier `dist`, à la racine du domaine. Le fichier de liaison à l’hébergement ChatGPT Sites n’est pas inclus dans cet export. Le domaine existant gnr-dev.com n’est pas modifié.

La configuration actuelle interdit l'indexation via `robots.txt`. Avant une publication sur le domaine officiel, mettre à jour l'origine des liens hreflang dans `build.py`, autoriser l'indexation si souhaitée et générer le sitemap. Le contenu juridique doit être complété.

## Contact

Le formulaire produit un lien `mailto:` et propose de copier le brouillon. Il n'envoie aucune donnée et n'affiche jamais une confirmation d'envoi. Pour recevoir les demandes directement depuis le site, connecter un service d'envoi ou une fonction serveur, puis adapter la politique de confidentialité. Les coordonnées du ZIP sont conservées.

## Contrôles effectués

- Génération réussie des 38 pages FR/EN.
- 1 494 liens, ancres et ressources internes vérifiés.
- Syntaxe JavaScript validée avec `node --check`.
- Rendu bureau et vues à 390 et 768 px contrôlés dans le navigateur (iframes aux dimensions fixées, pas émulation d'un vrai téléphone).
- Menu mobile et bureau, navigation FR/EN, schéma, progression des expertises et préparation du courriel testés.
- Les préférences de réduction des animations sont prises en charge dans le code ; aucun score Lighthouse n'est revendiqué.

## Mascotte et vérifications locales

La mascotte 3D nécessite un navigateur compatible WebGL. Une illustration de secours est affichée si WebGL est indisponible. Les limites de vérification du rendu sont documentées dans `docs/robot-integration.md`.

```sh
node --check src/app.js
node --check src/robot.js
node tests/robot-lifecycle.cjs
```

Le test de cycle de vie utilise le vrai modèle Three.js et un moteur de rendu simulé ; il ne valide pas le rendu GPU.
