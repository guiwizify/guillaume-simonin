# Handoff : Landing page Guillaume Simonin (auteur & conférencier)

## Overview
Landing page one-page pour **Guillaume Simonin**, auteur et conférencier en éducation
financière. Objectif : présenter son positionnement, prouver sa crédibilité (marques,
médias, livre best-seller), montrer ses conférences réalisées et convertir via un
formulaire « Organiser une conférence ». La page est en français.

Sections, dans l'ordre :
1. **Hero** — barre transparente (nom + lien LinkedIn), titre, sous-titre, CTA, photo avec badges.
2. **Preuve** — bandeau « Marques et institutions… » + marquee de logos qui défile.
3. **Vidéo TEDx** — bande large 16:9, lecture YouTube autoplay muet + bouton « Activer le son ».
4. **Feuilles volantes** — texte + éventail de 4 fiches illustrées.
5. **Livre** — couverture + descriptif + CTA Amazon + note 4,7★.
6. **Médias & audience** — texte + « orbite » animée des réseaux (LinkedIn, YouTube, Newsletter, Instagram, X) autour d'un total « 150k+ ».
7. **Conférences** — 2 colonnes : coverflow photo (auto) + études de cas (onglets par marque).
8. **Booking** — formulaire « Organiser une conférence ».
9. **Footer** — nom + réseaux + 3 cartes entreprises (Wizify, WizExpert, WizPatrimoine).

## About the Design Files
Les fichiers de ce bundle sont des **références de design réalisées en HTML/CSS/JS
vanilla** — des prototypes montrant l'apparence et le comportement voulus, **pas du code
de production à copier tel quel**. La tâche est de **recréer ces designs dans
l'environnement cible** (Next.js/React, Astro, Vue, etc.) en suivant ses conventions.
S'il n'existe pas encore de codebase, **Next.js + Tailwind** est un bon choix par défaut
pour ce type de landing statique (déploiement Vercel/Netlify).

Le HTML est autonome (un seul fichier + 2 CSS + assets). Aucune dépendance JS externe
sauf les Google Fonts et les embeds YouTube. Tout le JS (coverflow, onglets, orbite,
bouton son) est en vanilla dans un `<script>` en bas du fichier — simple à porter en
composants.

## Fidelity
**High-fidelity (hifi).** Couleurs, typographie, espacements et interactions sont finaux.
À recréer fidèlement. Deux fichiers :
- `Guillaume Simonin - Landing V2.html` — **version desktop** (référence maître, design à 1440px).
- `Guillaume Simonin - Landing Mobile.html` — **même page + media queries** (`max-width:820px` et `max-width:420px`). C'est la version responsive à shipper ; le desktop V2 est identique hors media queries.

> Recommandation : partir du fichier **Mobile** (il contient desktop + responsive) comme source unique.

## Design Tokens
Définis dans `tokens.css` (variables `--of-*`). Valeurs clés utilisées :

**Couleurs**
- Bleu primaire `--of-blue` : `#3340FA` (hover `--of-blue-hover`)
- Fond sombre de page : `hsl(234 68% 40%)` — grille + halo aurora (voir `.gs-page-bg`)
- Accent (vert) : `#26DEB5` (rgb `38,222,181`) — variable `--accent`, utilisée pour eyebrows, « simple et accessible », titres audiences, « 150k+ ».
- Encre claire `--of-ink` `#141628`, `--of-ink-2`, `--of-mute`
- Bleus clairs : `--of-blue-50`, `--of-blue-100`, `--of-blue-200`
- Blanc `#fff`, jaune étoiles `#FFB400`, rouge TEDx `#EB0028`, orange Amazon `#FF9900`

**Typographie**
- Titres/corps : famille du design system (voir `tokens.css`, `--of-font-*` / Poppins).
- Manuscrite : **Caveat** (Google Fonts) — utilisée pour le lien LinkedIn du hero (`.gs-li-btn__lbl`).
- Hero H1 desktop : 60px, 700, letter-spacing -2.5px ; mobile 33px.
- H1 sections (`.h-1`) : ~44px desktop / 30px mobile ; descriptions `.body--lg` ~17px / 14px mobile.

**Radius / ombres**
- Cartes : radius 12–16px. Boutons/inputs : ombre « liquid glass »
  `0 2px 6px rgba(0,0,0,.16), 0 14px 34px rgba(10,14,45,.42), inset 0 1px 0 rgba(255,255,255,.9)`.
- Badges hero & orbite : glass sombre `linear-gradient(rgba(18,22,60,.55),rgba(18,22,60,.55)),rgba(255,255,255,.1)` + `backdrop-filter:blur(14px) saturate(150%)` + bordure `rgba(255,255,255,.3)`.

**État figé du thème** (sur `<div class="of-site ...">`) : `page-dark glass has-accent hp-1 cf-2`
avec `--bg-hue:234; --bg-sat:68%; --grid-l:40%; --accent:#26DEB5`. Ce sont d'anciens
tweaks « gelés » dans le markup — le rendu final est **fond sombre bleu + accent vert**.

## Interactions & Behavior
- **Marquee logos** : défilement CSS infini (piste dupliquée).
- **Vidéo TEDx** : iframe YouTube `autoplay=1&mute=1&loop=1` ; bouton « Activer le son » recharge l'iframe avec `mute=0`. (L'autoplay sonore est bloqué par les navigateurs — d'où le bouton.)
- **Orbite médias** : conteneur `.gs-orbit__spin` en rotation CSS 44s ; chaque badge contre-tourne (`gsOrbitCounter`) pour rester droit. `prefers-reduced-motion` coupe l'animation.
- **Coverflow conférences** : JS vanilla, auto toutes les 4,8s, pause au survol, flèches + points. Les cartes n'apparaissent que du côté droit→centre (offsets dans `pos()`).
- **Onglets conférences (études de cas)** : boutons `[data-case]` affichent le `.gs-casepanel__pane` correspondant.
- **Boutons** : soulèvement + ombre glass au survol.
- **Formulaire** : `onsubmit` local (prévient l'envoi, change le libellé du bouton en « Demande envoyée ✓ »). À brancher sur un vrai back (email/CRM).

## Responsive (mobile, fichier Mobile)
- `< 820px` : hero 1 colonne centré (photo au-dessus, lien LinkedIn masqué, badges masqués), toutes les grilles passent en 1 colonne, textes de section centrés, `.body--lg` à 14px, éventail + orbite réduits, livre & orbite placés **sous** leur texte, footer 1 colonne, nav coverflow allégée.
- `< 420px` : titre hero 32px, éventail encore réduit.

## Assets (dans ce bundle)
- `illustrations/guillaume-hero.png` — photo hero (masque dégradé bas via CSS `.gs-hero__photo`).
- `illustrations/livre-guide-visuel.png` — couverture du livre.
- `illustrations/feuilles/feuille-1..4.jpg` — fiches « feuilles volantes ».
- `uploads/TedX.jpg, loreal-conf.png, credit-agricole-conf.png, paris-investor-week.jpg, aktionnaire-day.jpg` — photos du coverflow conférences.
- `uploads/logo-credit-agricole.png, logo-loreal.png, logo-tedx.png, logo-matmut.png` — logos études de cas.

**⚠️ Assets externes hotlinkés (à re-héberger avant prod)** :
- Les logos du **marquee** « Marques et institutions » sont chargés depuis `framerusercontent.com` (URLs en dur dans le HTML). À télécharger et servir en local.
- La photo/vidéo TEDx pointe vers YouTube (`P9fN5Ph-C7o`) et la vidéo Crédit Agricole (`fCTs3frzluI`).

## Liens / données à finaliser
- Réseaux : LinkedIn OK (`linkedin.com/in/guillaume-simonin/`) ; **YouTube, Instagram, X, Newsletter en `href="#"`** — à renseigner.
- Entreprises (footer, liens externes réels) : Wizify `https://wizify.fr/`, WizExpert `https://www.wiz-expert.com/`, WizPatrimoine `https://lp.wizify.fr/wiz-patrimoine`.
- Contact partenariats : `hello@wizify.fr`.
- Livre : lien Amazon en place.

## Files
- `Guillaume Simonin - Landing V2.html` — desktop (référence).
- `Guillaume Simonin - Landing Mobile.html` — desktop + responsive (**source à porter**).
- `tokens.css` — variables & primitives du design system.
- `ds2.css` — composants complémentaires (avatars, etc. ; tout n'est pas utilisé par la landing).
- `illustrations/`, `uploads/` — assets référencés.
