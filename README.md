# 🏃 Endurain Docker - Rastreador de Fitness Autohospedado

[![GitHub Stars](https://img.shields.io/github/stars/endurain-project/endurain?style=flat-square&logo=github)](https://github.com/endurain-project/endurain)
[![Docker Pulls](https://img.shields.io/docker/pulls/endurainproject/endurain?style=flat-square&logo=docker)](https://hub.docker.com/r/endurainproject/endurain)
[![License](https://img.shields.io/github/license/endurain-project/endurain?style=flat-square)](https://github.com/endurain-project/endurain/blob/main/LICENSE)
[![Codeberg](https://img.shields.io/badge/Codeberg-endurain--project%2Fendurain-2F80ED?style=flat-square&logo=codeberg)](https://codeberg.org/endurain-project/endurain)

## 📋 Descripción general

**Endurain** es un rastreador de fitness autohospedado construido como alternativa privada a Strava. Desarrollado con **Python FastAPI** en el backend, **Vue.js 3 + Tailwind CSS** en el frontend y **PostgreSQL** como base de datos. Permite importar entrenamientos en formatos GPX, TCX, FIT y EXIF, analizar entrenamientos con mapas interactivos, soportar múltiples deportes, sincronizar con Garmin Connect y Strava, y mantener control total sobre tus datos sin compartirlos con terceros.

> 🎯 **Propuesta clave**: Self-hosted fitness tracker (Python + Vue.js + PostgreSQL). Import GPX/TCX/FIT. Analyze workouts. Display maps. Support multiple sports. Statistics. Garmin/Strava sync. Multi-language (Weblate). No third-party data sharing. API REST. Privacy-first. 173+ GitHub stars. AGPL-3.0 open source. Demo available. Feature freeze ongoing. Development active on Codeberg. Multi-arch Docker image. Production-ready for personal/small team use.

## ✨ Características principales

- 📁 **Importación de datos**: GPX, TCX, FIT (Garmin), EXIF fotos, Strava export, múltiples fuentes
- 📊 **Análisis entrenamientos**: Duración, distancia, calorías, ritmo medio, elevación, mapas con track
- 🏃 **Múltiples deportes**: Running, ciclismo, natación, esquí, senderismo, hiking, triatlón
- 📈 **Estadísticas**: Por mes, año. Distancia total, tiempo, calorías. Gráficos de progreso
- 🔄 **Sincronización Garmin**: Conecta con Garmin Connect. Import automático de entrenamientos desde reloj
- 🗺️ **Mapas interactivos**: Leaflet.js. Visualiza rutas. Zoom, satélite, topográfico, layers
- 🌐 **Multi-idioma**: Weblate. Crowdsourced translations. Español, inglés, francés, más
- 🔌 **API REST**: API completa. Webhooks. Automatización. Integración con terceros
- 🔒 **Privacidad total**: Sin datos compartidos con terceros. Control total sobre tu información
- ⚡ **Stack moderno**: Python 3.10+, FastAPI, Vue.js 3, TypeScript, Tailwind CSS, PostgreSQL 15+

## 📋 Requisitos del sistema

- **Docker y Docker Compose**: versión reciente
- **RAM**: mínimo 2 GB; recomendado 3+ GB
- **Almacenamiento**: 5-20 GB (entrenamientos históricos)
- **Puertos**: 8000 (app web), 5432 (PostgreSQL opcional)
- **Navegador**: Chrome, Firefox, Safari moderno (VueJS 3)

> 📌 **Tip**: Endurain está en feature freeze temporal. Desarrollo activo en Codeberg. Demo diaria se resetea.

## 🐳 Instalación

### Paso 1: Crear docker-compose.yml

```yaml
version: '3.8'

services:
  endurain:
    image: codeberg.org/endurain-project/endurain:latest
    ports:
      - "8000:8000"
    environment:
      DATABASE_URL: postgresql://endurain:contraseña@postgres:5432/endurain
      DEBUG: "false"
      TZ: Europe/Madrid
    depends_on:
      - postgres
    volumes:
      - ./data:/app/data
    networks:
      - endurain-net

  postgres:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: endurain
      POSTGRES_USER: endurain
      POSTGRES_PASSWORD: contraseña_db_segura
      TZ: Europe/Madrid
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - endurain-net

volumes:
  postgres_data:

networks:
  endurain-net:
```

### Paso 2: Lanzar Docker Compose

```bash
docker compose up -d
```

### Paso 3: Acceder a la interfaz

La aplicación estará disponible en **http://localhost:8000** en ~30 segundos.

## ⚙️ Configuración

1. **Accede a la interfaz web** en http://localhost:8000
2. **Regístrate** creando tu cuenta de administrador o usa credenciales demo (admin/admin)
3. **Configura zona horaria** en Settings → General → Timezone (ej. Europe/Madrid)
4. **Importa tu primer entrenamiento** subiendo archivo GPX/TCX/FIT o desde Strava Export
5. **Configura sincronización Garmin** (opcional): Settings → Garmin Connect → Autoriza con credenciales Garmin
6. **Ajusta notificaciones** (opcional): Settings → Notifications → Apprise (email, Slack, Discord, etc)
7. **Configura backup automático** de la base de datos PostgreSQL

## 🚀 Primeros pasos

1. **Clona o descarga** el archivo `docker-compose.yml` en tu servidor
2. **Modifica las contraseñas** en el archivo (POSTGRES_PASSWORD y DATABASE_URL) por valores seguros
3. **Ejecuta** `docker compose up -d` para levantar los contenedores
4. **Espera ~30 segundos** a que la aplicación inicie completamente
5. **Abre el navegador** en http://localhost:8000 (o tu IP:8000)
6. **Crea tu cuenta** de administrador en la pantalla de registro
7. **Sube tu primer entrenamiento** arrastrando un archivo GPX/TCX/FIT o importando desde Strava
8. **Explora** el dashboard, mapas, estadísticas y configuración

## 💡 Casos de uso

- 🏃 **Atletas privados**: Rastreo sin compartir datos con Strava/Garmin
- 👥 **Equipos**: Análisis entrenamientos del equipo. Comparación performance
- 🏋️ **Entrenadores**: Monitoreo entrenamientos de atletas. Análisis colectivo
- 🔄 **Migración desde Strava**: Import histórico. Control total después
- 🛡️ **GDPR compliance**: Datos locales. Sin sincronización automática a terceros
- 📊 **Análisis personal**: Histórico detallado. Gráficos. Progreso a largo plazo

## 🔒 Acceso remoto seguro

Para acceder a Endurain desde internet de forma segura:

1. **Reverse Proxy** (recomendado): Nginx Proxy Manager, Traefik o Caddy con SSL automático (Let's Encrypt)
2. **VPN**: WireGuard, Tailscale o OpenVPN para acceso solo a tu red privada
3. **Cloudflare Tunnel**: Acceso sin abrir puertos en router, con WAF y DDoS protection
4. **Autenticación adicional**: Authelia/Keycloak delante del proxy para 2FA

> ⚠️ **Nunca expongas el puerto 8000 directamente a internet** sin autenticación y TLS.

## 🛠️ Gestión y mantenimiento

### Ver estado y logs
```bash
docker compose ps
docker compose logs -f endurain
```

### Detener contenedor
```bash
docker compose down
```

### Actualizar Endurain
```bash
docker compose pull
docker compose up -d
```

### Backup de entrenamientos
```bash
docker exec endurain_postgres_1 pg_dump -U endurain endurain > entrenamientos_backup.sql
```

### Restaurar backup
```bash
docker exec -i endurain_postgres_1 psql -U endurain endurain < entrenamientos_backup.sql
```

### Monitoreo
- **Entrenamientos subidos**: Dashboard muestra total
- **Últimos entrenamientos**: Ver en timeline
- **Sincronización Garmin**: Log en Settings
- **Uso DB**: PostgreSQL crece ~10-50 MB por 1000 entrenamientos

## 📝 Licencia

Este proyecto está licenciado bajo **AGPL-3.0** - ver el archivo [LICENSE](https://codeberg.org/endurain-project/endurain/src/branch/main/LICENSE) para más detalles.

---

> 📖 **Artículo original**: [Cómo instalar Endurain en Docker: Rastreador de Fitness Autohospedado en Docker](https://genbyte.blogspot.com/2026/10/endurain-rastreador-de-fitness.html)  
> 🎥 **Vídeo tutorial**: [Canal GENBYTE en YouTube](https://www.youtube.com/@GENBYTE)  
> 💬 **Comunidad**: [Telegram](https://t.me/genbyte) | [Discord](https://discord.gg/genbyte) | [GitHub](https://github.com/endurain-project)  
> ☕ **Apoya el proyecto**: [Ko-fi](https://ko-fi.com/genbyte) | [Codeberg](https://codeberg.org/endurain-project/endurain)