# AlphaFold & PyMOL - Análisis de Proteínas


Repositorio en GitHub: [https://github.com/giselabcruz/alphafold-pymol](https://github.com/giselabcruz/alphafold-pymol)
---

Este repositorio contiene ejercicios prácticos para el análisis de estructuras de proteínas utilizando **AlphaFold** y **PyMOL**, enfocándose en la comparación entre predicciones computacionales y estructuras experimentales.

## Proteína de Estudio: Cytochrome c (CYCS)

<div align="center">
  <img src="cytochrome_c_structure.png" width="500">
  <p><i>Estructura 3D del Cytochrome c mostrando α-hélices y el grupo heme</i></p>
</div>

>*Imagen generada con Gemini 3 Pro Image*

### Información General

| Propiedad | Valor |
|-----------|-------|
| **Nombre** | Cytochrome c (CYCS) |
| **UniProt ID** | [P99999](https://www.uniprot.org/uniprotkb/P99999) |
| **PDB Experimental** | [1HRC](https://www.rcsb.org/structure/1HRC) |
| **Longitud** | 105 aminoácidos |
| **Peso Molecular** | ~12 kDa |
| **Organismo** | *Homo sapiens* |
| **Localización** | Espacio intermembrana mitocondrial |
| **Cofactor** | Grupo heme c |

### Función Biológica

<div align="center">
  <img src="cytochrome_c_function.png" width="500">
  <p><i>Función del Cytochrome c en la cadena de transporte de electrones</i></p>
</div>

>*Imagen generada con Gemini 3 Pro Image*

**Cytochrome c** desempeña dos funciones críticas:

1. **⚡ Cadena de transporte de electrones**: Transfiere electrones entre el Complejo III (citocromo bc1) y el Complejo IV (citocromo c oxidasa) en la mitocondria, siendo esencial para la producción de ATP.

2. **💀 Señalización de apoptosis**: Cuando se libera al citosol, activa la cascada de caspasas que conduce a la muerte celular programada.

## Contenido del Repositorio

```
alphafold-pymol/
├── alphafold-exercises.ipynb    principal con ejercicios completos
├── images/                       
│   ├── cytochrome_c_structure.png
│   ├── cytochrome_c_function.png
│   └── visualization_web_alphafold.png
├── fasta/                        
│   └── P99999.fasta             
├── pdb/                          
│   └── AF-P99999-F1-model_v6.pdb
├── pdb_experimental/             
│   └── 1HRC.pdb                 
├── pdb_predicted/                
│   └── alphafold_aligned_to_1HRC.pdb
├── requirements.txt              
└── README.md                     
```

## Especificaciones Técnicas

### Archivos Generados Durante los Ejercicios

| Archivo | Descripción | Tamaño | Fuente |
|---------|-------------|--------|--------|
| `P99999.fasta` | Secuencia de aminoácidos | 105 AA | UniProt |
| `AF-P99999-F1-model_v6.pdb` | Predicción AlphaFold | ~825 átomos | AlphaFold DB |
| `1HRC.pdb` | Estructura experimental | ~827 átomos | RCSB PDB |
| `alphafold_aligned_to_1HRC.pdb` | Estructura alineada | ~825 átomos | Generado |

### Herramientas Utilizadas

- **Biopython:** Manejo de secuencias y estructuras PDB
- **py3Dmol:** Visualización 3D interactiva
- **NumPy:** Cálculos numéricos y matrices de distancias
- **Matplotlib:** Generación de gráficos de pLDDT
- **Bio.PDB.Superimposer:** Alineamiento estructural y cálculo de RMSD

## Objetivos del Proyecto

Este proyecto tiene como objetivo:

- Descargar y analizar secuencias de proteínas desde UniProt
- Obtener predicciones estructurales de AlphaFold
- Visualizar estructuras 3D con py3Dmol y PyMOL
- Analizar la confianza de predicción mediante valores pLDDT
- Comparar predicciones con estructuras experimentales (RMSD)
- Generar mapas de distancias internas
- Identificar regiones flexibles y sitios activos

## Ejercicios Incluidos y Resultados

### Bloque 1: Descarga de Secuencia desde UniProt
**Objetivo:** Obtención de la secuencia FASTA y análisis de anotaciones biológicas.

**Resultados obtenidos:**
- **Longitud de la secuencia:** 105 aminoácidos
- **Primeros 20 AA:** `MGDVEKGKKIFIMKCSQCHT`
- **Secuencia completa:**
  ```
  MGDVEKGKKIFIMKCSQCHTVEKGGKHKTGPNLHGLFGRKTGQAPGYSYTAANKNKGIIWGEDTLMEYLENPKKYIPGTKMIFVGIKKKEERADLIAYLKKATNE
  ```

**Datos curiosos descubiertos:**
- Es una proteína altamente conservada evolutivamente
- Su nombre significa "color celular" (*cyto* + *chroma*) debido al hierro que le da color rojo
- Es extremadamente resistente al calor y al ácido
- Funciona como "repuesto universal" entre especies

---

### Bloque 2: Descarga del Modelo AlphaFold
**Objetivo:** Descarga y visualización de la estructura predicha por AlphaFold.

**Resultados:**
- Modelo descargado: `AF-P99999-F1-model_v6.pdb`
- Visualización 3D interactiva con py3Dmol
- La estructura muestra claramente las α-hélices características
- El grupo heme está correctamente posicionado

---

### Bloque 3: Extracción de pLDDT
**Objetivo:** Análisis de valores de confianza (pLDDT) desde el archivo PDB.

**Estadísticas de pLDDT:**
- **pLDDT medio:** 97.25
- **pLDDT mínimo:** 75.75 (residuo 1, Met inicial)
- **pLDDT máximo:** 98.88 (residuo 19, His)
- **Desviación estándar:** 3.89

**Distribución de confianza:**
- Residuos con pLDDT > 90 (muy alta confianza): 104 de 105 (99.0%)
- Residuos con pLDDT 70-90 (alta confianza): 1 de 105 (1.0%)
- Residuos con pLDDT < 70 (baja confianza): 0 de 105 (0.0%)

---

### Bloque 4: Gráfico de pLDDT por Residuo
**Objetivo:** Visualización de la confianza de predicción a lo largo de la secuencia.

**Observaciones del gráfico:**
- La mayoría de los residuos muestran pLDDT > 95
- Ligera disminución en los extremos N y C-terminal
- Región central (residuos 20-90) con confianza extremadamente alta (>98)
- El Loop Ω (residuos 70-85) mantiene alta confianza a pesar de ser flexible

---

### Bloque 5: Colorear por pLDDT
**Objetivo:** Representación 3D con esquema de colores según confianza.

**Esquema de colores aplicado:**
- **Azul:** pLDDT > 90 (muy alta confianza) - 104 residuos
- **Cyan:** pLDDT 70-90 (alta confianza) - 1 residuo
- **Amarillo:** pLDDT 50-70 (confianza media) - 0 residuos
- **Naranja:** pLDDT < 50 (baja confianza) - 0 residuos

**Resultado:** La visualización muestra una estructura predominantemente azul, indicando predicción de altísima calidad.

---

### Bloque 6: Comparación con Estructura Experimental
**Objetivo:** Cálculo de RMSD entre AlphaFold y estructura experimental (1HRC).

**Resultados del alineamiento:**
- **Número de residuos alineados:** 104 (de 105 totales)
- **RMSD Cα:** **0.33 Å** ⭐
- **Interpretación:** RMSD < 1 Å indica predicción **EXCELENTE**
  - RMSD < 1 Å: Predicción casi perfecta
  - RMSD 1-2 Å: Predicción muy buena
  - RMSD 2-3 Å: Predicción aceptable
  - RMSD > 3 Å: Predicción con desviaciones significativas

**Conclusión:** AlphaFold predijo la estructura del Cytochrome c con una precisión excepcional, prácticamente idéntica a la estructura experimental determinada por cristalografía de rayos X.

---

### Bloque 7: Mapa de Distancias CA–CA
**Objetivo:** Generación de mapa de calor de distancias entre átomos Cα.

**Análisis del mapa:**
- Matriz de distancias 105×105 calculada
- Patrón diagonal característico de estructura compacta
- Identificación de regiones de contacto entre hélices
- Visualización de la topología del plegamiento

## Aspectos Interesantes del Cytochrome c

| Característica | Descripción | Relevancia para AlphaFold |
|----------------|-------------|---------------------------|
| **Sitio activo** | Grupo heme unido a Cys14 y Cys17 | ¿Predice correctamente la geometría? |
| **Ligandos del hierro** | His18 y Met80 | ¿Identifica residuos clave? |
| **Loop Ω** | Residuos 70-85 (región flexible) | ¿Captura la flexibilidad? |
| **Conservación evolutiva** | Altamente conservada | Excelente para estudios comparativos |

## Configuración del Entorno y Ejecución

### Requisitos del Sistema
- Python 3.9 o superior
- pip (gestor de paquetes de Python)
- Jupyter Notebook (opcional, para ejecutar el notebook)


### Ejecución de Ejercicios

#### Jupyter Notebook
```bash
source venv/bin/activate

jupyter notebook

```

### Solución de Problemas Comunes

- **Error "ModuleNotFoundError":** Asegúrate de tener activado el entorno virtual (`source venv/bin/activate`).
- **Error "externally-managed-environment":** Evita instalar paquetes globalmente; usa siempre el entorno virtual como se indica arriba.


## Resultados Obtenidos

### Métricas de Calidad de la Predicción

| Métrica | Valor Obtenido | Interpretación |
|---------|----------------|----------------|
| **pLDDT medio** | 97.25 | Excelente (>90) |
| **pLDDT mínimo** | 75.75 | Aceptable |
| **pLDDT máximo** | 98.88 | Excepcional |
| **RMSD Cα** | 0.33 Å | Casi perfecta |
| **Residuos alineados** | 104/105 | 99% |

### Interpretación de Resultados

**pLDDT medio de 97.25:** Supera ampliamente el umbral de 90 considerado "muy alta confianza"

**RMSD de 0.33 Å:** Valor excepcional que indica que la predicción de AlphaFold es prácticamente idéntica a la estructura experimental

**99% de residuos con pLDDT > 90:** Indica que casi toda la estructura fue predicha con muy alta confianza

### Regiones de Interés Identificadas

| Región | Residuos | pLDDT Promedio | Observaciones |
|--------|----------|----------------|---------------|
| **Core de α-hélices** | 20-90 | >98 | Predicción perfecta |
| **Loop Ω** | 70-85 | >95 | Alta confianza a pesar de flexibilidad |
| **N-terminal** | 1-5 | ~80 | Menor confianza (típico en extremos) |
| **C-terminal** | 100-105 | ~90 | Buena confianza |
| **Sitio de unión al heme** | 14-18 | >98 | Geometría correctamente predicha |

## Hallazgos Clave

### 1. Precisión Excepcional de AlphaFold
El RMSD de **0.33 Å** demuestra que AlphaFold predijo la estructura del Cytochrome c con una precisión extraordinaria, comparable a la resolución de estructuras experimentales de alta calidad.

### 2. Conservación Estructural
La alta confianza en la predicción (pLDDT medio de 97.25) refleja la fuerte conservación evolutiva de esta proteína, que mantiene su estructura prácticamente idéntica a través de millones de años de evolución.

### 3. Predicción Correcta del Sitio Activo
AlphaFold identificó correctamente:
- La geometría del grupo heme unido a **Cys14** y **Cys17**
- Los ligandos del hierro: **His18** y **Met80**
- La orientación espacial necesaria para la transferencia de electrones

### 4. Captura de Flexibilidad
A pesar de que el **Loop Ω** (residuos 70-85) es una región conocida por su flexibilidad, AlphaFold mantuvo una alta confianza (>95), sugiriendo que esta región tiene una conformación preferida bien definida.

### 5. Validación de AlphaFold
Este análisis demuestra que AlphaFold es capaz de predecir con precisión atómica estructuras de proteínas pequeñas y altamente conservadas, validando su utilidad como herramienta de predicción estructural.

---

