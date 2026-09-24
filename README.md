# TP15 Semgrep como SAST

## Paso 1: Probar Semgrep localmente
Se creó un entorno virtual (.venv) en Python para instalar Semgrep aisladamente y no mezclar dependencias del sistema.

## Paso 2: Creación del Workflow
Se creó .github/workflows/semgrep.yml sin modificar ni eliminar cicd.yml
El archivo contiene:
•	Preparación del entorno
•	Escaneo Multilenguaje
•	Reporte ($GITHUB_STEP_SUMMARY)
•	Almacenamiento de Artefactos
•	Integración SARIF
•	Andon Cord

## Paso 3: Integración con la pestaña "Security" de GitHub
En GitHub se exportan los hallazgos en formato SARIF para visualizarlos en Security > Code scanning alerts.
Para habilitar esta funcionalidad, se incorporaron los pasos de generación y carga del reporte SARIF dentro del archivo .github/workflows/semgrep.yml:

## Paso 4: Configurar la estrategia del "Andon Cord"
Se configuró la guardia estricta (Andon Cord) utilizando la opción --error. Al detectar cualquier riesgo crítico, el job se interrumpe de inmediato, bloqueando el pipeline y previniendo la integración del código afectado.

## Paso 5: Ejecución y Prueba de Fallo Controlado
Run Exitoso: Subida a la rama principal con generación de artefactos y resumen de auditoría en verde.
Prueba Andon Cord: Se inyectó temporalmente un fallo crítico de inyección de comandos (os.system) en el backend, verificando que el pipeline fallara y detuviera la integración. 

## Entregables
github/workflows/semgrep.yml versionado.
Captura o enlace del run exitoso.
semgrep-report descargado desde el run.
Captura del $GITHUB_STEP_SUMMARY.
Evidencia de bloqueo por Andon Cord en falla controlada y posterior resolución.
