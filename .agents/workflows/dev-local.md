---
description: Lancer l'environnement de développement local complet
---

# Environnement de dev local

## Prérequis
- Docker Desktop démarré
- Node.js 20+
- Tous les repos clonés dans `d:\dev\`

## Étapes

// turbo
1. Démarrer les services Docker (TimescaleDB + Mosquitto)
```bash
cd d:\dev\iot-mesurable-infra
docker-compose -f docker-compose.dev.yml up -d
```

2. Vérifier que les services sont up
```bash
docker-compose -f docker-compose.dev.yml ps
```

3. Démarrer le backend
```bash
cd d:\dev\iot-mesurable-server
npm run dev
```

4. Démarrer le frontend (dans un autre terminal)
```bash
cd d:\dev\iot-mesurable-nuxt-app
npm run dev
```

5. Accéder au dashboard
- Frontend : http://localhost:3000
- API : http://localhost:3001
- Swagger : http://localhost:3001/documentation

## Notes
- Le backend se connecte au MQTT broker local (port 1883)
- TimescaleDB est exposé sur le port 5432
- Drizzle Studio : `npm run db:studio` dans le dossier server
