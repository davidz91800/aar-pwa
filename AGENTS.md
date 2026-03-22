# AGENTS.md - C - AAR PWA

## Role
Ce dossier (`C - AAR PWA`) est la source de verite du formulaire AAR (`AAR.html`).

## Validation avant propagation
- NP est la reference de travail.
- Une modification faite sur NP n'est propagee aux applications couplees qu'apres validation explicite utilisateur.
- Ne jamais propager en avance "par defaut".

## Schema AAR actif (maj 2026-03-22)
- `Type d'AAR`: l'option UI `AAR FLASH` est renommee en `AAR BAAP` (valeur technique conservee: `FLASH`).
- `0. Configuration`: les blocs `Type LOG/TAC` et `Cadre TAC` restent dans le JSON legacy mais sont masques dans l'UI.
- `0. Configuration`: `mission-config.js` expose le catalogue hashtags general (`hashtags`) + un referentiel dedie boutons FAITS (`factsHashtags`, `factsHashtagsConfigured`, `factsHashtagTooltipMap`) + `tooltipComments`.
- `1. Faits`: nouveaux modules BAAP optionnels:
  - `facts.baapSelected`,
  - `facts.baapAirfield`,
  - `facts.baapPilot`,
  - `facts.baapLoadmaster`,
  - `facts.baapMissionSupport`,
  - `facts.baapIntel`,
  - `facts.baapC2`.
- `1. Faits` (UI): les boutons `#...` sont dynamiques (catalogue `factsHashtags`) pour tous les types d'AAR et synchronises bidirectionnellement avec `meta.hashtags` (0. Configuration).
- `1. Faits` (UI): l'ordre des boutons `#...` suit strictement l'ordre de `factsHashtags` (pas de tri alphabetique).
- `1. Faits` (UI): suppression des encarts specifiques par bouton; un unique encart d'edition est conserve (`What? Why? When? Where? Who? How?`).
- `Infobulles`: les textes des aides utilisent `tooltipComments` (catalogue dynamique fusionne avec les valeurs par defaut) et les boutons `#` de `1. FAITS` resolvent leur infobulle via `factsHashtagTooltipMap`.
- `Infobulles` (boutons `#`): les hashtags personnalises peuvent porter des cles dediees `FACTS_HASHTAG_*` pour avoir un commentaire propre par bouton, tout en conservant les cles socle `BAAP_ROLE_*`.

## Couplage obligatoire
- Toute evolution de schema/champs/sections dans `AAR.html` doit etre repercutee dans:
  - `D - AAR READER HUB/app.js` (normalisation, recherche, affichage),
  - `E - AAR READER HUB QWI/app.js` (meme normalisation).
- La copie de deploiement web du formulaire doit etre mise a jour aussi:
  - `E - AAR READER HUB QWI/aar-pwa/AAR.html`,
  - `E - AAR READER HUB QWI/aar-pwa/mission-config.js`,
  - `E - AAR READER HUB QWI/aar-pwa/manifest.webmanifest`,
  - `E - AAR READER HUB QWI/aar-pwa/sw.js`.
- Le mode edition externe du formulaire (URL `externalEditor=1&session=...`) doit rester compatible avec:
  - `E - AAR READER HUB QWI/qwi-mode.js`.

## Regle de livraison
Quand une modification touche le formulaire AAR, livrer dans le meme changement:
1. MAJ formulaire NP (`C - AAR PWA`).
2. Validation explicite utilisateur.
3. MAJ hub lecteur (`D - AAR READER HUB`).
4. MAJ hub QWI editable (`E - AAR READER HUB QWI`).
5. MAJ copie formulaire deploiement (`E - AAR READER HUB QWI/aar-pwa/`).
6. MAJ equivalent DR.
7. Verification manuelle du flux d'edition QWI (ouvrir, modifier, enregistrer retour).
8. MAJ des `AGENTS.md` impactes (racine + dossiers couples + sous-dossiers techniques concernes).

## Regles d'encodage (obligatoires)
- Encodage unique: `UTF-8` pour tous les fichiers texte.
- En PowerShell, toujours preciser l'encodage en ecriture (`-Encoding UTF8`).
- Controle anti-mojibake avant push sur les fichiers modifies:
  - rechercher `Ãƒ|Ã‚|Ã¢â‚¬Â¦|Ã¢â‚¬â€|Ã°Å¸`,
  - corriger toute chaine UI corrompue.

## Contexte d'exploitation
- Flux operationnel:
  - Un e-mail AAR arrive sur `david.zemmour3@gmail.com`.
  - Apps Script extrait le JSON et l'ecrit dans le dossier Drive metier.
  - Les hubs lisent via `action=listAars` (sans push GitHub des donnees en nominal).
- Le schema AAR doit rester compatible avec ce pipeline e-mail -> Apps Script -> Drive -> hubs.
- `AAR_ACCESS_KEY` doit rester coherent entre `mission-config.js` et les `config.js` des hubs.
