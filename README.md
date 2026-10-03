# Práctica XML y DTD
Estudiante: Beltran Astorga Santiago 225203551
## Objetivo
Al finalizar la práctica, el estudiante será capaz de:

-   diseñar documentos XML a partir de información no estructurada;
-   identificar elementos y atributos;
-   construir documentos XML bien formados;
-   definir DTD internos y externos;
-   utilizar cardinalidades y restricciones de atributos;
-   validar documentos XML;
-   gestionar incrementalmente los artefactos mediante Git.
## Ejercicio 1: Pedido
### Modelo propuesto
<?xml version="1.0" encoding="UTF-8"?>
<pedido>
    <nombre>Juan Delgado Martinez</nombre>
    <articulo>Bicicleta Bianchi</articulo>
    <direccion>Reforma 423</direccion>
    <fecha>19-09-2021</fecha>
</pedido>

### Decisiones de diseño
Tome esas decisiones para hacer un diseno mas simple, pero despues
vi las preguntas y le eche mas coco.

## Ejercicio 2: Nota
### DTD externo
<!ELEMENT nota (para, de, titulo, contenido)>
<!ELEMENT para (#PCDATA)>
<!ELEMENT de (#PCDATA)>
<!ELEMENT titulo (#PCDATA)>
<!ELEMENT contenido (#PCDATA)>
### DTD interno
<!DOCTYPE nota [
    <!ELEMENT nota (para, de, titulo, contenido)>
    <!ELEMENT para (#PCDATA)>
    <!ELEMENT de (#PCDATA)>
    <!ELEMENT titulo (#PCDATA)>
    <!ELEMENT contenido (#PCDATA)>
]>
### Pruebas realizadas
| Modificación       | ¿Bien formado? | ¿Válido? | ¿Por qué? |
 |--------------------|----------------|----------|-----------|
 | Cambiar `para`     |           si               |  no | No esta declarado |
| Cambiar orden      |     no     |        no          | No sigue el orden |
| Agregar `telefono` |   si   |          no            | Porque no esta declarado |

## Ejercicio 3: Matrícula
### Modelo
``` text
matricula
├── personal
│   ├── dni
│   ├── nombre
│   ├── titulacion
│   ├── curso_academico
│   └── domicilios
│       └── domicilio+
└── pago
    └── tipo_matricula
```
### Cardinalidad
| Símbolo|  Significado|
 |---------|------------|
 |`?` |     cero o uno|
| `*`  |    cero o más|
 |`+`   |   uno o más|
### Restricción del atributo tipo
El XML utiliza:

``` xml
<domicilio tipo="familiar">
<domicilio tipo="habitual">
```

El atributo `tipo` debe ser obligatorio y solo admitir `familiar` o
`habitual`.
### DTD externo
<!ELEMENT matricula (personal, pago)>

<!ELEMENT personal (dni, nombre, titulacion, curso_academico, domicilios)>
<!ELEMENT dni (#PCDATA)>
<!ELEMENT nombre (#PCDATA)>
<!ELEMENT titulacion (#PCDATA)>
<!ELEMENT curso_academico (#PCDATA)>

<!ELEMENT domicilios (domicilio+)>
<!ATTLIST domicilio tipo (familiar|habitual) #REQUIRED>

<!ELEMENT pago (tipo_matricula)>
<!ELEMENT tipo_matricula (#PCDATA)>
### DTD interno
<!DOCTYPE matricula [
    <!ELEMENT matricula (personal, pago)>

    <!ELEMENT personal (dni, nombre, titulacion, curso_academico, domicilios)>
    <!ELEMENT dni (#PCDATA)>
    <!ELEMENT nombre (#PCDATA)>
    <!ELEMENT titulacion (#PCDATA)>
    <!ELEMENT curso_academico (#PCDATA)>

    <!ELEMENT domicilios (domicilio+)>
    <!ATTLIST domicilio tipo (familiar|habitual) #REQUIRED>

    <!ELEMENT pago (tipo_matricula)>
    <!ELEMENT tipo_matricula (#PCDATA)>
]>
### Pruebas realizadas
 | Caso              | Predicción | Resultado | Explicación |
|-------------------|------------|-----------|-------------|
 | `tipo="familiar"` |     Si       |     Si      |      Porque declara uno o mas       |
 | `tipo="habitual"` |     Si       |      Si     |      Porque declara uno o mas       |
| `tipo="temporal"` |     No      |    No      |      No esta declarado en el dtd entonces no es valido       |
| sin `tipo`        |     No       |     No      |  Porque no declara ninguno, entonces no es valido |

## Conclusiones
Con todo lo que hemos visto, nos hemos dado cuenta de que la consistencia en programacion es muy
importante.
No tan solo porque varios van a ver y contribuir al codigo, sino porque algunas herramientas dependen
de esas consistencia.
