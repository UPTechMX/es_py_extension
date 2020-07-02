# Extensión de muestra del servidor para Oskari

Esta es una platilla que puede ser utilizada como base para extender y personalizar el servidor oskari.

Da clíc en el botón "Use this template" en el repositorio para crear una copia de los archivos bajo tu nombre de usuario y comienza a personalizarlo.

Esta aplicación puede ser vista en http://dev.oskari.org.

## Modificando la configuración inicial de la aplicación:
 
El contenido inicial y la configuración sobre la base de datos es creada con Flyway-scripts debajo de:
 - app-resources/src/main/java/flyway/example
 - app-resources/src/main/resources/flyway/example

Estas migraciones se ejecutan en el orden de las versiones, y cambiarlas modificará la aplicación que es creada sobre bases de datos vacías.

También puedes renombrar el folder de "example" a algo más apropiado para tu aplicación.
Nota que esta línea en oskari-ext.properties será utilizada para encontrar los scripts, así que renombrala "example" en ella también:

    db.additional.modules=myplaces, userlayer, example

Las capas pueden ser configuradas en json:

    app-resources/src/main/resources/json/layers

Y referenciadas en las configuraciones de la aplicación como en (las capas clave seleccionadas):

    app-resources/src/main/resources/json/views/geoportal-3857.json

Compila con:

    mvn clean install
    
Reemplaza oskari-map.war debajo de {jetty.home}/webapps/ con la creada debajo de webapp-map/target 

¡Nota! Si modificas el orden de "vistas" (configuraciones de aplicación) podrías necesitar modificar oskari-ext.properties:

    # default view is the first app setup (value is the database id)
    view.default=1

    # publish template is the second app setup
    view.template.publish=2

    # "native" projection to store the myplaces etc user-generated content:
    oskari.native.srs=EPSG:3857

Para activar el registro de nombre de usuario, configura estos (más información en http://oskari.org/documentation/features/usermanagement):

    allow.registration=true
    oskari.email.sender=<sender@domain.com>
    oskari.email.host=<smtp.domain.com>

*¡Nota!* Nosotros actualizarémos las Flyway-migrations existentes en este repositorio para igualar cualquier
 cambio que consideremos como una mejora para esta plantilla. Esto es algo que _TU NO DEBERIAS_ hacer en tu personalización
 ya que ejecutar migraciones modificadas en una base de datos existente detonara un error. Esto sólo se hace para mantener la plantilla más simple.

# Reporte de problemas

Todas los problemas relacionadas con Oskari deberían ser reportados aquí: https://github.com/oskariorg/oskari-docs/issues

## Licencia

Este trabajo tien licencia dual por MIT y [EUPL v1.1](https://joinup.ec.europa.eu/software/page/eupl/licence-eupl)
(cualquier versión de lenguaje aplica, la versión en Inglés se incluye en https://github.com/oskariorg/oskari-docs/blob/master/documents/LICENSE-EUPL.pdf).
Puedes elegir cualquiera de ellas, si lo necesitas.

`SPDX-License-Identifier: MIT OR EUPL-1.1`

Copyright (c) 2014-present National Land Survey of Finland
