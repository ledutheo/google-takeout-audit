# google-takeout-audit

Audit graphique d'un export **Google Takeout** — 100 % local, sans dépendances externes.

Génère un dashboard HTML à partir de ton Takeout décompressé : géolocalisation, carte mondiale, volume par catégorie, et analyse des recherches sensibles (santé, vocal, nocturne, etc.).

## Prérequis

- Python 3.10+
- Un export [Google Takeout](https://takeout.google.com/) décompressé (dossier `Takeout/`)

## Installation

```bash
git clone git@github.com:ledutheo/google-takeout-audit.git
cd google-takeout-audit
chmod +x takeout-audit.sh
```

## Usage

```bash
./takeout-audit.sh ~/Downloads/Takeout
```

Le script génère `audit-dashboard.html` dans le dossier Takeout, lance un serveur local et ouvre le navigateur sur `http://127.0.0.1:8765/audit-dashboard.html`.

**Important** : n'ouvre pas le HTML en `file://` — les graphiques (Leaflet, Chart.js) ne se chargent pas correctement.

### Options Python

```bash
python3 google-takeout-audit.py /chemin/vers/Takeout
python3 google-takeout-audit.py /chemin/vers/Takeout -o /tmp/audit.html
python3 google-takeout-audit.py /chemin/vers/Takeout --raw-gps   # carte plus dense (plus lent)
```

## Fonctionnalités

| Section | Source Takeout |
|---------|----------------|
| Carte de chaleur mondiale | Semantic Location History + échantillon Records.json |
| Voyages hors domicile | Adresses timeline |
| Audit par catégorie | Inventaire des fichiers exportés |
| Recherches sensibles | Mon activité / My Activity (HTML) |
| Alertes vie privée | Géoloc, vocal, domicile tagué… |

## Avertissement

Le dashboard contient des **données personnelles extrêmement sensibles**. Ne le partagez pas tel quel, ne l'hébergez pas en ligne. L'outil sert à comprendre ce que Google a conservé sur vous.

## Limites

- Parsing HTML de « Mon activité » (français et anglais) — pas d'API Google
- Stdlib Python uniquement (pas de `pip install`)
- Les regrets sont un échantillon classé par mots-clés heuristiques, pas une analyse IA

## Licence

MIT — voir [LICENSE](LICENSE).