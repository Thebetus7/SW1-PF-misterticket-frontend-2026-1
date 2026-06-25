# Paso 5: Actualizar el Proyecto en Producción

Cuando modificas código del frontend en tu PC y quieres que esos cambios se reflejen en AWS, el flujo es el siguiente:

### A) En tu PC local (antes de tocar el servidor)

Abre una terminal en la carpeta del proyecto frontend en tu computadora:

```bash
cd MisterTicket/frontend
```

Guarda tus cambios y súbelos a GitHub:

```bash
git add .
git commit -m "Descripción breve de lo que cambiaste"
git push origin main
```

### B) En el servidor AWS

**1. Conéctate por SSH:**
```bash
ssh -i misterticket-key.pem ec2-user@TU_IP_PUBLICA_EC2_FRONTEND
```

**2. Ve a la carpeta del proyecto:**
```bash
cd /home/ec2-user/misterticket-frontend
```

**3. Descarga el código nuevo desde GitHub:**
```bash
git pull origin main
```

**4. Reconstruye y reinicia el contenedor:**
```bash
docker-compose up -d --build
```
*Next.js generará una nueva compilación de producción con los últimos cambios.*

**5. Comprueba que la actualización funcionó revisando los logs:**
```bash
docker-compose logs --tail=50 frontend
```

---

### Resumen rápido (solo servidor AWS)

Copia y pega esto en orden después de conectarte por SSH:

```bash
cd /home/ec2-user/misterticket-frontend
git pull origin main
docker-compose up -d --build
docker-compose logs --tail=30 frontend
```

---

> **Siguiente paso:** [06_APAGAR_SERVICIOS.md](./06_APAGAR_SERVICIOS.md)  
> **Volver al índice:** [00_RESUMEN_GENERAL.md](./00_RESUMEN_GENERAL.md)
