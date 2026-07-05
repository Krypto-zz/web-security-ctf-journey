# Notas - Día 3 OS Command Injection

## Objetivo del día

Comprender cómo una entrada controlada por el usuario puede terminar siendo interpretada como un comando del sistema operativo.

## Teoría aprendida

Bash es un intérprete de comandos utilizado en sistemas Linux.

Una función como `system()` permite ejecutar comandos del sistema operativo. El peligro aparece cuando una aplicación concatena directamente datos enviados por el usuario dentro del comando.

Ejemplo conceptual vulnerable:

```text
comando = "ping " + entrada_usuario
system(comando)
```

Si la entrada no es tratada correctamente, Bash puede interpretar caracteres especiales y ejecutar instrucciones adicionales.

## Operadores estudiados

### Punto y coma

```bash
comando1; comando2
```

Ejecuta ambos comandos sin importar si el primero tuvo éxito o falló.

### AND lógico

```bash
comando1 && comando2
```

Ejecuta el segundo comando solamente si el primero devuelve un código de salida correcto.

### OR lógico

```bash
comando1 || comando2
```

Ejecuta el segundo comando solamente si el primero falla.

### Pipe

```bash
comando1 | comando2
```

Envía la salida del primer comando como entrada del segundo.

### Sustitución de comandos

```bash
echo "$(whoami)"
```

Ejecuta primero `whoami` y coloca su resultado dentro del comando exterior.

---

## Laboratorio 1 — Command Injection visible

La funcionalidad investigada fue el comprobador de stock.

La petición era de tipo POST y contenía parámetros parecidos a:

```http
productId=1&storeId=1
```

Probé modificando los parámetros desde Burp Repeater hasta descubrir que `storeId` llegaba a un comando del sistema.

Introduje el comando `whoami` utilizando un separador de Bash.

La aplicación mostró directamente la salida del comando y devolvió el usuario:

```text
peterGl4gdv
```

Esto confirmó que existía una OS Command Injection visible.

## Laboratorio 2 — Blind Command Injection

La funcionalidad investigada fue el formulario de feedback.

Los parámetros enviados incluían datos como el nombre, correo electrónico, asunto y mensaje.

Después de probar los parámetros, determiné que el campo vulnerable era `email`.

Al principio probé `whoami`, pero no observé ningún cambio. Después entendí que el comando podía ejecutarse, pero la aplicación no devolvía su salida.

Para demostrar la ejecución fue necesario provocar un efecto secundario observable: un retraso controlado.

Utilicé un comando que realizaba diez solicitudes `ping` hacia la dirección loopback del propio servidor:

```bash
ping -c 10 127.0.0.1
```

La petición modificada tardó aproximadamente diez segundos más que una petición normal.

## Errores y dificultades

* Al principio esperaba que `whoami` causara algún cambio visible.
* No había comprendido completamente que, en una vulnerabilidad ciega, la salida del comando no aparece.
* Probé diferentes parámetros, pero no tenía todavía el comando adecuado para provocar una señal observable.
* Necesité consultar la solución para descubrir la prueba basada en tiempo.

## Qué aprendí

Aprendí que resolver una vulnerabilidad no siempre significa recibir directamente información del servidor.

En una Command Injection ciega debo buscar una forma indirecta de confirmar la ejecución, por ejemplo:

* Retrasos en la respuesta.
* Peticiones externas.
* Creación de archivos.
* Cambios observables en el comportamiento.


## Qué debo mejorar

* Practicar más laboratorios de Command Injection ciega.
* Medir tiempos normales antes de probar payloads.
* Cambiar un solo parámetro por vez.
* Diferenciar entre comandos que producen salida y comandos que producen efectos observables.
