# Paso 2: Crear la Instancia EC2 en AWS

1. **Nombre:** `misterticket-frontend`
2. **AMI:** **Amazon Linux 2023 AMI** (capa gratuita).
3. **Tipo de Instancia:** `t2.micro` o `t3.micro` (Next.js puede funcionar bien aquí, aunque `t3.small` compilará más rápido).
4. **Par de claves (inicio de sesión - SSH):**
   * Usa una clave existente (como `misterticket-key.pem`) o crea una nueva.
   * **Guárdalo en un lugar seguro**, ya que lo usarás para conectarte por SSH.
5. **Configuraciones de red (Security Group):**
   - Permitir **SSH** (puerto `22`) desde tu IP o cualquier lugar (`0.0.0.0/0`).
   - Permitir **HTTP** (puerto `80`) desde cualquier lugar (`0.0.0.0/0`) (ya que Docker Compose mapeará el puerto 80 del servidor directamente a Next.js).
6. **Almacenamiento:** `8 GiB gp3` o `16 GiB gp3`.

Anota la **IP pública** de tu nueva instancia.

---

> **Siguiente paso:** [03_INSTALAR_HERRAMIENTAS.md](./03_INSTALAR_HERRAMIENTAS.md)  
> **Volver al índice:** [00_RESUMEN_GENERAL.md](./00_RESUMEN_GENERAL.md)
