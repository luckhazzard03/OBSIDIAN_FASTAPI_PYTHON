
En la siguiente parte debemos explicar la configuración realizada en el entorno de desarrollo 

Backend 

El backend es construido plenamente con una arquitectura modularizada buscando dividir las responsabilidades entre adaptador, rutas, servicios y procesadores. 

Los endpoint del proyecto están dividido en seis los cuales son: 

## - Sonarqube – info 
    

El cual nos retornara las project key de los proyectos escaneados de Sonarqube, información del estado y salud del sistema, por último, detalles del sistema. 

## - Dashboard 
    

Los end points dentro de dashboard contienen la utilización de varios servicios para alimentar los índices de elastic search con la información que requiere el dashboard. Se cuenta con cuatro dashboards los cuales son General y otros tres que son los atributos de calidad evaluados por Sonarqube  

## - General 
    

Los end points del grupo “General” representan la recuperación de información general como seria la deuda técnica, numero de problemas por atributo de calidad y la deuda técnica del proyecto. 

## - Seguridad 
    

Los end points del grupo “Seguridad” representan la recuperación de información sobre los problemas de seguridad por impacto, el número de hotspots y el porcentaje de la cobertura de las pruebas. 

## - Mantenibilidad 
    

Los end points del grupo “Mantenibilidad” representan la recuperación de la información sobre los problemas de mantenibilidad por impacto, porcentaje de líneas duplicadas y code smells. 

## - Fiabilidad 
    

Los end points del grupo “Fiabilidad” representan la recuperación de la información sobre los problemas de fiabilidad por impacto, bugs y complejidad ciclomatica. 

Para la recuperación de las métricas de sonarqube se crea un end point el cual realiza la llamada a un método factory que retorna la instancia del adaptador que ayuda a que el servicio realice la petición autenticada a los end points de sonarqube, seguido de obtener la información se pasa por un procesador que ajusta la información obtenida a una respuesta adecuada y menos pesada.