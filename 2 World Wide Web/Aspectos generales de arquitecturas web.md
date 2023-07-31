# Aspectos generales de arquitecturas web

@Inma Gijón Cardos 

La arquitectura World Wide Web (WWW) de Internet provee un modelo de programación sumamente poderoso y flexible. Las aplicaciones y los contenidos son presentados en formatos de datos estándar y son localizados por aplicaciones conocidas como "web browsers", que envían requerimientos de objetos a un servidor y éste responde con el dato codificado según un formato estándar.

Los estándares WWW especifican muchos de los mecanismos necesarios para construir un ambiente de aplicación de propósito general, por ejemplo:

- **Modelo estándar de nombres:** todos los servidores, así como el contenido de la WWW se denominan según un URL (Uniform Resource Locator)
- **Contenido:** a todos los contenidos en la WWW se les especifica un determinado tipo permitiendo de esta forma que los browsers los interpreten correctamente.
- **Formatos de contenidos estándar:** todos los navegadores soportan un conjunto de formatos estándar, por ejemplo HTML, ECMA, JavaScript...
- **Protocolos estándar:** éstos permiten que cualquier navegador pueda comunicarse con cualquier servidor web. El más comúnmente usado en WWW es HTML (protocolo de transporte de hipertexto) que opera sobre el conjunto de protocolos TCP/IP.

Esta infraestructura permite a los usuarios acceder a una gran cantidad de aplicaciones y servicios de terceros. También permite a los desarrolladores crear aplicaciones y servicios para una gran comunidad de clientes.

Los aspectos generales a destacar en una arquitectura web son los siguientes:

- Escalabilidad
- Separación de responsabilidades
- Portabilidad
- Utilización de componentes en los servicios de infraestructura
- Gestión de las sesiones del usuario
- Aplicación de patrones de diseño

El esquema de funcionamiento de los servicios web requiere de tres elementos fundamentales:

1. **Proveedor del servicio web,** que es quien lo diseña, desarrolla e implementa y pone disponibilidad para su uso, dentro de la misma organización o en lo público.
2. **Consumidor del servicio,** que es quien accede al componente para utilizar los servicios que éste presta.
3. **Agente del servicio,** que sirve como enlace entre el proveedor y consumidor para efectos de publicación, búsqueda y localización del servicio.

<aside>
💡 De forma genérica podríamos decir que la arquitectura web es un modelo compuesto de tres capas: **capa de base de datos, servidores de aplicaciones web y clientes del servicio web.**

</aside>

1. **Capa de base de datos:** documentación de la información que se pretende administrar mediante el servicio web y emplearía una pataforma del tipo MySQL, PostgreSQL...
2. En una segunda capa estarían los **servidores de aplicaciones web**, ejecutando aplicaciones de tipo Apache, Tomcat, Resin...
3. En  una tercera capa estarían los **clientes del servicio web** al que accederían mediante un navegador web como Firefox, Chrome, Opera...