# Día 1 - SSRF

## Objetivo

Aprender cómo una aplicación vulnerable puede hacer peticiones internas usando el servidor como intermediario.

## Resumen

SSRF ocurre cuando un atacante logra que el servidor realice peticiones hacia direcciones internas del sistema.

En este laboratorio, la vulnerabilidad estaba en el parámetro `stockApi`, porque la aplicación tomaba una URL enviada por el usuario y el servidor hacía la petición hacia esa dirección.

## Laboratorio

- Plataforma: PortSwigger Web Security Academy
- Laboratorio: Basic SSRF against the local server
- Categoría: SSRF
- Herramienta principal: Burp Suite

## Herramientas usadas

- Burp Suite
- Burp Browser
- PortSwigger Academy

## Qué aprendí

Aprendí que `localhost` o `127.0.0.1`, cuando es consultado por el servidor vulnerable, apunta al propio servidor porque es una direccion IP dedicada a loopback.

También entendí que SSRF puede permitir acceder a recursos internos que normalmente no están expuestos desde internet.

## Nota ética

Este ejercicio fue realizado únicamente en un laboratorio legal y controlado de PortSwigger Academy.
