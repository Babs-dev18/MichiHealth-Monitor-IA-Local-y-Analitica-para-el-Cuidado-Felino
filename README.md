# 🐈 MichiHealth Monitor: IA Local y Analítica para el Cuidado Felino

¡Bienvenido! Este proyecto de Home-Lab nace de la necesidad de monitorizar la salud urinaria de mis dos gatos siameses mediante el análisis de su frecuencia de uso del arenero. Utiliza hardware reciclado, cámaras analógicas, procesamiento en los bordes (Edge Computing) e Inteligencia Artificial local para identificar a cada mascota sin depender de la nube.

## 📊 Arquitectura del Sistema
El sistema se compone de una infraestructura híbrida que optimiza el uso de CPU mediante aceleración de hardware nativa:

* **Captura de Vídeo:** Cámara analógica Loocam -> Capturadora USB EasyCap -> Servidor HP EliteDesk G4.
* **Procesamiento de Streaming:** `go2rtc` para la gestión de flujos eficientes a bajos FPS.
* **Detección de Objetos e IA:** Frigate NVR (aceleración OpenVINO por CPU Intel de 8ª Gen) -> Double Take -> CompreFace (Reconocimiento facial y de patrones).
* **Lógica y Alertas:** Home Assistant (Docker) para registrar datos en bases de datos locales y lanzar notificaciones automáticas vía Telegram/App.
* **Container Tools:** Extensión VSCODE para crear, manejar y desplegar servicios en contenedores.

## 🛠️ Requisitos de Hardware
* **Servidor:** HP EliteDesk 800 G4 Mini (Intel i5-8500T, 32GB RAM, 500GB NMVE).
* **Red:** Smart Switch Cudy GS105ES1 (Aislamiento por puertos / MTU VLAN para aislar la cámara IoT y el punto de acceso de la red principal).
* **Almacenamiento:** HDD Western Digital Red 8TB (CMR) dedicado a las grabaciones y eventos de la IA.
* **Alimentación:** Cargador de 12V 3A (5.5mm x 2.1mm) para asegurar la estabilidad del almacenamiento.

## 🚀 Despliegue rápido
1. Clonar este repositorio.
2. Configurar las variables de entorno en el archivo `docker/.env`.
3. Levantar el stack de monitorización:
   ```bash
   docker compose -f docker/docker-compose.yml up -d