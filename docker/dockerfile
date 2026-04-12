# 1. Imagen base ligera con Python
FROM python:3.11-slim

# 2. Evitar problemas con buffers (logs en tiempo real)
ENV PYTHONUNBUFFERED=1

# 3. Directorio de trabajo dentro del contenedor
WORKDIR /app

# 4. Copiar requirements primero (optimiza caché)
COPY app/requirements.txt .

# 5. Instalar dependencias!
RUN pip install --no-cache-dir -r requirements.txt

# 6. Copiar el resto del código
COPY app/ .

# 7. Exponer puerto (informativo)
EXPOSE 5000

# 8. Comando de arranque
CMD ["python", "app.py"]