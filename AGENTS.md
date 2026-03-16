# AGENTS.md - C - AAR PWA

## Role
Ce dossier (`C - AAR PWA`) est la source de verite du formulaire AAR (`AAR.html`).

## Couplage obligatoire
- Toute evolution de schema/champs/sections dans `AAR.html` doit etre repercutee dans:
  - `E - AAR READER HUB/app.js` (normalisation, recherche, affichage)
  - `E - AAR READER HUB/AAR READER HUB QWI/app.js` (meme normalisation)
- La copie de deploiement web du formulaire doit etre mise a jour aussi:
  - `E - AAR READER HUB/AAR READER HUB QWI/aar-pwa/AAR.html`
  - `E - AAR READER HUB/AAR READER HUB QWI/aar-pwa/mission-config.js`
  - `E - AAR READER HUB/AAR READER HUB QWI/aar-pwa/manifest.webmanifest`
  - `E - AAR READER HUB/AAR READER HUB QWI/aar-pwa/sw.js`
- Le mode edition externe du formulaire (parametres URL `externalEditor=1&session=...`) doit rester compatible avec:
  - `E - AAR READER HUB/AAR READER HUB QWI/qwi-mode.js`

## Regle de livraison
Quand une modification touche le formulaire AAR, livrer dans le meme changement:
1. MAJ formulaire (`C - AAR PWA`)
2. MAJ hub lecteur (`E - AAR READER HUB`)
3. MAJ hub QWI editable (`E - AAR READER HUB/AAR READER HUB QWI`)
4. MAJ copie formulaire deploiement `AAR READER HUB QWI/aar-pwa/`
5. Verification manuelle du flux d'edition QWI (ouvrir, modifier, enregistrer retour).

## Contexte d'exploitation (a conserver)
- Flux operationnel actuel:
  - Un e-mail AAR arrive sur `david.zemmour3@gmail.com`.
  - Une automatisation extrait le JSON de l'e-mail et l'ecrit dans le dossier Google Drive des JSON.
  - Un push GitHub met a jour les donnees consommees par les hubs.
- Toute evolution du schema AAR doit rester compatible avec ce pipeline e-mail -> Drive -> GitHub -> hubs.
- Politique credentials:
  - Projet Google Cloud recommande: `RETEX` (unique projet).
  - Cle API frontend (hub) separee de la cle API automatisation.
  - Edition QWI: necessite un OAuth Client ID Web (pas seulement une cle API).
