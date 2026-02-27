# IoT Mesurable - Infrastructure

Infrastructure Docker pour le déploiement sur Raspberry Pi (production) et le développement local.

## Architecture de déploiement

```
Raspberry Pi 5
├── Nginx (reverse proxy, port 80)
│   ├── / → Frontend Nuxt (port 3000)
│   ├── /api → Backend Fastify (port 3001)
│   └── /socket.io → WebSocket Backend
├── Backend Fastify (port 3001)
├── Frontend Nuxt (port 3000)
├── Mosquitto MQTT (port 1883, 9001 WS)
└── TimescaleDB PostgreSQL (port 5432)
```

## Environnements

### Dev (docker-compose.dev.yml)
- Seulement TimescaleDB + Mosquitto
- Backend et frontend tournent **en local** (npm run dev)
- Ports exposés : 5432, 1883, 9001

### Prod (docker-compose.yml)
- Stack complète avec Nginx
- Backend et frontend en containers Docker
- Seul port exposé : 80 (via Nginx)

## Commandes

```bash
# Dev
docker-compose -f docker-compose.dev.yml up -d

# Prod (sur Raspberry Pi)
docker-compose up -d --build

# Logs
docker-compose logs -f backend
docker-compose logs -f mosquitto
```

## Bonnes pratiques

- Toujours utiliser `.env` pour les credentials (pas de valeurs en dur)
- Le bridge Mosquitto permet le dev local avec le broker du Pi
- En prod, les services communiquent via le réseau Docker `iot_net`
- TimescaleDB utilise un volume nommé pour la persistance

## Problèmes connus

- Après coupure de courant, le Raspberry Pi peut ne pas se reconnecter au réseau → vérifier la config réseau systemd
