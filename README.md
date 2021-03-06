![](./images/logos_feder.png)



| Entregable     | Procesador de datos                                          |
| -------------- | ------------------------------------------------------------ |
| Fecha          | 28/04/2021                                                   |
| Revisado por   | Paloma Terán Pérez                                           |
| Proyecto       | [ASIO](https://www.um.es/web/hercules/proyectos/asio) (Arquitectura Semántica e Infraestructura Ontológica) en el marco de la iniciativa [Hércules](https://www.um.es/web/hercules/) para la Semántica de Datos de Investigación de Universidades que forma parte de [CRUE-TIC](https://www.crue.org/proyecto/hercules/) |
| Módulo         | Fuseki                                                       |
| Tipo           | Software                                                     |
| Objetivo       | Servidor SPARQL 1.1 para proyecto ASIO                       |
| Estado         | **100%**                                                     |
| Próximos pasos |                                                              |
| Documentación  | [Manual de usuario](https://github.com/HerculesCRUE/ib-asio-docs-/blob/master/00-An%C3%A1lisis/Manual%20de%20usuario/Manual%20de%20usuario.md)<br />[Manual de despliegue](https://github.com/HerculesCRUE/ib-asio-composeset/blob/master/README.md)<br />[Documentación técnica](https://github.com/HerculesCRUE/ib-asio-docs-/blob/master/00-Arquitectura/arquitectura_semantica/documento_arquitectura/ASIO_Izertis_Arquitectura.md) |


## FUSEKI

Servidor SPARQL 1.1 para proyecto ASIO

Se añade configuración propia para interactuar con Trellis

#### Configuración

Todos los ficheros de configuración se encuentran en la ruta ./fuseki-conf

##### trellis.ttl

Configuración relativa a el dataset usado por Trellis, en la construcción del contenedor, creara el dataset

##### shiro.ini

Configuración relativa autorización y autentificación, en este momento, se usa configuración por defecto

##### log4j.properties

Configuración relativa logs

#### Construcción

El fichero **Dockerfile**, crea imagen Docker a partir de la imagen oficial `stain/jena-fuseki:latest` y añade ficheros de configuración

El fichero **docker-compose.yml**  usa la imagen definida en el contenedor, y añade volúmenes persistentes para datos y backups

#### Despliegue

```bash
docker-compose up -d
```

#### EndPoint SPARQL

A partir del despliegue esta disponible el End Point SPARQL.

Es accesible desde el **navegador** en la ruta http://localhost:3030/

![fuseki_main](https://i.ibb.co/5xhJqcf/fuseki-main.png)

Y pulsando el botón query, podemos ejecutar queries SPARQL en el EndPoint http://localhost:3030/trellis

![](https://i.ibb.co/X3M8fYS/fuseki-query.png)



También es posible realizar la consulta a partir de su **API REST**

Petición

```http
GET /trellis/query?query=SELECT+%3Fsubject+%3Fpredicate+%3Fobject%0A%09WHERE+%7B%0A+%09%09+%3Fsubject+%3Fpredicate+%3Fobject%0A%09%7D HTTP/1.1
Host: localhost:3030
```

Respuesta

```json
{
  "head": {
    "vars": [
      "subject",
      "predicate",
      "object"
    ]
  },
  "results": {
    "bindings": [
      {
        "subject": {
          "type": "uri",
          "value": "trellis:data/"
        },
        "predicate": {
          "type": "uri",
          "value": "http://purl.org/dc/terms/modified"
        },
        "object": {
          "type": "literal",
          "datatype": "http://www.w3.org/2001/XMLSchema#dateTime",
          "value": "2020-03-20T11:05:12.109241Z"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:data/"
        },
        "predicate": {
          "type": "uri",
          "value": "http://www.w3.org/1999/02/22-rdf-syntax-ns#type"
        },
        "object": {
          "type": "uri",
          "value": "http://www.w3.org/ns/ldp#BasicContainer"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:data/basic"
        },
        "predicate": {
          "type": "uri",
          "value": "http://purl.org/dc/terms/modified"
        },
        "object": {
          "type": "literal",
          "datatype": "http://www.w3.org/2001/XMLSchema#dateTime",
          "value": "2020-03-20T11:05:11.999422400Z"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:data/basic"
        },
        "predicate": {
          "type": "uri",
          "value": "http://www.w3.org/1999/02/22-rdf-syntax-ns#type"
        },
        "object": {
          "type": "uri",
          "value": "http://www.w3.org/ns/ldp#BasicContainer"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:data/basic"
        },
        "predicate": {
          "type": "uri",
          "value": "http://purl.org/dc/terms/isPartOf"
        },
        "object": {
          "type": "uri",
          "value": "trellis:data/"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:data/basic"
        },
        "predicate": {
          "type": "uri",
          "value": "http://www.w3.org/ns/prov#wasGeneratedBy"
        },
        "object": {
          "type": "uri",
          "value": "trellis:bnode/baf33ea3-b1fc-4aac-ab9c-f898dd72c509a4417e75-b8c7-47d1-b0bd-68a5848ca43c"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:data/basic/"
        },
        "predicate": {
          "type": "uri",
          "value": "http://purl.org/dc/terms/title"
        },
        "object": {
          "type": "literal",
          "value": "A Basic Contanier"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:bnode/baf33ea3-b1fc-4aac-ab9c-f898dd72c509a4417e75-b8c7-47d1-b0bd-68a5848ca43c"
        },
        "predicate": {
          "type": "uri",
          "value": "http://www.w3.org/1999/02/22-rdf-syntax-ns#type"
        },
        "object": {
          "type": "uri",
          "value": "http://www.w3.org/ns/prov#Activity"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:bnode/baf33ea3-b1fc-4aac-ab9c-f898dd72c509a4417e75-b8c7-47d1-b0bd-68a5848ca43c"
        },
        "predicate": {
          "type": "uri",
          "value": "http://www.w3.org/1999/02/22-rdf-syntax-ns#type"
        },
        "object": {
          "type": "uri",
          "value": "https://www.w3.org/ns/activitystreams#Create"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:bnode/baf33ea3-b1fc-4aac-ab9c-f898dd72c509a4417e75-b8c7-47d1-b0bd-68a5848ca43c"
        },
        "predicate": {
          "type": "uri",
          "value": "http://www.w3.org/ns/prov#wasAssociatedWith"
        },
        "object": {
          "type": "uri",
          "value": "http://www.trellisldp.org/ns/trellis#AnonymousAgent"
        }
      },
      {
        "subject": {
          "type": "uri",
          "value": "trellis:bnode/baf33ea3-b1fc-4aac-ab9c-f898dd72c509a4417e75-b8c7-47d1-b0bd-68a5848ca43c"
        },
        "predicate": {
          "type": "uri",
          "value": "http://www.w3.org/ns/prov#atTime"
        },
        "object": {
          "type": "literal",
          "datatype": "http://www.w3.org/2001/XMLSchema#dateTime",
          "value": "2020-03-20T11:05:11.890386100Z"
        }
      }
    ]
  }
}
```



#### Configuración Trellis para conectar con el Triplestore a partir de el EndPoint SPARQL

A partir del proyecto Trellis personalizado para le proyecto [asio-ldp](https://git.izertis.com/universidaddemurcia/semantmurc/asio-ldp), es necesario modificar el fichero config-dev.yml (la línea resources para que apunte al Endpoint SPARQL de Fuseki con el dataset del proyecto).

```bash
server:
  applicationConnectors:
    - type: http
      port: 8080
  requestLog:
    appenders:
      - type: console
        target: stdout
        threshold: INFO

logging:
  level: WARN
  appenders:
    - type: console
      target: stdout
      threshold: INFO
  loggers:
    org.trellisldp: INFO
    io.dropwizard: INFO

resources: http://localhost:3030/trellis/  # Configuraci�n para conexi�n al EndPoint Fuseki, apuntando al dataset trellis

binaries: /opt/trellis/data/binaries

mementos: /opt/trellis/data/mementos

namespaces: /opt/trellis/data/namespaces.json

# This may refer to a static base URL for resources. If left empty, the
# base URL will reflect the Host header in the request.
baseUrl:

# This configuration will enable a WebSub "hub" header.
hubUrl:

auth:
    adminUsers: []
    webac:
        enabled: false
    jwt:
        enabled: false
        key: changeme
    basic:
        enabled: true
        usersFile: /opt/trellis/etc/users.auth

cors:
    enabled: true
    allowOrigin:
        - "*"
    maxAge: 180

cache:
    maxAge: 86400
    mustRevalidate: true

notifications:
    enabled: false
    type: JMS
    topicName: "trellis"
    connectionString: "tcp://localhost:61616"

# JSON-LD configuration
jsonld:
    cacheSize: 10
    cacheExpireHours: 24
    contextWhitelist: []
    contextDomainWhitelist: []


```
