# Paso 1: Archivos de Configuración Requeridos en tu Proyecto Frontend

Para habilitar Docker en el frontend de **MisterTicket**, debes asegurarte de tener los siguientes dos archivos en la raíz de tu carpeta `MisterTicket/frontend/`:

### 📄 `Dockerfile`
Este archivo en la raíz del frontend define cómo se construye la imagen de la aplicación Next.js:

```dockerfile
# Usa la imagen oficial de Node.js como base
FROM node:20-alpine

# Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar package.json y package-lock.json
COPY package.json package-lock.json ./

# Instalar dependencias
RUN npm ci

# Copiar el resto del código de la aplicación
COPY . .

# Construir la aplicación para producción
RUN npm run build

# Exponer el puerto en el que Next.js correrá
EXPOSE 3000

# Iniciar la aplicación
CMD ["npm", "start"]
```

### 📄 `docker-compose.yml`
Este archivo orquesta la aplicación web para que sea fácil levantarla y actualizarla:

```yaml
services:
  frontend:
    build: .
    container_name: misterticket_frontend
    restart: always
    ports:
      - "80:3000"  # Expone el puerto 80 del servidor hacia el 3000 del contenedor
    environment:
      # URL pública de tu backend EC2 (ej. http://IP_EC2_BACKEND/api)
      - NEXT_PUBLIC_API_URL=http://TU_IP_PUBLICA_EC2_BACKEND/api
```

> **Nota:** La variable `NEXT_PUBLIC_API_URL` es crucial. Si el backend está en otra instancia EC2, aquí debes poner la IP pública de esa máquina.

---

> **Siguiente paso:** [02_CREAR_INSTANCIA_EC2.md](./02_CREAR_INSTANCIA_EC2.md)  
> **Volver al índice:** [00_RESUMEN_GENERAL.md](./00_RESUMEN_GENERAL.md)
