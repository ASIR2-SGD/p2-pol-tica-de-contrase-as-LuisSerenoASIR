# Política de contraseñas

## Contexto
Por defecto, la mayoría de sistemas operativos, vienene con una política de contraseña muy laxa, una contraseña segura presenta una barrera más al atacante, que en su intento de acceder al sistema, indudablemete dejará más rastro y en algunos casos a provocar el abandondo de ataque.

## Objetivos
* Entender el sistema de contraseñas del sistema operativo linux
* Entender el PAM (Plugable authentication Module)
* Instalar y configurar la libreria _pwquality_
* Comprobar y verificar que se ha llevado la práctica de forma correcta
* Documentar la práctica.
* __Política Debil (min. 6, *)__
* __Política Media (min. 8, [0,9], [A-Z] *)__
* __Política Extrema (min. 12, [0-9], [A-z], [a-z], [#,$,@...])__

___
___
___

# PRÁCTICA

## Como funcionan las contraseñas.

En linux las contraseñas se alamacenan principalmente en dos archivos, ```/etc/passwd``` y en este se encuentra la información del usuario como es su **username** de login, su **nombre completo**, directorio home, etc...
    
Por otro lado tenemos el archivo ```/etc/shadow``` en el cual se encuentran las contraseñas pero esta vez cifradas y la información de **validez de la cuenta**, **caducidad**, 

---
## PAM (Plugable authentication Module)

El PAM consiste en el uso de diferentes módulos para cada servicio el cual facilita que cada uno de ellos no nencesite un mecanismo propio de acceso, esto se usa en la autenticación de usuarios en el sistema Linux.

---
## Instalación y configuración de _pwquality_.

Usamos el siguiente comando para instalar **pwquality**

        apt install libpam-pwquality

Tenemos que modificar el archivo ```/etc/pam.d/common-password```, y modificamos la siguiente linea:

        password [success=1 default=ignore] pam_unix.so obscure yescrypt

# DESAROLLO

A continuación en una tabla tendremos los diferentes criterios de contraseñas:

|           | Score     | Long.Min  | Requisitos|Ejemplo|
|-----------|-----------|-----------|-----------|-----------|
|NO VALIDA  | <35       |   -       | -         |     Hola22   |
|DÉBIL      | 35-50     | 6         |  minlen = 6,dcredit = 0,ucredit = 0, lcredit = 0, ocredit = 0|Hol@5t|
|MEDIA      | 50-80     | 8         | minlen = 8, dcredit = -1, ucredit = -1, lcredit = 0, ocredit = -1  |H0?A#_Ñ´|
|EXTREMA    | >80       | 10        | minlen = 10, dcredit = -1, ucredit = -1, lcredit = -1 , ocredit = -1  |ñWR3·ÑDM#¨|
