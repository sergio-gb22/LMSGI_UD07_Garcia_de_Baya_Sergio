# LMSGI_UD07_Garcia_de_Baya_Sergio

## *Entregable 1:* Generación del Informe Dinámico (QWeb XML)
Accedemos a Odoo vamos a ajustes y activamos el modo desarrollador como ya vimos en una actividad anterior para despues irnos a Tecnico en la barra superior buscamos el menu de interfaz de usuario y entramos a vistas despues filtramos por clave sale.report_saleorder_document y ya tenemos el XML con la sistaxis de QWeb

## *Entregable 2:* Interoperabilidad de Datos (Extracción JSON/XML)
Para poder conseguir invoice_ubl.xml, en Odoo (tenemos que tener el modo administrador activo) vamos a la aplicacion de facturacion tras esto en una factura que este ya comfirmada le clicamos en Acciones (el engranaje) y pulsamos la opcion de exportar en XML

## *Entregable 3:* Manual de Explotación bajo Norma ISO/IEC/IEEE 26514
### 1. Introducción y Arquitectura
Este documento muestra la implementación de Odoo, los modulos que tenemos que tener activos son:
* Ventas 
* Facturación 
la infraestructura es el uso de Docker que es una web que tiene un servidor de aplicaciones independiente

### 2. Guía de Instalación y Reinstalación
Descargar el código fuente .yml  y tener en visual studio code las extensiones:
* Container Tools
* Dev Containers
* Docker

 Despues dentro del archivo .yml abrir una terminal con el el atajo de teclas control + ñ para en esa terminal poner el comando docker-compose up -d y que se comiencen a descargar los contenedores

### 3. Seguridad y Control de Acceso
 Docker tiene un control de acceso basado en roles que son los siguientes:
* Administrador: tiene todos los permisos (Lectura,Escritura y Configuracion del sistema)
* Contable: tiene los permisos de crear, modificar y leer, pero en el permiso de leer solo tiene acceso a las facturas
* Comercial: tiene acceso a clientes y presupuesto y de lectura pero solo a las facturas que esten validadas

Para la contraseña es obligatorio que contenga simbolos,mayusculas y un numero y que tenga un alongitus de 12 caracteres

### 4. Procedimiento de Backup y Restauración
Para guardar la base de datos se usa las herramientas de docker que son:
docker exec -t willmantech_db pg_dump -U [usuario] -d [base_datos] -F c > backup_willmantech_$(date +%F).dump

### 5.Flujo Operativo de Facturación e Informes
* El usuario confirma la factura a traves de Odoo
* Odoo extrae los datos y genera un QWeb XML
* El documeto se renderiza y se forma un HTML
* Para despues wkhtmltopdf usa ese HTML y lo transforma a un PDF