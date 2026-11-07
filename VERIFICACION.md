# Verificación de la PreEntrega 1

Autor: José Ignacio Valbuena · Data Science III · Comisión 102200.

| Comprobación | Estado | Evidencia |
|---|---|---|
| Nombre, curso y comisión | Correcto | Primera celda del notebook, README y experimento.json |
| Organización del proyecto (20 %) | Correcto en el paquete | data/, notebooks/, results/, README.md y requirements.txt |
| Entorno PyTorch y dispositivo (15 %) | Implementado; probado en CPU | Semillas, versiones y detección CUDA/MPS/CPU |
| Arquitectura base (15 %) | Correcto | nn.Module, 4 entradas, 8 neuronas, 3 logits; 67 parámetros |
| Entrenamiento y Adam (35 %) | Correcto | zero_grad, forward, pérdida, backward y optimizer.step |
| Validación (10 %) | Correcto | Función separada, eval y no_grad, pérdida y Accuracy |
| README (5 %) | Correcto | Versión de PyTorch, learning rate, ejecución e interpretación |
| Separación de datos | Correcto | 120 entrenamiento, 30 validación, estratificación e índices disjuntos |
| Prevención de filtración en escalado | Correcto | StandardScaler se ajusta solo con entrenamiento |
| Tipos y dimensiones | Correcto | float32, int64 y salida de tres clases |
| Métricas por época | Correcto | 100 registros completos en historial.csv |
| Ejecución completa | Correcto | 10 celdas de código ejecutadas sin errores |
| Actualización de pesos | Correcto | Se comprueba que cambien al entrenar y no al evaluar |
| Curvas y conclusiones | Correcto | Gráfico, resultados, interpretación y limitaciones |
| Voz de redacción | Unificada | Redacción impersonal: se guarda, se reserva, se registran |
| Dependencias | Registradas | requirements.txt con versiones directas utilizadas |
| Publicación y commits en GitHub/GitLab | Pendiente | Subir los archivos descomprimidos y utilizar un mensaje descriptivo |
| Entrega del enlace | Pendiente | Presentar el enlace del repositorio en la plataforma |

Resultado de la ejecución en CPU: Accuracy de entrenamiento 98,33 % y validación 96,67 % (29 de 30 flores).
Las pérdidas finales son 0,0401 y 0,0663, respectivamente.
Las rutas CUDA y MPS están implementadas, pero no se verificaron con hardware de esos tipos.
No se probó una instalación desde cero en otro sistema operativo.
La lista comprueba los requisitos observables; la calificación corresponde al docente.
