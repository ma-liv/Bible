# Verset du Jour — compagnon spirituel quotidien

Même architecture que tes autres apps (PWA front seul + Supabase), mais ambiance propre :
lavande et crème, typographie sereine, pas de rose.

## Ce que ça fait
- **Accueil** : le verset du jour en grand sur fond lavande (change automatiquement chaque jour,
  flèches ‹ › pour parcourir), bouton 🔖 Garder, Partager, et la carte « Ton parcours du jour » :
  série de jours consécutifs (🔥), cercles L→D de la semaine, barre de progression du jour
  (lire un verset + faire le quiz).
- **Lire** : la Bible entière (Louis Segond 1910, domaine public) — choisis le livre et le
  chapitre, navigation Précédent/Suivant. Les chapitres sont chargés depuis l'API publique
  getBible (api.getbible.net) ; nécessite une connexion internet.
- **Quiz** : 10 questions tirées au hasard d'une banque de questions bibliques en français,
  correction immédiate (vert/rouge), score enregistré.
- **Mes versets** : tes versets gardés, avec date, retrouvables à tout moment.

## 1. Backend (Supabase)
Tu peux réutiliser ton projet Supabase existant (recommandé — les tables ont des noms
différents, aucun conflit) :
1. SQL Editor → colle `supabase-setup.sql` → Run (3 tables : saved_verses, daily_checkins, quiz_results)
2. Settings → API → Project URL + clé anon public (les mêmes que tes autres apps si même projet)

## 2. Connecter le front
Dans `index.html`, tout en haut du script :
```
const SUPABASE_URL = "COLLE_TON_PROJECT_URL_ICI";
const SUPABASE_ANON_KEY = "COLLE_TA_CLE_ANON_ICI";
```

## 3. Héberger et installer
Comme d'habitude : GitHub Pages ou Netlify Drop avec les 5 fichiers
(`index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`),
puis Safari → Partager → « Sur l'écran d'accueil ».

## Notes honnêtes
- Les 30 versets de l'accueil et les questions du quiz sont intégrés dans l'app
  (traduction Louis Segond 1910, domaine public — libre d'utilisation).
- L'onglet Lire dépend d'une API externe gratuite (getBible). Si elle est indisponible,
  l'app affiche un message d'erreur propre, le reste continue de fonctionner.
- Le « widget verset sur l'écran verrouillé » des captures n'est pas possible pour une
  PWA : c'est réservé aux apps natives iOS. Le plus proche : l'icône sur l'écran d'accueil
  + l'app qui s'ouvre directement sur le verset.
- Les « notifications spirituelles » programmées demandent des notifications push web,
  faisables mais plus lourdes (serveur + autorisations iOS 16.4+). À ajouter plus tard si tu veux.

## Idées d'évolution
- Plans de lecture (ex : lire Jean en 21 jours)
- Prières guidées par moment de la journée
- Notifications push à heure choisie
