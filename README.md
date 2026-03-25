# ColonScan — Proyecto Conjunto

Este repositorio actúa como punto de entrada para el proyecto ColonScan, que está compuesto por dos repositorios independientes pero complementarios:

- API/Microservicio de ML: Detección de pólipos en imágenes (FastAPI y modelo de Vision Transformer).
- Aplicación Web: Interfaz Django para gestión de pacientes y visualización de resultados.

Enlaces a los repositorios principales:

- [API / ML](https://github.com/DavidAlejandroMedina/ColonScan-API-ML.git)
- [Aplicación Web (Django)](https://github.com/DavidAlejandroMedina/ColonScan-App-Web.git)

---

## ColonScan-API-ML
	- Microservicio en FastAPI para analizar series DICOM y detectar pólipos usando un modelo Vision Transformer (ViT).
	- Endpoints principales: `/`, `/api/v1/health`, `/api/v1/analyze`, `/api/v1/model-info`.
	- Incluye scripts para conversión/optimización del modelo Keras y configuración para Docker (imagen CPU).
	- Archivos importantes: `app/main.py`, `app/models/vit_model.py`, `models/best_polyp_vit_improved.keras`, `polyp_model_config.json`.

## ColonScan-App-Web
	- Aplicación web desarrollada con Django (MVT) para gestión de pacientes, carga de archivos con imágenes DICOM y envío de estos al microservicio ML.
	- Contiene panel de administración, seed data, y configuración para Docker y PostgreSQL.
	- Archivos importantes: `manage.py`, `colonscan_project/settings.py`, `medical_service/models.py`, `templates/`.

---

## Diagrama general

```mermaid
flowchart TB
	A[Usuario / Médico] -->|Sube DICOM| B[App-Web (Django)]
	B -->|Llama API ML (HTTP)| C[API-ML (FastAPI)]
	C -->|Procesa con ViT| D[Modelo ViT / TF]
	D -->|Resultados| C
	C -->|Respuesta JSON| B
	B -->|Muestra Reporte| A
	subgraph Infra
		C
		D
	end
```

Uso recomendado

- Clona los repositorios por separado y sigue las instrucciones en cada `README.md` para levantar servicios (Docker o local).
- Primero inicia el `ColonScan-API-ML` (puerto por defecto `8001`) para que la `App-Web` pueda enviarle series DICOM.


Archivo modificado: [README.md](README.md)
