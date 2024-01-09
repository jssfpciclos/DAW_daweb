### **Conceptos**

  - FASTCGI

    FastCGI es un protocolo que permite la comunicación entre un servidor web y un programa externo, en este caso, el intérprete de PHP.

    La principal ventaja de FastCGI es su capacidad para mantener conexiones persistentes, lo que mejora el rendimiento al reducir la sobrecarga asociada con la creación de procesos para cada solicitud.

*   CGI

    CGI (Common Gateway Interface) es un protocolo estándar para ejecutar aplicaciones web externas a través de servidores web.

    CGI crea un nuevo proceso para cada solicitud, lo que puede generar una sobrecarga considerable en comparación con FastCGI.

    A pesar de su simplicidad, CGI ha sido en gran medida reemplazado por enfoques más eficientes como FastCGI y PHP-FPM.

<br>

**PHP-FPM** (FastCGI Process Manager) es una herramienta que permite a PHP **procesar peticiones web de forma más rápida y eficiente**. Funciona como un gestor de procesos FastCGI, que es un protocolo de comunicación entre el servidor web y PHP. Al usar PHP-FPM, es posible mejorar el desempeño de tu servidor, haciéndolo capaz de manejar un mayor número de peticiones simultaneas y reduciendo el tiempo de respuesta para el usuario final. En este artículo, exploraremos **cómo utilizar PHP-FPM en tu servidor y los beneficios que puede ofrecer para el rendimiento de tu sitio o aplicación web**. ¿Vamos? 

## **¿Qué es PHP-FPM?** 

En términos simples, **PHP-FPM** es una herramienta que **ayuda a que las páginas web en PHP sean más rápidas y eficientes**, permitiendo que más personas accedan al sitio web al mismo tiempo. Lo hace separando el procesamiento PHP del servidor web, lo que significa que el servidor web puede manejar más peticiones al mismo tiempo sin sobrecargar el sistema. 

Cuando se realiza una petición a una página PHP, el servidor web envía la petición a PHP-FPM, que a su vez inicia un proceso PHP separado para gestionar la petición. Esto significa que en lugar de que el servidor web gestione la petición y ejecute PHP en cada petición, PHP-FPM gestiona el proceso PHP por separado, **permitiendo al servidor web gestionar más peticiones en paralelo**. 

PHP-FPM también proporciona **recursos de administración de procesos**, como la posibilidad de ajustar el número de procesos PHP en ejecución en función de la carga del servidor y limitar el uso de recursos del servidor por proceso. 

##  **Cuándo usar o no usar PHP-FPM** 

No todos los servidores o sitios web se beneficiarán del uso de PHP-FPM, por lo que es importante entender los factores que influyen en su funcionamiento. Conoce a continuación los escenarios: 

### **Cuando usar PHP-FPM** 

Situaciones en las que es interesante habilitar PHP FPM: 

*   **Cuando el servidor aloja un gran número de sitios o aplicaciones web:** PHP FPM es una opción interesante para hacer frente a la sobrecarga de varios sitios web y aplicaciones que compiten por los recursos del servidor. Con PHP FPM, es posible administrar los recursos de forma más eficiente e garantizar que cada sitio web tenga su parte justa de los recursos necesarios. 
*   **Cuando los sitios web alojados tienen mucho tráfico y requieren un alto rendimiento del servidor:** PHP FPM es capaz de procesar más peticiones simultáneamente que otros métodos de procesamiento PHP, por lo que es ideal para sitios web con mucho tráfico y necesidades de alto rendimiento. 
*   **Cuando es necesario administrar eficientemente los recursos del servidor, como CPU y memoria:** PHP FPM es un gestor de procesos separado que permite un mejor control sobre el uso de los recursos del servidor. Esto significa que es posible asignar recursos de manera más precisa y equilibrar la carga del servidor de forma más eficiente. 
*   **Cuando es necesario mejorar la escalabilidad del servidor, permitiendo la adición de más sitios web sin degradar el desempeño:** PHP FPM es capaz de escalar fácilmente en ambientes de alta demanda, permitiendo que el servidor aloje más sitios web sin impactar el desempeño. 
*   **Cuando es importante tener una mayor estabilidad y confianza en el ambiente de alojamiento web:** PHP FPM es un proceso separado y autónomo que ejecuta scripts PHP de forma más segura y estable que otros métodos de procesamiento PHP. Esto puede ayudar a garantizar que el servidor esté disponible y funcione sin problemas durante períodos de tiempo más largos. 

### **Cuando NO utilizar PHP-FPM** 

Situaciones en las que es mejor evitar habilitar PHP FPM: 

*   **Sitios web con bajo tráfico y recursos del servidor limitados:** Si el sitio web tiene poco tráfico y el servidor tiene recursos limitados, puede que no haya ningún beneficio al usar PHP-FPM, e incluso puede perjudicar el rendimiento del servidor. 
*   **Sitios web que dependen de extensiones PHP que no son compatibles con PHP-FPM:** Algunas extensiones PHP pueden no funcionar correctamente com PHP-FPM, y, en este caso, puede ser mejor evitar su uso. 
*   **Sitios web que utilizan scripts antiguos o mal escritos:** Si el sitio web utiliza scripts antiguos o mal escritos que no están optimizados para PHP-FPM, puede haber problemas de rendimiento o compatibilidad. 
*   **Configuración incorrecta de PHP-FPM:** Si PHP-FPM no está configurado correctamente, esto puede provocar problemas de desempeño o incluso el fallo del servidor. 
*   **Servidores con pocos recursos de CPU y memoria:** PHP-FPM puede exigir más recursos de CPU que PHP en modo CGI tradicional, por lo que en servidores con pocos recursos de CPU, puede ser mejor evitar activarlo. Además de esto, cPanel recomienda poseer al menos 30MB de RAM disponibles para el dominio.