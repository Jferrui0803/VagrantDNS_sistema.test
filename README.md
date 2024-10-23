# Proyecto: Configuración de Servidor DNS Maestro-Esclavo

Este proyecto consiste en la configuración de un sistema DNS maestro-esclavo utilizando **BIND9** y **Vagrant**. La red está configurada con dos servidores: **tierra.sistema.test** (maestro) y **venus.sistema.test** (esclavo).

## Contenido

- [Requisitos previos](#requisitos-previos)
- [Infraestructura del Proyecto](#infraestructura-del-proyecto)
- [Pasos Realizados](#pasos-realizados)
- [Configuración del Servidor Maestro](#configuración-del-servidor-maestro)
- [Configuración del Servidor Esclavo](#configuración-del-servidor-esclavo)
- [Verificación y Solución de Problemas](#verificación-y-solución-de-problemas)
- [Comprobación Final](#comprobación-final)
- [Licencia](#licencia)

---

## Requisitos previos

- **Vagrant** instalado.
- **VirtualBox** instalado.
- Acceso a internet para descargar las imágenes de Debian.

---

## Infraestructura del Proyecto

Este proyecto está compuesto por 2 máquinas virtuales en una red privada (192.168.57.0/24):

| Máquina                | FQDN                  | IP              | Rol                         |
|------------------------|-----------------------|-----------------|-----------------------------|
| Tierra (maestro)        | tierra.sistema.test    | 192.168.57.103  | Servidor DNS Maestro (BIND9) |
| Venus (esclavo)         | venus.sistema.test     | 192.168.57.102  | Servidor DNS Esclavo (BIND9) |

---

## Pasos Realizados

1. **Inicialización del Proyecto con Vagrant:**
   - Se crearon dos máquinas virtuales con Vagrant para actuar como el servidor maestro (tierra) y el esclavo (venus). Ambas se configuraron en la red privada `192.168.57.0/24`.

2. **Configuración del Servidor Maestro (`tierra.sistema.test`):**
   - Instalamos BIND9 y configuramos las zonas directa e inversa.
   - Permitimos la transferencia de zonas al servidor esclavo (venus) mediante la opción `allow-transfer`.

3. **Configuración del Servidor Esclavo (`venus.sistema.test`):**
   - Configuramos BIND9 para actuar como esclavo, recibiendo las zonas del maestro.

4. **Solución de Problemas:**
   - Se corrigieron errores de permisos en los archivos de zona.
   - Se ajustaron configuraciones en el archivo de opciones de BIND9 para escuchar solo en IPv4.
   - Se habilitó la transferencia de zona y se resolvieron problemas de conectividad entre las máquinas.

---

## Configuración del Servidor Maestro

## Configuración de zonas
Aquí se muestra la configuración del servidor maestro (`tierra.sistema.test`), donde se ajustaron las zonas directa e inversa.

![Configuración zonas del Servidor Maestro](./images/named-conf-loc.png)

---

## Configuración de Opciones
El archivo /etc/bind/named.conf.options se ajustó para escuchar solo en IPv4 y permitir consultas desde la red local.

![Configuración opciones del Servidor Maestro](./images/named-conf-options.png)

---

## Archivos de Zona Directa e Inversa

## El archivo de Zona Directa

El archivo db.sistema.test define cómo el servidor DNS maestro resuelve los nombres de dominio dentro de la zona sistema.test a sus respectivas direcciones IP.

![Configuración zona directa](./images/db-sistema-test.png)


---

## El archivo de Zona Inversa

El archivo db.sistema.test define cómo el servidor DNS maestro resuelve los nombres de dominio dentro de la zona sistema.test a sus respectivas direcciones IP.


![Configuración zona inversa](./images/db127.png)


---

## Comprobación Final

Para asegurarnos de que la configuración DNS está funcionando correctamente, realizamos las siguientes comprobaciones:

1. **Resolver registros A**:
   
   - Se resolvieron los registros A para verificar que las direcciones IP de los servidores maestro y esclavo.

   ![Resolver Registros A](./images/1(tierra).png)
   ![Resolver Registros A](./images/1(venus).png)

2. **Resolver direcciones inversas**:

   - Se verificó la resolución inversa para las IP de los servidores.

   ![Resolver Direcciones Inversas](./images/3(tierra).png)
   ![Resolver Direcciones Inversas](./images//3(venus).png)

3. **Alias**:

   - Comprobamos si puede resolver los alias.

   ![Alias](./images/5(tierra).png)
   ![Alias](./images/5(venus).png)

4. **Servidores NS**:

   - Se comprueba los servidores NS.

   ![Servidores NS](./images/7(tierra).png)
   ![Servidores NS](./images/7(venus).png)

5. **Servidores MX**:

    - Se comprueba los servidores MX

    ![Servidores MX](./images/8(tierra).png)
    ![Servidores MX](./images/8(venus).png)

6. **Registro AXFR**:

    - Se comprueba si se ha realizado la transferencia de la zona entre el servidor DNS maestro y el esclavo-

    Me ha dado error a la hora de hacer la conexion , he intentado de todo
    pero no hay manera de que salgan los datos.

    ![Servidores MX](./images/9(venus).png)


---

## Licencia

Este proyecto está licenciado bajo la [Apache 2.0 License](LICENSE).

---
