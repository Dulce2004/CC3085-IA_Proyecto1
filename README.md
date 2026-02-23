# Proyecto 1 - IA

**Curso:** CC3085 - Inteligencia Artificial  
- Dulce Ambrosio - 231143 
- Daniel Chet - 231177 
- Gadiel Ocaña - 231270 

---

## Descripción del Proyecto

Implementación de algoritmos de búsqueda informada y no informada para navegación en laberintos, integrado con una red neuronal multicapa entrenada desde cero para clasificación de terrenos y cálculo de costos dinámicos.

---

## Características Principales

### Task 1: Búsqueda en Laberintos

#### 1.1 Discretización del Mundo
- Conversión de imagen .bmp a matriz discreta (grid)
- Clasificación de tiles: Pared, Inicio, Meta, Espacio Libre
- Agrupación de píxeles por tamaño de baldosa configurable

#### 1.2 Búsqueda No Informada
- **BFS (Breadth-First Search)**: Garantiza el camino con menor número de pasos
- **DFS (Depth-First Search)**: Exploración en profundidad
- Implementación con Graph Search (conjunto de visitados)

#### 1.3 Búsqueda Informada
- **(A\*)**: Algoritmo heurístico con Distancia Manhattan
- Optimización considerando costo acumulado g(n) + estimación heurística h(n)
- Heurística admisible y consistente

### Task 2: Red Neuronal 

#### 2.1 Entrenamiento desde Cero
- **Arquitectura MLP**: 
  - Entrada: 3 neuronas (R, G, B normalizados)
  - Capa oculta: 16 neuronas + ReLU
  - Salida: 11 clases + Softmax
- **Backpropagation manual** con Gradient Descent
- Función de pérdida: Cross-Entropy
- Dataset: final_data_colors.csv

#### 2.2 Integración con A*
- Clasificación en tiempo real de terrenos según color RGB
- Mapeo Color - Costo:
  - Gris (Pavimento): Costo 1
  - Verde (Grama): Costo 3
  - Amarillo (Arena): Costo 5
  - Azul (Agua): Costo 50
- A* considera tanto distancia como dificultad del terreno

---



## Estructura del Proyecto

```
CC3085-IA_Proyecto1/
│
├── Proyecto1.ipynb          # Notebook principal con implementación
├── final_data_colors.csv    # Dataset de colores RGB etiquetados
├── turing.bmp               # Imagen del laberinto
└── README.md                # Este archivo
```

---

## Cómo Ejecutar

1. **Requisitos previos:**
   ```bash
   pip install numpy pandas matplotlib pillow scikit-learn
   ```

2. **Abrir el notebook:**
   ```bash
   jupyter notebook Proyecto1.ipynb
   ```

3. **Ejecutar las celdas secuencialmente:**
   - Task 1.1: Cargar y discretizar el laberinto
   - Task 1.2: Probar BFS y DFS
   - Task 1.3: Ejecutar A* con costo uniforme
   - Task 2.1: Entrenar red neuronal
   - Task 2.2: Ejecutar A* con costos dinámicos

---

## Resultados Destacados

### Comparación de Algoritmos
- **BFS**: Camino más corto garantizado (costo uniforme)
- **DFS**: Exploración completa pero no óptima
- **A\***: Óptimo y eficiente (menos nodos explorados que BFS/DFS)

### Red Neuronal
- Precisión en entrenamiento: >95%
- Precisión en prueba: >90%
- Clasificación de 11 tipos de terreno

### A* con Costos Dinámicos
- Evita terrenos costosos (agua) cuando es posible
- Optimiza costo total vs distancia mínima
- Demostrado en laberinto complejo de 100×100

---

## Experimentos Demo

El proyecto incluye dos experimentos visuales:
1. **Demo Básico**: Laberinto 30×30 con dos rutas (corta costosa vs larga barata)
2. **Laberinto con mayor dificultad**: Grid 100×100 con múltiples tipos de terreno y obstáculos complejos

