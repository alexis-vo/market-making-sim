# Market Making Sim

Plateforme de simulation de market making : cotation simultanée bid/ask avec
gestion de l'inventaire, testée sans passage d'ordres réels.

## Objectif

Simuler le passage d'ordres sur un marché pour tester des stratégies de
market making, en tenant compte :
- des coûts de transaction réels (frais fixes, spread bid-ask, frais
  proportionnels au volume)
- de l'impact de marché : sur un marché peu liquide, un ordre simulé de
  taille significative doit affecter le prix simulé, même s'il n'apparaît
  pas dans les données historiques rejouées.

## Architecture

Le projet est découpé en trois briques, correspondant aux modules de `src/` :

```
src/
├── market_data/     # Récupération des données de marché (prix, volumes,
│                    # profondeur de carnet d'ordres) en temps réel ou
│                    # quasi temps réel, coûts de transaction inclus
├── execution/        # Simulation du passage d'ordres (limite / marché)
│                    # sur le carnet, avec calcul du prix et volume exécutés
└── market_impact/    # Modèles d'impact de marché : Almgren-Chriss,
                     # loi en racine carrée, agent-based, processus de
                     # Hawkes, calibration sur données granulaires (LOBSTER)
```

## Pistes explorées pour l'impact de marché

- Modèles paramétriques (impact temporaire / permanent, Almgren-Chriss)
- Loi en racine carrée : impact ∝ σ√(Q/V)
- Simulateurs de carnet d'ordres à agents (agent-based models)
- Processus ponctuels (Hawkes) pour l'auto-excitation des arrivées d'ordres
- Calibration empirique sur données granulaires type LOBSTER

## Installation

```bash
python -m venv .venv
source .venv/bin/activate  # Windows : .venv\Scripts\activate
pip install -r requirements.txt
```

## Équipe

- Alexis VO
- Guerand DEWELL
- Thomas PRICE
- Sergio NOBIME

## Statut

🚧 En cours — projet réalisé en autonomie de groupe.
