# Projet Big Data & Business Intelligence - DigiCheese

## 📌 Description
Ce projet a pour objectif de mettre en oeuvre un ensemble de technologies **Big Data** (Hadoop, HBase, Python, HappyBase) et **Business intelligence** (Power BI) afin d'analyser un entrepôt de données d'une fromagerie de merde.

À partir du fichier source `dataw_fro.csv` (données de commande depuis 2004), le projet est découpé en plusieurs **lots** :

- **LOT 0** : Nettoyage et préparation des données (Data Analyst)
- **Lot 1** : Traitement MapReduce Hadoop pour obtenir les 100 meilleurs commandes (2006-2010 départements 53/61/28)
- **LOT 2** : Analyse complémentaire (2011-2016, départements 22/49/53, échantillon aléatoire 5%) avec export et graphiques
- **LOT 3** : Stockage et interrogation des données dans **Hbase** (NoSQL) via **HappyBase (Pyhon)**
- **LOT 4** : Création de **dashboards interactifs Power BI** connectés aux données

Le livrable final comprend : 

- Un **ensemble d'applications/scripts** (Hadoop, HBase, Python)
- Des **exports de résultats** (CSV, Excel, PDF)
- Un **dashboard Power BI**
- Un **dossier documentaire** (analyses, procédures, recommandations)

## 📂 Arborescence du dépôt

```
/data/            → Données sources et résultats
   ├── dataw_fro.csv         (fichier source brut)
   ├── dataw_fro_clean.csv   (données nettoyées, LOT 0)
   └── exports/              (résultats en CSV, Excel, PDF)

/notebooks/       → Notebooks Jupyter pour exploration et prototypes
   └── 00_cleaning.ipynb     (nettoyage et analyse exploratoire)

/etl/             → Scripts Hadoop Streaming (ETL)
   ├── mapper_lot1.py
   ├── reducer_lot1.py
   ├── mapper_lot2.py
   └── reducer_lot2.py

/hbase/           → Scripts et définitions HBase
   ├── create_table.hbase    (DDL HBase)
   ├── import_csv.py         (import depuis CSV)
   └── queries.py            (requêtes HappyBase)

/analytics_py/    → Scripts analytiques Python
   ├── cleaning.py           (LOT 0 automatisé)
   ├── lot3_exports.py       (exports CSV/XLSX/PDF depuis HBase)
   └── tests/                (tests unitaires)

/powerbi/         → Fichiers Power BI
   ├── projet_bigdata.pbix   (dashboard interactif)
   └── sources.md            (notes de connexion à HBase/CSV)

/docs/            → Documentation projet
   ├── dictionnaire.md       (dictionnaire de données)
   ├── procedures_nettoyage.md
   ├── lot1.md, lot2.md, lot3.md (notes techniques par lot)
   ├── recommandations.md
   └── rapport_final.pdf
```

## ⚙️ Installation & Environnement 

### Prérequis

- **Python** ≥ 3.11
- **Java JDK** ≥ 8
- **Hadoop** (pseudo-distributed mode)
- **HBase** (avec ZooKeeper local)
- **Power BI Desktop** (Windows)

### Dépendances Python

Les dépendances principales sont listées dans `requirements.txt` :

- `pandas`
- `numpy`
- `matplotlib`
- `openpyxl / xslxwriter`
- `happybase`
- `fastparquet / pyarrow`

Installation :

```bash
pip install -r requirements.txt
```

## 🚀 Utilisation

### - LOT 0 (Nettoyage)

```bash
python analytics_py/cleaning.py data/dataw_fro.csv data/dataw_fro_clean.csv
```


### - LOT 1 & 2 (Hadoop Streaming)

```bash
hdfs dfs -put data/dataw_fro_clean.csv /input/
hadoop jar hadoop-streaming.jar \
  -input /input/dataw_fro_clean.csv \
  -output /output/lot1 \
  -mapper etl/mapper_lot1.py \
  -reducer etl/reducer_lot1.py
```

### - LOT 3 (HBASE + HappyBase)

```bash
python hbase/import_csv.py data/dataw_fro_clean.csv
python analytics_py/lot3_exports.py
```

###- LOT 4 (POWER BI)

Ouvrir `powerbi/projet_bigdata.pbix` dans Power BI Desktop.

## 🧾 Documentation

Toutes les procédures détaillés (nettoyage, import HDFS, création HBase, requêtes Python, connexion Power BI) sont décrites dans le dossier `/docs/`.
