# ⚽ FutBotMX – Yoni4Vision

## 📌 Descripción
Este proyecto aplica **YOLOv8 + ByteTrack + SAM3** para analizar partidos de fútbol robótico de la **Copa FutBotMX 2026**.  
El pipeline permite:

- Segmentar campo, robots aliados, robots rivales y balón.  
- Rastrear trayectorias de los robots y el balón.  
- Detectar eventos clave (goles).  
- Generar visualizaciones narrativas: mapas de calor, análisis de posesión y flujo del juego.  

Repositorio oficial: **[Yoni4Vision en GitHub](https://github.com/BlackPanter04/Yoni4Vision.git)**

---

## ⚙️ Instalación y Entorno

### Opción A — Anaconda
1. Instalar **Anaconda**.  
2. Crear entorno:

```bash
conda create -n supervision python=3.11
conda activate supervision
Instalar librerías:
---
CPU:

bash
pip install supervision ultralytics trackers jupyter
GPU NVIDIA:

bash
conda install pytorch torchvision pytorch-cuda=12.1 -c pytorch -c nvidia
pip install supervision ultralytics trackers jupyter
Ajusta pytorch-cuda según tu driver (nvidia-smi).

Descargar modelo SAM3  [Drive Link](https://drive.google.com/drive/folders/18I6zf9HGyLC_w6fJWnResbu0FBkmdveu?usp=drive_link)

HuggingFace → sam3.pt  [Drive Link](https://drive.google.com/drive/folders/18I6zf9HGyLC_w6fJWnResbu0FBkmdveu?usp=drive_link)

Abrir VS Code:
Instalar extensión Python.
Seleccionar kernel supervision.

## Requisitos adicionales
bash
pip install transformers accelerate safetensors datasets opencv-python seaborn matplotlib
pip install -r requirements.txt

##  Archivos externos

Por limitaciones de GitHub, los archivos pesados se encuentran en Google Drive:

- Videos completos del partido → [Drive Link](https://drive.google.com/drive/folders/18I6zf9HGyLC_w6fJWnResbu0FBkmdveu?usp=drive_link)
- Dataset anotado → [Drive Link](https://drive.google.com/drive/folders/18I6zf9HGyLC_w6fJWnResbu0FBkmdveu?usp=drive_link)


## Flujo de Fases
🔹 Fase 1 – YOLO + ByteTrack
Detección de objetos con YOLO.

Tracking con ByteTrack.

Exportación de CSV con detecciones (detecciones_yolo.csv).

🔹 Fase 2 – Segmentación con SAM3
SAM3 recibe cajas de YOLO como prompts.

Segmentación de campo, robots y balón.

Pelota con ID fijo = 1.

Video anotado con trazas (fase1_yolo_bytetrack.mp4).

🔹 Fase 3 – Análisis y Visualización
Mapa de calor de actividad por equipo.

Análisis de posesión con métricas temporales.

Detección de eventos clave (pases, intercepciones, tiros, goles).


##Resultados esperados
posesion_por_frame.csv → métricas de posesión por frame.

Resumen de goles → listado de goles detectados en consola o exportado a CSV.

Gráficas interactivas:

Heatmap de jugadores (Aliados vs Rivales).

Trayectoria del balón.

Análisis de posesión.

##Videos
Demo completo (1:30 min): fase3_demo.mp4

Reel Instagram (30 seg): https://www.instagram.com/reel/DZyyykitWbV/?igsh=MTdtaWpndG9kZTZhbQ==

## 🎙️ Breve explicación del enfoque utilizado
El enfoque combina tres componentes principales:  
- **YOLOv8 + ByteTrack** para detectar y seguir a los robots y al balón en cada frame del partido.  
- **SAM3** como modelo de segmentación, que recibe las cajas de YOLO como prompts y permite separar con precisión el campo, los aliados y los rivales.  
- **Módulos de análisis estadístico** que calculan métricas de posesión, generan mapas de calor, trazan la trayectoria del balón y detectan automáticamente los goles.  
 
⚙️ Configuración
Parámetros ajustables:

ESCALA_PX_CM → Escala de conversión de centímetros a píxeles.

umbral → Tolerancia en píxeles para detección de goles.

min_gap → Frames mínimos entre goles para evitar duplicados.
## Notas
El sistema depende de la calidad del archivo detecciones_yolo.csv.

Las coordenadas de las porterías (goal_sup, goal_inf) deben ajustarse según el campo y la calibración inicial.

Se recomienda usar YOLOv8 para generar las detecciones.

##Licencia y Créditos
Proyecto bajo licencia MIT.

Dependencias: YOLO (Ultralytics), SAM3 (Meta), ByteTrack, Supervision, OpenCV, Seaborn, Matplotlib.

Créditos: Equipo FutBotMX – Alejandra.


