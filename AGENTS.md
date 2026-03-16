# AGENTS.md - C - AAR PWA

## Role
Ce dossier (`C - AAR PWA`) est la source de verite du formulaire AAR (`AAR.html`).

## Couplage obligatoire
- Toute evolution de schema/champs/sections dans `AAR.html` doit etre repercutee dans:
  - `E - AAR READER HUB/app.js` (normalisation, recherche, affichage)
  - `E - AAR READER HUB/AAR READER HUB QWI/app.js` (meme normalisation)
- Le mode edition externe du formulaire (parametres URL `externalEditor=1&session=...`) doit rester compatible avec:
  - `E - AAR READER HUB/AAR READER HUB QWI/qwi-mode.js`

## Regle de livraison
Quand une modification touche le formulaire AAR, livrer dans le meme changement:
1. MAJ formulaire (`C - AAR PWA`)
2. MAJ hub lecteur (`E - AAR READER HUB`)
3. MAJ hub QWI editable (`E - AAR READER HUB/AAR READER HUB QWI`)
4. Verification manuelle du flux d'edition QWI (ouvrir, modifier, enregistrer retour).
