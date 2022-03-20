---
title: Recibir notificaciones del log de errores
date: 2021-04-24T08:58:10-03:00
description: Herramienta para el monitoreo de logs
draft: false
slug: recibir_notificaciones_del_log_de_errores
categories: [ administración ]
tags: [ linux, swatch ]
---
#### Swatch
Al momento de monitorear un archivo de log hay muchas alternativas. Una opción simple es el uso de la herramienta **Swatch** que nos va a permitir recibir un correo electrónico ante una nueva entrada en un archivo de log dado. Cuando se debe monitorear un log para dar una respuesta rápida ante errores o ataques este método no es el correcto por la demora que puede haber en la recepción de ese correo.
Pero si este método sirve como herramienta de notificación para que eventualmente sea revisada.

Es necesario definir en un archivo aquellos patrones de búsqueda y la acción a realizar. En este caso simplemente vamos a atender aquellas entradas que coincidan con la palabra **"error"** y enviaremos un email con el asunto **ERROR**.

{{< gist jogianotti 0e13763a26608a63b99d5a5f0cb73765 ".swatchrc" >}}

Una vez que se han definido todas las reglas necesarias en el archivo de configuración se debe levantar el servicio indicando el archivo de log al cual observar.

```
swatch --config-file .swatchrc --tail-file /var/log/apache2/error.log --daemon
```

#### Conclusión
Esta es una forma simple y efectiva de recibir notificaciones ante determinados eventos que se registren en un archivo de log.
