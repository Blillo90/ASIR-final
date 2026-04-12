# 🚀 ASIR Final Project - DevOps Deployment on AWS

Proyecto de despliegue automatizado de una aplicación web utilizando prácticas DevOps reales.

---

## 📌 Descripción

Este proyecto implementa un flujo completo de despliegue automatizado usando:

- AWS EC2 como infraestructura
- Docker para la contenedorización
- Ansible para la automatización
- GitHub Actions para CI/CD

El objetivo es simular un entorno real de producción simplificado, optimizado para una sola máquina EC2, manteniendo buenas prácticas DevOps y aprovechando la automatización del ciclo completo de despliegue.

---

## 🏗️ Arquitectura

```text
Local (VSCode)
   ↓
GitHub (Repositorio)
   ↓
GitHub Actions (CI/CD)
   ↓
Ansible (automatización)
   ↓
EC2 en AWS
   ↓
Docker
   ↓
Aplicación Web
```

---

## ⚙️ Tecnologías utilizadas

- Python
- Flask
- Docker
- Docker Compose
- Ansible
- GitHub Actions
- AWS EC2
- UFW
- Fail2Ban

---

## 📂 Estructura del proyecto

```text
ASIR-final/
├── app/                 # Código fuente de la aplicación
├── docker/              # Dockerfile y docker-compose.yml
├── ansible/             # Inventario, variables y playbooks
├── .github/workflows/   # Pipeline CI/CD
├── README.md
└── .gitignore
```

---

## 🚀 Despliegue automático

Cada vez que se hace un `push` a la rama `main`, GitHub Actions ejecuta automáticamente el pipeline de despliegue.

El flujo es el siguiente:

1. GitHub Actions descarga el repositorio.
2. Configura la conexión SSH con la máquina EC2.
3. Ejecuta Ansible contra la EC2.
4. Ansible:
   - prepara el servidor
   - instala o verifica Docker
   - copia la aplicación y los archivos necesarios
   - lanza el despliegue con Docker Compose

---

## 🔐 Secrets necesarios en GitHub

En el repositorio, dentro de:

**Settings > Secrets and variables > Actions**

se deben crear los siguientes secretos:

- `EC2_HOST` → IP pública o DNS público de la máquina EC2
- `EC2_SSH_KEY` → clave privada SSH usada por GitHub Actions para conectarse a la EC2

Opcionalmente, si se quiere parametrizar más adelante:

- `EC2_USER`
- variables de entorno de la aplicación

---

## 🐳 Ejecución manual para pruebas

Si se quiere probar manualmente en la EC2:

```bash
docker compose up -d --build
```

---

## 🔧 Ejecución manual de Ansible

Para lanzar los playbooks manualmente desde local:

```bash
ansible-playbook ansible/playbooks/site.yml
```

---

## 🌐 Acceso a la aplicación

Una vez desplegada, la aplicación será accesible desde:

```text
http://IP_PUBLICA_EC2
```

Si más adelante se configura dominio y HTTPS, el acceso podrá hacerse por nombre DNS y con certificado.

---

## 🛡️ Seguridad aplicada

La solución incluye medidas básicas de seguridad:

- uso de firewall con UFW
- protección básica contra intentos de fuerza bruta mediante Fail2Ban
- acceso SSH con clave privada
- secrets sensibles almacenados en GitHub Secrets
- automatización reproducible mediante Ansible

---

## 📈 Posibles mejoras futuras

- Configuración de HTTPS con Let's Encrypt
- Uso de Nginx como reverse proxy
- Separación de entornos `dev` y `prod`
- Publicación de imágenes en Docker Hub o GitHub Container Registry
- Uso de Amazon RDS en lugar de base de datos local
- Monitorización con Prometheus y Grafana
- Backups automáticos

---

## 👨‍💻 Autor

Proyecto realizado por Pablo Pérez Herrero  
ASIR - Administración de Sistemas Informáticos en Red

---

## 📄 Licencia

Proyecto con fines educativos.

