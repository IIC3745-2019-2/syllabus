# Pauta AC04 Testing - Charla Cornershop

## Pregunta 1

¿Qué se conoce como "flaky test"? ¿Cómo se detectan y resuelven dentro de Cornershop?

_Respuesta:_

**(1 pto)** Son _tests_ que pasan o fallan ''de manera aleatoria".

**(0.5 ptos)** Se detectan de manera aleatoria ya que hacen fallar al _build_ en algún momento sin que haya habido cambios en el código que el _flaky test_ prueba. 

**(0.5 ptos)** Para resolverlos revisan quién fue el que lo creó y se lo asignan para su corrección. 

**Aclaración:** Muchas personas no contestaron las preguntas, sino que dieron formas de corregir los _flaky tests_. Si se realizó esto, se tiene mitad de puntaje.

Las razones de porqué un _test_ es _flaky_ pueden ser varias: se basan en variables aleatorias, sólo funciona en configuraciones del entorno de ese momento (caché, concurrencia, etc), utiliza servicios externos, entre otros.

Su corrección, naturalmente, va a depender de porqué es un _flaky test_ (por ejemplo, si es por un uso inadecuado de un servicio externo, entonces se corrige utilizando _mocks_).

**Aclaración 2:** _Sentry_ es una herramienta para notificar errores ocurridos en distintos ambientes (_staging_, experimentales, _canaries_, producción). Además entrega información para replicar el error. Este no se usa en el ambiente de _testing_.

## Pregunta 2

¿A qué se refieren con "ambiente experimental" dentro de Cornershop? ¿Cuáles son los principales propósitos de este?

_Respuesta_:

**(1 pto)** Es un ambiente **temporal** _pre-staging_, es decir,  busca (al igual que _staging_) simular a producción sin alterar los datos reales ni el _gitflow_ de la empresa.

**(1 pto)** Se utiliza normalmente para probar **las nuevas funcionalidades creadas/modificadas en una rama** con personas que no necesariamente son desarrolladores. La gracia es que si la funcionalidad no está correcta, no afecta el _gitflow_ de la empresa porque esa funcionalidad ''mala" no está _mergeada_ todavía en _development_ y puede ser reparada con tiempo.

**Aclaración:** Si se definió el ambiente _staging_, se tiene mitad de puntaje.

En Cornershop también tienen un ambiente _staging_ para probar las cosas antes de desplegar a producción. Este ambiente también se usa para que nuevos integrantes de los equipos se familiaricen con la aplicación. 

Este ambiente tiene funcionalidades terminadas y listas para desplegarse. También puede ser utilizado para probar la aplicación "de forma definitiva" antes de desplegar la aplicación con personas de otras áreas.

## Pregunta 3

¿A qué se refiere el concepto "canary release"? ¿En qué caso se usó esta técnica dentro de Cornershop?

_Respuesta:_

**(1 pto)** Es una forma de realizar el despliegue de la aplicación, que se caracteriza por distribuir un bajo porcentaje del tráfico de la aplicación hacia la nueva versión. Sirve para probar nuevas funcionalidades o configuraciones con clientes reales.

**(1 pto)** El uso más emblemático fue el cambio de versión de Python.
