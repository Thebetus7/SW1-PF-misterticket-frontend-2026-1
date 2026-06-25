# Paso 4: Subir y Desplegar el Proyecto en AWS

Una vez preparadas las herramientas en el servidor, desplegaremos la aplicación frontend.

## 4.1 Clonar el proyecto
Clona tu repositorio en la EC2:
```bash
git clone <URL_DEL_REPOSITORIO> misterticket-frontend
cd misterticket-frontend
```

## 4.2 Levantar contenedores
Levanta el contenedor en segundo plano (background):
```bash
docker-compose up -d --build
```
*Nota: Este proceso instalará las dependencias y construirá (`npm run build`) el proyecto Next.js dentro de la imagen. Puede tardar un par de minutos.*

¡Listo! Tu frontend está en línea en `http://IP_PUBLICA_EC2_FRONTEND/`.

---

## ⚠️ Solución de problemas comunes

### `compose build requires buildx 0.17.0 or later`
Ejecuta en la EC2:
```bash
sudo mkdir -p /usr/local/lib/docker/cli-plugins
sudo curl -L "https://github.com/docker/buildx/releases/download/v0.19.3/buildx-v0.19.3.linux-amd64" -o /usr/local/lib/docker/cli-plugins/docker-buildx
sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-buildx
export DOCKER_CLI_PLUGIN_EXTRA_DIRS=/usr/local/lib/docker/cli-plugins
echo 'export DOCKER_CLI_PLUGIN_EXTRA_DIRS=/usr/local/lib/docker/cli-plugins' >> ~/.bashrc
sudo systemctl restart docker
docker-compose up -d --build
```

---

## 🛑 Comandos de Mantenimiento

### Ver Logs:
```bash
docker-compose logs -f frontend
```

### Detener el Contenedor:
```bash
docker-compose down
```

### Reiniciar/Levantar de nuevo:
```bash
docker-compose up -d
```

---

> **Siguiente paso:** [05_ACTUALIZAR_PRODUCCION.md](./05_ACTUALIZAR_PRODUCCION.md)  
> **Volver al índice:** [00_RESUMEN_GENERAL.md](./00_RESUMEN_GENERAL.md)
