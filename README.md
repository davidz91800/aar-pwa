# AAR PWA

PWA offline basee sur `AAR.html`.

## Contenu

- `AAR.html` (application principale)
- `mission-config.js` (listes LOG/TAC modifiables par l'admin)
- `manifest.webmanifest`
- `sw.js` (service worker cache shell)
- `icons/icon-192.svg`, `icons/icon-512.svg`

## Utilisation

1. Servir ce dossier via HTTP local (ex: serveur statique) pour l'installation PWA.
2. Ouvrir `AAR.html` et installer l'application depuis le navigateur.
3. Une fois installee, l'application reste accessible hors ligne.
