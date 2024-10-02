# Aprendizaje Automático para Visión por Computadora

## Descripción

Este repositorio contiene implementaciones prácticas realizadas durante el curso de **Aprendizaje Automático para Visión por Computadora** de la carrera de Licenciatura en Ciencias de la Computación. El proyecto se centra en técnicas avanzadas de visión por computadora y aprendizaje automático para la búsqueda y recuperación de imágenes, incluyendo verificación geométrica, matching de descriptores y reducción de dimensionalidad con PCA.

## Contenido del Proyecto

### Lab 2: Búsqueda y Recuperación de Imágenes

El laboratorio aborda los siguientes puntos clave:

1. **Verificación Geométrica**:
   - Matching entre descriptores utilizando SIFT.
   - Estimación de transformaciones afines mediante RANSAC.
   - Implementación desde cero de la estimación afín y RANSAC.

2. **PCA sobre Descriptores**:
   - Entrenamiento de un modelo PCA a partir de 100,000 descriptores aleatorios.
   - Proyección de descriptores locales.
   - Evaluación del impacto de la dimensionalidad (16, 32, 64) con y sin re-normalización L2.

3. **Evaluación de Scoring y Ranking**:
   - Análisis de la influencia del tamaño de la lista corta.
   - Modificación del esquema de scoring utilizando el kernel de intersección sobre vectores BoVW normalizados L1.
   - Extensión a kernels aditivos.

### Dataset

Se utiliza el dataset de Nister y Stewenius (2006) para la evaluación:

- **Referencia**: Nister, D., & Stewenius, H. (2006). *Scalable recognition with a vocabulary tree*. In CVPR.
- **Enlace al dataset**: [UKBench Dataset](http://vis.uky.edu/~stewe/ukbench/)

## Requisitos

Antes de ejecutar el proyecto, asegúrate de instalar las siguientes dependencias:

```bash
numpy
scipy
scikit-learn==0.17.1
scikit-image==0.12.3
opencv-python
multiprocessing==2.6.2.1
```

Puedes instalarlas utilizando:

```bash
pip install -r requirements.txt
```

## Instalación

1. **Clona el repositorio**:

   ```bash
   git clone https://github.com/marina-nh/Machine-Learning-for-Computer.git
   ```

2. **Navega al directorio del proyecto**:

   ```bash
   cd ml
   ```

3. **Configura el entorno** (opcional pero recomendado):

   - Crea un entorno virtual:

     ```bash
     python -m venv venv
     ```

   - Activa el entorno:

     - En Linux/Mac:

       ```bash
       source venv/bin/activate
       ```

     - En Windows:

       ```bash
       venv\Scripts\activate
       ```

4. **Instala las dependencias**:

   ```bash
   pip install -r requirements.txt
   ```

## Uso

### 1. Verificación Geométrica

Implementación de la función `geometric_consistency` en `lab2.py`:

- **Matching de features**: Se utilizan descriptores SIFT para encontrar correspondencias entre imágenes.
- **Estimación de transformación afín**: Utilizando RANSAC para filtrar correspondencias erróneas.
- **Cálculo de inliers**: Contabiliza el número de correspondencias que cumplen con la transformación estimada.

Ejemplo de uso:

```python
def geometric_consistency(feat1, feat2):
    kp1, desc1 = feat1['kp'], feat1['desc']
    kp2, desc2 = feat2['kp'], feat2['desc']
    # Implementación del matching y RANSAC
```

Para ejecutar la verificación geométrica:

```bash
python lab2.py
```

### 2. Aplicación de PCA

Reducir la dimensionalidad de los descriptores para optimizar el rendimiento.

- **Entrenamiento del modelo PCA**:

  ```python
  P, mu = pca_fit(samples)
  ```

- **Proyección de los descriptores**:

  ```python
  pca_samples = [pca_project(x, P, mu, k) for x in samples]  # k = 16, 32, 64
  ```

- **Re-normalización L2**:

  ```python
  pca_samples = [x / (np.linalg.norm(x) + epsilon) for x in pca_samples]
  ```

### 3. Evaluación y Scoring

Modificar el esquema de scoring para mejorar el ranking de imágenes.

- **Normalización L1**:

  ```python
  bovw_vectors = [x / np.sum(x) for x in bovw_vectors]
  ```

- **Kernel de intersección**:

  ```python
  def intersection_kernel(x, y):
      return np.sum(np.minimum(x, y))
  ```

## Evaluación del Rendimiento

Se utilizan las primeras imágenes de los 100 primeros objetos del dataset como queries.

- **Configuración**:

  En `lab2.py`, ajustar el número de queries:

  ```python
  N_QUERY = 100  # Modificar según sea necesario
  ```

- **Ejecución**:

  ```bash
  python lab2.py
  ```

- **Análisis de resultados**: Se evalúa la precisión y recall en función de las diferentes configuraciones implementadas.

## Estructura del Proyecto

- `lab2.py`: Script principal con las implementaciones del laboratorio.
- `pca.py`: Funciones para el entrenamiento y aplicación de PCA.
- `utils.py`: Funciones auxiliares (carga de datos, cálculo de features, etc.).
- `requirements.txt`: Lista de dependencias necesarias.
- `README.md`: Documentación del proyecto.
- `LICENSE`: Información sobre la licencia del proyecto.

## Resultados

Los resultados obtenidos demuestran mejoras en el rendimiento de la recuperación de imágenes al aplicar PCA y modificar el esquema de scoring. La implementación de la verificación geométrica reduce significativamente los falsos positivos en el matching de imágenes.

## Contribuciones

Las contribuciones son bienvenidas. Para reportar errores o proponer mejoras:

1. Abre un **Issue** en GitHub.
2. Envía un **Pull Request** con los cambios propuestos.

Por favor, sigue las pautas de estilo y asegúrate de que el código se ejecuta correctamente antes de enviar.

## Licencia

Este proyecto está licenciado bajo la [Licencia MIT](LICENSE).

## Agradecimientos

- **Institución**: Facultad de Matemática, Astronomía, Física y Computación, Universidad Nacional de Córdoba (UNC)
- **Referencia Principal**: Nister, D., & Stewenius, H. (2006). *Scalable recognition with a vocabulary tree*. In CVPR.

## Contacto

Para más información o consultas:

- **Autor**: [marina-nh](https://github.com/marina-nh)
- **Email**: [contact@marinanunez.tech](contact@marinanunez.tech)
