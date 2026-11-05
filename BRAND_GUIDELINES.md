# Vigie — guide de marque

Source de vérité : `vigie/static/tokens.css` (tokens), `brand/build/build_brand.py` (logos, icônes, illustrations, visuels sociaux). Pour régénérer : `python brand/build/build_brand.py && node brand/build/export.mjs && python brand/build/gallery.py` (fonttools, brotli, Pillow ; `sharp` via npm pour les PNG). Références visuelles : `brand/design-system.html` et `brand/gallery.html`.

## Positionnement

Vigie est une sentinelle numérique : elle observe, analyse et protège des boîtes mail, sans bruit. Personnalité : protectrice, calme, précise, discrète, accessible. Le produit rassure ; il ne dramatise pas (pas de rouge pour une simple information, pas de vocabulaire de « hackers »).

**Signature de travail** : « Votre messagerie, sous bonne garde. » Pistes alternatives à challenger : « La tranquillité, message après message. », « Vigie veille. Vous respirez. ». Aucune n'est définitive.

**Ton** : phrases courtes, verbes d'action, vouvoiement dans les textes de marque, pas de jargon ni de superlatifs, pas d'alarmisme. Un verdict s'explique (« Pourquoi ce verdict »).

## Logo

Le symbole est un **V** (le filtre, la vigie) qui retient un **point** (le message observé). Il vient de trois pistes évaluées :

| Direction | Originalité | Petite taille | Fonds clair/sombre | Pertinence | Verdict |
|---|---|---|---|---|---|
| A — œil/sentinelle abstrait | moyenne (proche de nombreux « eyes ») | faible (détails) | bonne | forte | écartée |
| B — signal protégé (arcs + filtre) | moyenne | moyenne | bonne | forte | gardée comme motif d'animation (anneau de balayage) |
| C — monogramme V | bonne | excellente | excellente | bonne | **retenue**, enrichie du point de A/B |

Géométrie (grille 64) : trait de 8, extrémités et jointures arrondies, V `M13 17 → 32 50 → 51 17`, point `cx 32 cy 21 r 6.5`. Toutes les variantes partagent cette géométrie ; seule la « version réduite » épaissit le trait (9,5) pour ≤ 24 px. Le wordmark « Vigie » est en Plus Jakarta Sans ExtraBold (800), détouré en vecteurs ; le point du premier « i » est remplacé par le point rond du symbole.

Fichiers (`brand/logos/`) : `vigie-{horizontal,vertical,symbol,symbol-small,wordmark}-{light,dark,mono-ink,mono-white}.svg`. « light » = pour fonds clairs (encre + vert profond), « dark » = pour fonds sombres (Mist + Signal). Fond transparent partout.

- **Zone de protection** : au moins la largeur du point (≈ 13/64 de la hauteur du symbole) tout autour.
- **Tailles minimales** : symbole 16 px (version réduite sous 24 px), logo horizontal 80 px de large, vertical 56 px.
- **À éviter** : déformer, recolorer hors palette, ajouter ombres/contours, poser le logo « light » sur fond sombre, changer l'angle du V, remplacer le point par une icône.

Icônes (`brand/icons/`) : favicon SVG/ICO, app icon 512, Apple touch 180, PWA 192/512 + maskable. Zone sûre maskable : symbole à 50 % du carré.

## Couleurs

| Rôle | Clair | Sombre |
|---|---|---|
| Fond | `#F3F6F4` | `#0B151A` |
| Surface | `#FFFFFF` | `#112028` |
| Texte | `#101F27` | `#EAF1EE` |
| Texte atténué | `#52666D` | `#94ABB2` |
| Primaire | `#1C333C` | `#B9F47C` |
| Accent | `#3E9B2F` | `#B9F47C` |
| Succès / Avertissement / Danger / Info | `#1E7A4C` / `#8F500F` / `#B3372B` / `#1F6C94` | `#7FDDA4` / `#EDB27A` / `#F58C80` / `#8CCDEE` |

Base de marque : Ink `#101F27`, Slate `#1C333C`, Signal `#B9F47C`, Mist `#F3F6F4`, Amber `#E7A568`, plus Signal profond `#3E9B2F` (Signal est illisible sur fond clair). Pas de violet, pas de dégradé décoratif, pas de néon. Sémantique des verdicts : spam = danger, suspect = avertissement, légitime = succès ; le rouge n'est jamais utilisé pour une information neutre. L'état n'est jamais porté par la couleur seule (texte + point/forme). Contrastes visés : WCAG AA pour le texte. Aucune couleur n'est codée en dur dans les composants : utiliser `var(--…)`.

Thèmes : automatique (préférence système), clair, sombre ; choix mémorisé (`localStorage`, clé `vigie-theme`) et appliqué par un script inline avant le rendu (pas de flash). La sidebar reste sombre dans les deux thèmes (signature de marque).

## Typographie

- **Plus Jakarta Sans** (variable 200–800, SIL OFL 1.1, auto-hébergée) : interface et titres.
- **IBM Plex Mono** 400/500/600 (SIL OFL 1.1, auto-hébergée) : scores, identifiants, dates, valeurs tabulaires.

Échelle (tokens `--fs-*`) : Display `clamp(2→3rem)` / 1,05 / −0,03 em ; Heading XL `clamp(1,5→1,9rem)` ; Heading L 1,3 rem ; Heading M 1,05 rem ; Body 0,9375 rem / 1,55 ; Small 0,84 rem ; Caption 0,76 rem ; Label 0,72 rem majuscules +0,06 em ; Numeric = mono avec chiffres tabulaires. Largeur de lecture : 68 caractères (`--measure`).

## Grille, rayons, élévation

Espacement : 4/8/12/16/24/32/48/64 px. Rayons : 6 / 10 / 16 / pilule. Élévation : bordure 1 px plutôt qu'ombre ; `--shadow-2` pour les cartes (clair), ombre portée uniquement pour les dialogues. Breakpoint principal : 860 px (sidebar ↔ barre du bas).

## Composants

Boutons (primaire, secondaire, fantôme, danger, icône, chargement `aria-busy`), champs, mot de passe, liste, cases, interrupteurs, radios, badges/tags, pastilles d'état, notices, cartes, tableaux (repli en lignes empilées sur mobile pour les règles), contrôle segmenté, pagination, états vides illustrés, squelettes, dialogue d'aperçu, graphique à barres. Chaque composant a hover, focus visible (anneau Signal), active, disabled ; la confirmation destructive passe par le bouton « armé » (`data-confirm`). Démonstration : `brand/design-system.html` (fichier statique, non servi par l'application).

## Illustrations

Style géométrique, trait de 3 px arrondi, un seul accent (Signal pour le calme, Amber pour le doute, Corail pour l'erreur), formes issues du symbole (V, point, anneaux de balayage). 9 SVG dans `brand/illustrations/` ; intégrés en ligne dans l'application (`vigie/templates/ill/`) pour hériter des tokens de thème. Ils s'adaptent au thème sombre seuls (media query) lorsqu'ils sont utilisés en `<img>`.

## Animation

Utile et brève : apparition du contenu (≈ 0,4 s), barres qui se remplissent, compteurs qui montent (600 ms), anneau de balayage unique autour du point au chargement du tableau de bord, squelettes. Pas d'animation permanente. `prefers-reduced-motion` coupe tout. Pas de dépendance JS d'animation.

## Accessibilité

Lien d'évitement, repères `nav`/`main`, `aria-current`, `aria-pressed`, `role="alert"/"status"`, focus visible, cibles ≥ 40 px sur mobile, navigation clavier (`/`, `j`, `k`, Entrée), fonctionnement à 320 px et au zoom. Le HTML des mails n'est jamais rendu actif : iframe `sandbox` + CSP, inchangés.

## Réseaux, notifications

Avatar : `brand/social/avatar.svg` / `avatar-512.png`. Partage : `og-image.png` (1200×630), `github-social-preview.png` (1280×640).

Notifications : icônes 256 px dans `brand/icons/notification-{default,success,alert,info,danger,digest}-256.png`. Les services comme Pushover/ntfy fixent l'icône par application (ou par topic) ; une icône par message n'est possible que si le service le permet. Titres : « Vigie — Protection active », « Vigie — Message suspect détecté », « Vigie — Compte déconnecté », « Vigie — Récapitulatif quotidien ». Corps : factuel, une ligne ; jamais d'expéditeur, d'objet ou d'extrait de mail par défaut.

## Logos de fournisseurs

Gmail, Outlook, iCloud, Proton Mail, OVH, IONOS, Fastmail : fichiers SVG de `logos.lndev.me` (dépôt MIT, **logos = marques de leurs propriétaires**), stockés dans `vigie/static/providers/` pour respecter la CSP (`img-src 'self'`). Jamais recolorés ; affichés en petit dans une pastille neutre ; icône générique pour un serveur inconnu. Ils ne sont pas redistribués avec les assets Vigie.

## Publication des assets

Le dépôt est privé et le reste. Les assets Vigie originaux (`brand/`) ne contiennent aucun secret ni donnée. Pour les rendre publics sans authentification : créer un dépôt public dédié (ex. `Thaskow/vigie-brand`) ou une page statique, y copier `brand/` (sans `licenses/` tiers inutiles) puis renseigner `publicUrl` dans `brand/assets-manifest.json` **après vérification des URLs**. Cette étape n'est pas faite automatiquement.
