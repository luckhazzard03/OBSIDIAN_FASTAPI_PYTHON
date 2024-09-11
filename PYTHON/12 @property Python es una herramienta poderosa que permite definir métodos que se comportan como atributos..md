#Python #property
El decorador `@property` en Python es una herramienta poderosa que permite definir métodos que se comportan como atributos. Aquí tienes una explicación detallada:

1. **Definición básica:**  
    `@property` es un decorador incorporado en Python que se utiliza para definir un método como una propiedad de una clase.
2. **Funcionalidad:**
    
    - Convierte un método de una clase en un atributo de solo lectura.
    - Permite acceder a un método como si fuera un atributo, sin necesidad de usar paréntesis.
    
3. **Ventajas:**
    
    - Encapsulación: Oculta la implementación interna de un atributo.
    - Control de acceso: Permite definir lógica personalizada para obtener, establecer o eliminar un valor.
    - Retrocompatibilidad: Facilita cambiar la implementación de un atributo sin modificar la interfaz pública de la clase.
    
4. **Uso básico:**python
    
    ```c
    class Ejemplo:
         def __init__(self, valor):
              self._valor = valor    
              
		 @property 
		 def valor(self):
		     return self._valor
		     ```
    
5. **Getters, Setters y Deleters:**
    
    - `@property`: Define el getter (método para obtener el valor).
    - `@atributo.setter`: Define el setter (método para establecer el valor).
    - `@atributo.deleter`: Define el deleter (método para eliminar el valor).
    
6. **Ejemplo completo:**python
    
    ```c
    class Temperatura:
         def __init__(self, celsius):  
            self._celsius = celsius   
            
		@property  
		 def celsius(self): 
		     return self._celsius  
		     
		@celsius.setter 
		  def celsius(self, valor):     
		     if valor < -273.15:
		        raise ValueError("Temperatura por debajo del cero absoluto")        
		        self._celsius = valor
		
		@property 
		def fahrenheit(self):
		    return (self.celsius * 9/5) + 32
		    ```
    
7. **Beneficios:**
    
    - Validación de datos: Puedes añadir lógica de validación en el setter.
    - Cálculos sobre la marcha: Puedes realizar cálculos en el getter sin almacenar el resultado.
    - Lazy evaluation: Puedes retrasar cálculos costosos hasta que sean necesarios.
    
8. **Consideraciones:**
    
    - Uso moderado: No es necesario usar `@property` para todos los atributos, solo cuando necesites control adicional.
    - Rendimiento: El uso excesivo puede tener un pequeño impacto en el rendimiento comparado con atributos simples.
    

En resumen, `@property` es una herramienta que mejora la encapsulación y la flexibilidad en el diseño de clases en Python, permitiendo un control más fino sobre cómo se accede y modifica los atributos de una clase.