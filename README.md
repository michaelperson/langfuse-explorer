# Langfuse Explorer — Guide

Guide d'exploration autonome de l'interface **Langfuse v4** (4.46.0 auto-hébergé, mode `events_only`).

C'est la partie « guide » du kit Langfuse Explorer, l'annexe de la formation « Orchestration d'agents & Monitoring : LangGraph + Langfuse ». Le kit démarre un Langfuse local et y injecte sept jours d'activité synthétique d'un helpdesk propulsé par des agents LangGraph. On y trouve des réponses correctes, mais aussi une boucle infinie, une fuite de données personnelles, une injection de prompt réussie et une régression en production. Ce guide aide l'apprenant à retrouver tout cela dans l'interface.

## Ce que contient le guide

`index.html` est une page unique et autonome. Elle s'ouvre dans un navigateur et fonctionne hors ligne. Elle propose :

- **Par question** : une question de diagnostic (« Quelle requête est la plus chère ? », « Que fait cet utilisateur ? ») renvoie vers l'écran qui y répond. La recherche parcourt aussi les missions.
- **Missions** : 33 missions réparties sur trois niveaux.
  - *Découverte* : se repérer et lire une trace.
  - *Enquête* : diagnostiquer les erreurs, les lenteurs, les coûts et le comportement de l'agent.
  - *Expert* : gouverner les données personnelles, la sécurité, les régressions et les décisions.

  Les réponses sont vérifiées dans la page. La progression est enregistrée dans le navigateur et peut être exportée.
- **L'interface, écran par écran** : pour chaque écran de Langfuse, son rôle, ce qu'il faut regarder, le piège classique, les missions associées et une capture.
- **Ce qui change en v4** : les différences avec la v3 (modèle de données, écran Tracing, ingestion OpenTelemetry, API, SDK). La plupart des tutoriels en ligne montrent encore la v3.
- **Glossaire** : trace, observation, session, score, dataset, TTFT…

Les liens « Ouvrir dans Langfuse » pointent vers l'adresse réglée en haut de la page (par défaut `http://localhost:3100`).

## Structure

```
guide/
├── index.html          # le guide généré, à ouvrir dans un navigateur
├── screens/            # captures des écrans de Langfuse
└── source/
    ├── ecrans.yaml     # carte de l'interface : rôle, points à regarder, pièges, questions
    ├── missions.yaml   # niveaux et missions : consigne, indice, réponses acceptées, enjeux
    └── template.html   # gabarit HTML/CSS/JS dans lequel les données sont injectées
```

`index.html` est **généré** : on ne le modifie pas à la main. Pour changer le contenu, on édite les fichiers de `source/`, puis on regénère depuis la racine du kit :

```bash
uv run --project seed tools/build_guide.py
```

Le script vérifie au passage que les réponses des missions qui référencent `formateur/faits.json` correspondent toujours aux données injectées. Les captures de `screens/` sont produites par `tools/capture_screens.py`.

## Utilisation

1. Lancer le kit depuis sa racine (`.\start.ps1` sous Windows, `./start.sh` sous Linux ou macOS). Docker doit être démarré.
2. Se connecter à Langfuse avec le compte affiché à la fin du script (`explorer@helpdesk.local`).
3. Ouvrir `index.html`, régler la période de Tracing sur **7 jours**, puis commencer par les missions du niveau Découverte.

Aucun GPU n'est requis : un portable avec Docker et 8 Go de RAM suffit (16 Go conseillés).

> Les données sont entièrement fictives : l'entreprise NordTech SA n'existe pas.
