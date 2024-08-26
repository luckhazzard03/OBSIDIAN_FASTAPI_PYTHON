
#### Diapositiva 11
![[Pasted image 20240826163202.png]]

#### Diapositiva 17
Con la experiencia en recuperación y procesamiento de datos de Sonarqube buscaremos realizar la entrega de informes inferenciales sobre los históricos de los repositorios en diferentes periodos de tiempo.


### 1. **Objetivo**

El objetivo es crear informes que proporcionen una visión detallada e inferencial sobre la evolución de los repositorios de código. Estos informes pueden incluir métricas como la cantidad de errores, la cobertura de pruebas y otros indicadores de calidad, desglosados por diferentes periodos de tiempo.

### 3. **Pasos para la Entrega de Informes Inferenciales**

#### 3.1 **Recuperación de Datos**

1. **Conectar con la API de SonarQube**:  Se utiliza la API de SonarQube para recuperar datos históricos de los repositorios. SonarQube ofrece varios endpoints API que  permiten acceder a la información de calidad del código. Para autenticar,  se usa un token de API proporcionado por SonarQube.
    
2. **Ejemplo de Endpoint API**:
    
    - Para obtener métricas históricas, se puede usar el endpoint `/api/measures/search_history`.

#### 3.2 **Procesamiento de Datos**

1. **Transformar los Datos**: Una vez que obtienen los datos, deben ser transformarlos en un formato que sea fácil de analizar y visualizar. Esto puede implicar limpiar los datos, calcular promedios o tendencias, y agrupar los datos por diferentes periodos de tiempo.

**Ejemplo de Procesamiento**:

- **Agregación de Métricas**: Sumarizar las métricas por mes o trimestre.
- **Cálculo de Tendencias**: Determinar cómo las métricas han cambiado con el tiempo.

#### 3.3 **Generación de Informes**

1. **Crear Informes**: Usar herramientas de visualización de datos para crear informes visuales. Puedes usar bibliotecas de Python como Matplotlib, Seaborn, o herramientas de informes como Jupyter Notebooks.
    
2. **Ejemplo de Visualización**:
    
    - **Gráficos de Tendencias**: Mostrar cómo las métricas de calidad han cambiado a lo largo del tiempo.
    - **Comparaciones**: Comparar diferentes repositorios o diferentes periodos de tiempo.

#### 3.4 **Entrega de Informes**

1. **Formato de Entrega**: Los informes pueden ser entregados en varios formatos, como PDF, HTML, o directamente en una interfaz web. Esto depende de las necesidades del equipo o del cliente.
    
2. **Automatización**: Puedes automatizar la generación y entrega de estos informes usando herramientas de programación y scripting para que se generen y envíen regularmente.


### 4. **Resumen**

- **Recuperación de Datos**: Usa la API de SonarQube para obtener datos históricos.
- **Procesamiento**: Limpia y transforma los datos para el análisis.
- **Generación de Informes**: Utiliza herramientas de visualización para crear informes gráficos.
- **Entrega**: Presenta los informes en un formato adecuado y considera automatizar el proceso.
-
