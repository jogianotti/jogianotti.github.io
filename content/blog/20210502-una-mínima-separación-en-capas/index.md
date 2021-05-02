---
title: Una mínima separación en capas
date: 2021-05-02T16:47:13-03:00
description: Con una mínima separación de capas se puede obtener grandes beneficios
draft: false
slug: una_minima_separacion_en_capas
categories: [ arquitectura ]
tags: [ dominio, infraestructura, tests ]
---

#### Acoplamiento
En desarrollo web es muy frecuente terminar con una arquitectura donde el nivel de acoplamiento dificulta la mantenibilidad del código de un proyecto.

Yo fui culpable de estos "errores" que no siempre son errores, pero dado el caso de una aplicación con expectativas de crecimiento estos "errores" se deberían evitar.

Cuando hablo de acoplamiento me refiero a un método controlador que se encarga de todo lo relacionado con la atención de una solicitud. Este método se encarga de recibir la solicitud, procesar los datos de entrada, ejecutar la lógica relacionada con el caso de uso, realizar tareas secundarias que se desprenden de ese caso de uso, comunicarse con servicios externos enviando o recibiendo datos, preparar los datos resultantes y por último retornar una respuesta.

Aquí pongo un ejemplo gráfico.

{{< figure src="estado_inicial.png" >}}

Se puede ver como el controlador gestiona la colaboración con el resto de las clases del sistema para atender la solicitud que recibe, siendo el responsable de todas las tareas mencionadas anteriormente.

Lo más importante a prestar atención es el hecho de que es el controlador quien contiene la **lógica del caso de uso** lo que dificulta la reutilización del mismo y la incorporación de tests útiles.

Si se quisiera reutilizar ese caso de uso, por ejemplo en un comando por consola, se deberían imitar los mismos pasos que se siguen en el controlador dificultando la mantenibilidad y consistencia de ese caso de uso. Además si se quisiera crear un test para ese caso de uso se debería realizar sobre la salida del controlador que en muchos casos significa procesar código HTML por lo que el test se volvería más complejo y lento.


#### Separación en dos capas

¿De qué forma se puede modificar esta arquitectura con el fin de mejorar la reutilización y permitir la incorporación de tests útiles?

Hay dos tareas relativamente sencillas que permiten tener una separación clara en dos capas. Una se suele nombrar como capa de **dominio** y la otra como capa de **infraestructura**. Nuestra capa de dominio contiene todo el código relacionado con nuestra **lógica de negocio**. Nuestra capa de infraestructura contiene todo el código que interviene en tareas de **entrada/salida**.

Lo primero es agrupar toda la lógica del caso de uso en su propia clase que será inyectada como colaborador del controlador o de cualquier otra clase que la requiera. Esto permite la reutilización de ese caso de uso manteniendo así la consistencia.

Lo segundo es implementar el **principio de inversión de dependencia (DIP)** para la relación con todos los servicios externos. Este principio establece que *"módulos de alto nivel no deberían depender de los de bajo nivel, ambos deberían depender de abstracciones"*. Entonces tomando este principio podemos decir que nuestro dominio no debería depender de un determinado servicio sino de una abstracción. Para lograr esto simplemente debemos establecer interfaces que definan el protocolo de comunicación con los diferentes servicios que utiliza nuestra aplicación y que nuestro dominio dependa solo de esas interfaces que serán nuestra abstracción.

Para hacer bien gráfico este ejemplo aquí está la arquitectura a la que se pretende llegar con este proceso.

{{< figure src="estado_final.png" >}}

#### Conclusión

Con una simple organización de nuestro desarrollo se tienen grandes beneficios que apuntan a tener una base de código que sea **fácil de mantener** y que **tolere el cambio**.
