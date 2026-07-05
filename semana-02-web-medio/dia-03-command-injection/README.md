# Día 3 - OS Command Injection

## Objetivo

Aprender cómo una aplicación vulnerable puede permitir la ejecución de comandos del sistema operativo mediante datos controlados por el usuario.

## Resumen

OS Command Injection ocurre cuando una aplicación introduce directamente datos proporcionados por el usuario dentro de un comando del sistema.

Si ese comando es procesado por un intérprete como Bash, caracteres especiales como `;`, `&&`, `||`, `|` o `$()` pueden modificar la instrucción original y permitir la ejecución de comandos adicionales.

## Laboratorios realizados

### Laboratorio 1 — Command Injection visible

* Plataforma: PortSwigger Web Security Academy
* Funcionalidad vulnerable: comprobación de stock
* Parámetro vulnerable: `storeId`
* Comando ejecutado: `whoami`
* Usuario obtenido: `peterGl4gdv`

En este laboratorio, la salida del comando se mostraba directamente en la respuesta HTTP.

### Laboratorio 2 — Blind Command Injection

* Plataforma: PortSwigger Web Security Academy
* Funcionalidad vulnerable: formulario de feedback
* Parámetro vulnerable: `email`
* Método de confirmación: retraso controlado en la respuesta

En este caso, la aplicación no mostraba la salida de los comandos. La ejecución se confirmó provocando un retraso observable mediante un comando de red.

## Herramientas utilizadas

* Burp Suite
* Burp Repeater
* Burp Browser
* PortSwigger Web Security Academy
* Kali Linux

## Qué aprendí

Aprendí que una Command Injection visible devuelve directamente la salida del comando ejecutado.

También aprendí que, en una Command Injection ciega, un comando puede ejecutarse correctamente aunque su resultado no aparezca en la respuesta. En esos casos es necesario comprobar la ejecución mediante efectos secundarios, como una diferencia de tiempo.

Además, comprendí la función de los principales operadores de Bash:

* `;` ejecuta el siguiente comando sin importar el resultado anterior.
* `&&` ejecuta el siguiente comando si el anterior tuvo éxito.
* `||` ejecuta el siguiente comando si el anterior falló.
* `|` envía la salida de un comando a otro.
* `$()` ejecuta un comando e inserta su resultado.

## Prevención

Para prevenir esta vulnerabilidad, una aplicación debería evitar construir comandos concatenando entradas del usuario.

También debería ejecutar procesos sin utilizar un shell, pasar los argumentos por separado y validar estrictamente los datos recibidos.

## Nota ética

Estas prácticas fueron realizadas exclusivamente en laboratorios legales y controlados de PortSwigger Web Security Academy.
