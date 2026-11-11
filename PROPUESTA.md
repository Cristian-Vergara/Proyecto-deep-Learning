# Propuesta del proyecto final · INFB6083 Deep Learning 2026-II

## 1. Identificación
**Título tentativo:** Agrupamiento de morfologías del polvo interestelar en mapas Herschel SPIRE mediante autoencoder y transfer learning
**Autor:** Cristian Ignacio Vergara Campos
**Repositorio:** https://github.com/Cristian-Vergara/Proyecto-deep-Learning

## 2. Problema y para quién
Los archivos de datos astronómicos (como el Herschel Science Archive) necesitan catalogar y buscar morfologías de polvo en miles de recortes de mapas infrarrojos. Hoy dependen de etiquetas manuales o de catálogos incompletos. El modelo agrupa recortes parecidos sin etiquetas para apoyar esa catalogación.

## 3. Tarea
**Entrada:** tile de 64×64 px (1 canal, unos 6,4 minutos de arco) de un mapa SPIRE 250 µm. **Salida:** grupo (cluster) del tile. **Tipo:** aprendizaje no supervisado (agrupamiento).

## 4. Corpus
Herschel Gould Belt Survey, imágenes SPIRE 250 µm alojadas en IRSA (NASA/IPAC; André et al. 2010, DOI 10.26131/IRSA72): 11 mapas de 10 nubes. Datos públicos; licencia exacta por confirmar. Unos 190 MB y 9 072 tiles sin NaN ni solapamiento: bajo el techo de 500 MB y 50 000 ejemplos, sin recorte. Partición por nube para evitar fuga: entrenamiento con 6 nubes (6 939 tiles), validación con Pipe e IC 5146 (731) y evaluación con Perseus y Lupus (1 402). Los datos se descargan por código y no se suben al repositorio.

## 5. Escalera de modelos
Todavía no lo sé; mi plan de momento, sobre la misma partición: (1) PCA + K-means; (2) autoencoder convolucional + K-means; (3) ResNet-18 preentrenada en ImageNet con transfer learning + K-means. Qué capas congelar y cuáles ajustar queda por definir.

## 6. Métricas
**Efectividad:** Silhouette y, sobre un subconjunto de tiles de evaluación etiquetado a mano (etiquetado pendiente), ARI y NMI; las etiquetas solo se usan para evaluar. **Eficiencia:** tiempo de entrenamiento, latencia por tile y memoria.

## 7. Visualización interactiva de resultados
Reporte HTML autocontenido, en el formato del profesor y sin necesidad de red: imágenes de los datos, mapa 2D de los tiles por grupo, galería de tiles por grupo y tabla comparativa de los tres modelos.

## 8. Recursos de cómputo y de IA
**Plan A:** MacBook Air con Apple M4 y 16 GB (PyTorch con MPS), local en VS Code. **Plan B:** PC con Ryzen 5 9600X, 32 GB de RAM y Radeon RX 7700 XT (ROCm según el sistema operativo; si no, CPU). No usaré Colab. **IA:** Claude Code y Codex.

## 9. Riesgo principal y plan B
Los grupos pueden reflejar ruido o brillo y no morfologías reales, y el modelo propuesto podría no superar a PCA. Plan B: reportar la comparación tal cual y contrastar los grupos con el subconjunto etiquetado.
