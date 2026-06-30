# Notas - Día 1 SSRF

## Fecha

30/06/2026

## Objetivo del día

Entender qué es SSRF y resolver el laboratorio básico de PortSwigger

## Conceptos que repasé antes de empezar

* HTTP (mas que todos el request y sus métodos)
* localhost
* 127.0.0.1
* red interna
* servidor como intermediario
* Burp Suite
* parámetros modificables

## Idea principal que entendí

SSRF ocurre cuando una aplicación permite que el servidor haga peticiones hacia una URL controlada por el usuario.

Lo más importante que aprendí es que `localhost` o `127.0.0.1` no siempre apunta a mi computadora
Si la petición la hace el servidor, entonces `localhost` apunta al propio servidor, osea que hace referencia al propio equipo.

## Laboratorio trabajado

* Plataforma: PortSwigger Web Security Academy
* Laboratorio: Basic SSRF against the local server
* Vulnerabilidad: SSRF
* Parámetro vulnerable: `stockApi`

## Proceso que seguí

1. Entré al laboratorio de PortSwigger
2. Abrí el navegador de Burp Suite
3. Intercepté la petición al usar la función de stock
4. Encontré el parámetro `stockApi`
5. Modifiqué la URL para que el servidor consultara `localhost`.
6. Accedí al panel interno del servidor.
7. Usé la ruta administrativa del laboratorio para completar el reto.

## Errores o dudas que tuve

* Tarde demasiado en encontrar la funcion CheckStock por no ver todas las funcionalidades de la web y centrarme solo en la pagina principal
* Me confundí un poco con la diferencia entre hacer yo la petición y hacer que el servidor la haga.
* Debo practicar más lectura de peticiones HTTP en Burp Suite.
* Debo aprender más a profundidad los metodos de HTTP.

## Qué aprendí

Aprendí que SSRF permite abusar de una función que recibe URLs para hacer que el servidor consulte recursos internos.

También entendí que muchas vulnerabilidades aparecen cuando una aplicación confía demasiado en datos enviados por el usuario.

## Qué haré mejor la próxima vez

* Analizar la web antes de empezar el ataque
* Leer con más calma los parámetros de cada petición.
* Revisar si algún parámetro recibe una URL completa.
* Probar primero con rutas internas simples como `localhost`.
* Documentar el proceso apenas termine el laboratorio.
