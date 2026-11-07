# PreEntrega 1 — Clasificador Iris en PyTorch

**Autor:** José Ignacio Valbuena  
**Curso:** Data Science III  
**Comisión:** 102200

Pipeline base para clasificar tres especies de Iris a partir de cuatro medidas. Implementa un MLP pequeño,
entrenamiento explícito con autograd y Adam, validación separada y seguimiento por época.

## Contenido

- `notebooks/PreEntrega1_PyTorch_Iris.ipynb`: notebook ejecutado, con comentarios breves y resultados.
- `data/iris.csv`: copia de las 150 observaciones.
- `results/historial.csv`: pérdida y Accuracy por cada época.
- `results/curvas_aprendizaje.png`: curvas de entrenamiento y validación.
- `results/resumen.csv`: resultados antes y después de entrenar.
- `results/experimento.json`: versiones, configuración y métricas finales.
- `results/preparacion.json`: índices de partición y parámetros del estandarizador.
- `requirements.txt`: versiones de las dependencias directas utilizadas.
- `VERIFICACION.md`: lista de comprobación de requisitos y estado de la entrega.

## Ejecución local

Se verificó en Python 3.12.14 con PyTorch 2.15.0+cpu y dispositivo cpu.
Crear un entorno virtual con Python 3.12 y ejecutar desde la raíz del proyecto:

```bash
python -m venv .venv
```

Activación en Windows PowerShell: `.venv\Scripts\Activate.ps1`.
Activación en macOS/Linux: `source .venv/bin/activate`.

```bash
python -m pip install -r requirements.txt
python -m ipykernel install --user --name preentrega1 --display-name "Python (PreEntrega1)"
```

Abrir el notebook con VS Code/Jupyter, seleccionar ese kernel y ejecutar todas las celdas en orden.
También puede subirse el notebook a Google Colab y ejecutar todas sus celdas; crea las carpetas necesarias.
Colab tiene sus propias versiones, por lo que debe revisarse la versión impresa en la primera sección.
No se necesita descargar Iris ni contar con GPU. El código detecta CUDA, MPS o CPU automáticamente.
La ejecución regenera los archivos de datos y resultados.

## Diseño del experimento

- División estratificada 80/20: 120 ejemplos de entrenamiento y 30 de validación.
- Estandarización ajustada solo sobre entrenamiento para evitar filtración de información.
- MLP: Linear(4, 8), ReLU, Linear(8, 3); 67 parámetros entrenables.
- Salidas en logits, pérdida CrossEntropyLoss y etiquetas enteras 0, 1 y 2.
- Adam, **learning rate 0.01**, lotes de 16, 100 épocas, semilla 42.
- Learning rate y épocas son decisiones iniciales fijas para esta prueba técnica, sin búsqueda de hiperparámetros.
- Cada época limpia gradientes, realiza forward, calcula pérdida, ejecuta backward y actualiza los pesos.
- Validación con eval() y no_grad(), sin actualizaciones de parámetros.
- Las métricas de ambos conjuntos se calculan al finalizar cada época usando el mismo estado del modelo.
- La pérdida se promedia por observación, no por lote. Se reporta la última época.

## Resultados verificados

| Métrica | Entrenamiento | Validación |
|---|---:|---:|
| Pérdida inicial | 1.1529 | 1.1489 |
| Pérdida final | 0.0401 | 0.0663 |
| Accuracy final | 98.33% | 96.67% |

La pérdida final es menor que la inicial en ambos conjuntos, lo que indica aprendizaje en este experimento.
Las curvas muestran un descenso de ambas pérdidas y estabilización en valores bajos, sin subida sostenida de la pérdida de validación. No se observa sobreajuste marcado en esta ejecución; los pequeños saltos de Accuracy son compatibles con el tamaño reducido de la validación.
La validación es pequeña: una flor equivale a 3,33 puntos porcentuales de Accuracy.
Los resultados no representan una evaluación final independiente ni garantizan desempeño sobre otras poblaciones.
Se conserva el Iris original, incluidas las medidas repetidas, porque no hay identificadores que permitan
atribuirlas a una duplicación de la misma flor. Una sola partición no estima toda la variabilidad.
Las semillas facilitan repetir el experimento, aunque versiones y dispositivos pueden producir diferencias.

## Comprobaciones realizadas

Notebook ejecutado de principio a fin; 100 épocas sin errores; particiones disjuntas; dimensiones y tipos correctos;
métricas finitas y Accuracy entre 0 y 1; pesos modificados por entrenamiento y sin cambios durante evaluación.
La detección de dispositivos está implementada; esta entrega se ejecutó en CPU.

## Relación con la evaluación

| Criterio | Peso | Evidencia |
|---|---:|---|
| Organización del repositorio | 20 % | Carpetas, notebook, requirements y README |
| PyTorch y dispositivo | 15 % | Configuración y selección automática |
| Arquitectura | 15 % | nn.Module y dimensiones verificadas |
| Entrenamiento | 35 % | zero_grad, forward, loss, backward, Adam.step |
| Validación | 10 % | Función separada, loss y Accuracy por época |
| README | 5 % | Versiones, learning rate, ejecución e interpretación |

## Publicación y entrega

Subir el contenido de esta carpeta a un repositorio de GitHub o GitLab y entregar su enlace.
No se ha publicado un repositorio remoto desde este paquete. Usar mensajes de commit descriptivos,
por ejemplo: `Implementar pipeline Iris con entrenamiento y validación en PyTorch`.
Antes de enviar, comprobar que el repositorio contiene el notebook con sus salidas, README y requirements.
La carpeta `data/` forma parte de la estructura sugerida; los resultados se incluyen como evidencia.

## Fuentes

- Consigna: Pre Entrega 1 — Pipeline de entrenamiento, validación y clasificador base.
- Data Science III, módulo 1: perceptrón, redes neuronales, backpropagation, PyTorch, autograd y Adam.
- Iris de scikit-learn: procedencia y descripción en `sklearn.datasets.load_iris().DESCR`.
