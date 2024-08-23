
#### Si los datos de calidad de código provenientes de SonarQube muestran inconsistencias  cuando se visualizan en Kibana, ¿ que factores en el API  de FastAPI podría investigar para identificar la causa del problema?

***Respuesta: 
Podría ser necesario revisar la transformación de datos en FastAPI para asegurar que no se estén perdiendo o alterando datos críticos .
También puede ser un problema en como los datos se están estructurando o indexando antes de enviarse a Elasticsearch. Además, revisar la lógica que determina que métricas se seleccionan de SonarQube para asegurarse que todas las métricas necesarias se estén enviando correctamente. 


#### Kibana muestra los datos desactualizados de SonarQube. 
#### ¿ Qué podría inferir sobre el manejo de las solicitudes y respuestas en el API de FastApi ?

***Respuesta:
Esto podría indicar que el API de FastApi no está solicitando o actualizando lo datos de SonarQube de manera adecuada o con la frecuencia necesaria. Podría haber  un problema con la cache de fastApi , donde se estan sirviendo datos antiguos en un lugar de solicitar información actualizada.  