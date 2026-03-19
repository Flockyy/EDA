# EDA — Airbnb Bordeaux

Analyse exploratoire de données (EDA) sur des annonces de logements type Airbnb à Bordeaux.

Le projet est centré sur le notebook `eda.ipynb`, avec préparation des données, analyses descriptives, exploration temporelle/saisonnière, corrélations, et visualisations géographiques.

## Executive summary

- Les prix varient fortement selon le quartier et le type de logement, avec des écarts marqués entre médiane et moyenne dans plusieurs zones.
- La disponibilité présente une saisonnalité nette, et le proxy d’occupation (1 - disponibilité) met en évidence des périodes plus tendues.
- Les hôtes multi-annonces montrent des comportements tarifaires distincts des hôtes mono-annonce.
- La relation entre prix et volume d’avis est explorée par corrélation et par tranches de prix (vue macro, non causale).
- La carte Folium permet de visualiser les contrastes géographiques (prix médian, volume d’annonces, occupation) par quartier.

## Structure du projet

```text
EDA/
├── eda.ipynb
├── README.md
├── carte_quartiers_bordeaux.html
├── eda_price_analysis.png
├── eda_reviews_analysis.png
├── eda_seasonality.png
├── eda_geographic_availability.png
├── eda_exploration_questions.png
└── data/
    ├── listings.csv
    ├── listings.csv.gz
    ├── calendar.csv.gz
    ├── reviews.csv
    ├── reviews.csv.gz
    ├── neighbourhoods.csv
    └── neighbourhoods.geojson
```

## Données utilisées

Le notebook charge plusieurs sources complémentaires :

- `listings.csv` et `listings.csv.gz` : caractéristiques des annonces (prix, type de logement, capacité, etc.)
- `calendar.csv.gz` : disponibilité quotidienne et prix dans le temps
- `reviews.csv` et `reviews.csv.gz` : avis et temporalité des avis
- `neighbourhoods.csv` et `neighbourhoods.geojson` : dimensions géographiques/quartiers

## Contenu du notebook

Le notebook couvre principalement :

1. **Chargement + inspection** des jeux de données
2. **Nettoyage/préparation** :
   - conversion des prix (`$`, `,`) en numérique
   - conversion des dates
   - traitement de colonnes numériques importées en texte
   - gestion de valeurs manquantes et clipping IQR
3. **Feature engineering & jointures** :
   - enrichissement `listings` avec métriques du calendrier
   - proxy de taux d’occupation
4. **Analyses descriptives** :
   - distributions de prix par type/quartier
   - statistiques agrégées de variables clés
   - dynamique des avis
5. **Analyses temporelles/saisonnalité** :
   - disponibilité/occupation mensuelle
   - saisonnalité par mois
6. **Questions exploratoires métier** :
   - quartiers les plus/moins chers
   - disponibilité par saison
   - tarification hôtes mono vs multi-annonces
   - corrélation prix vs volume d’avis
7. **Visualisations** :
   - graphiques statiques (`matplotlib`, `seaborn`)
   - carte interactive (`folium` + `geojson`)

## Sorties générées

Le notebook génère (ou met à jour) les fichiers suivants :

- `carte_quartiers_bordeaux.html`
- `eda_price_analysis.png`
- `eda_reviews_analysis.png`
- `eda_seasonality.png`
- `eda_geographic_availability.png`
- `eda_exploration_questions.png`

## Environnement et exécution

### Prérequis

- Python 3.10+
- Environnement virtuel recommandé (`.venv`)
- Jupyter/VS Code Notebook

### Installation rapide

```bash
python -m venv .venv
source .venv/bin/activate
pip install pandas numpy matplotlib seaborn folium ipython jupyter
```

### Lancer l’analyse

1. Ouvrir `eda.ipynb` dans VS Code ou Jupyter Lab.
2. Exécuter les cellules dans l’ordre.
3. Vérifier les fichiers de sortie générés à la racine du projet.

## Notes de qualité

- Le notebook contient des versions complémentaires de certaines analyses (tableaux + visualisations).
- Les variables de prix sont standardisées en numérique avant agrégation.
- Le taux d’occupation est calculé comme un **proxy** basé sur la disponibilité (`available_flag`).

## Pistes d’amélioration

- Factoriser certaines cellules en fonctions réutilisables.
- Ajouter une section de validation (tests de cohérence des agrégats).
- Exporter un rapport final (HTML/Markdown) synthétisant les indicateurs clés.