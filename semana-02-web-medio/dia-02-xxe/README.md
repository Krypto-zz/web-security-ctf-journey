# Día 2 - XXE Injection

## Objetivo

Aprender cómo una aplicación vulnerable puede procesar XML de forma insegura y permitir la lectura de archivos del servidor mediante entidades externas.

## Resumen

XXE ocurre cuando una aplicación procesa XML enviado por el usuario y permite el uso de entidades externas.  
En este laboratorio, la vulnerabilidad estaba en la función `Check stock`, porque el servidor procesaba XML controlado por el usuario.

## Laboratorio

- Plataforma: PortSwigger Web Security Academy
- Laboratorio: Exploiting XXE using external entities to retrieve files
- Categoría: XXE Injection
- Archivo obtenido: /etc/passwd

## Herramientas usadas

- Burp Suite
- Burp Browser
- PortSwigger Academy

## Qué aprendí

Aprendí que XML puede definir entidades externas usando `DOCTYPE` y `ENTITY`.

También entendí que si el parser XML está mal configurado, puede leer archivos internos del servidor.

## Nota ética

Este ejercicio fue realizado únicamente en un laboratorio legal y controlado de PortSwigger Academy.
