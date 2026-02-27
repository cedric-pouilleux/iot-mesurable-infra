---
description: Déployer la stack complète sur Raspberry Pi
---

# Déployer sur Raspberry Pi

## Prérequis
- SSH accès au Raspberry Pi
- Docker et Docker Compose installés
- Les repos clonés sur le Pi

## Étapes

1. Se connecter au Raspberry Pi
```bash
ssh pi@<IP_DU_PI>
```

2. Aller dans le dossier infra
```bash
cd ~/iot-mesurable-infra
```

3. Pull les dernières modifications
```bash
git pull
cd ../iot-mesurable-server && git pull
cd ../iot-mesurable-nuxt-app && git pull
cd ../iot-mesurable-infra
```

4. Rebuild et redémarrer les services
```bash
docker-compose up -d --build
```

5. Vérifier que tout tourne
```bash
docker-compose ps
docker-compose logs -f backend
```

6. Vérifier l'accès web
- Dashboard : http://<IP_DU_PI>
- API : http://<IP_DU_PI>/api/modules
