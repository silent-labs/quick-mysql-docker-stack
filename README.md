# Docker MySQL y phpMyAdmin

![Docker](https://img.shields.io/badge/Docker-20.10+-blue.svg)
![MySQL](https://img.shields.io/badge/MySQL-8.0-orange.svg)
![phpMyAdmin](https://img.shields.io/badge/phpMyAdmin-latest-blueviolet.svg)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

Este proyecto proporciona una configuración de Docker para ejecutar MySQL y phpMyAdmin de manera rápida y sencilla.

## Requisitos Previos

- Docker instalado en tu sistema
- Docker Compose instalado en tu sistema
- Puertos 3307 y 8080 disponibles en tu sistema

## Estructura del Proyecto

```
mysql servidor/
├── docker-compose.yml    # Configuración de los servicios
├── .env                  # Variables de entorno
└── README.md            # Esta documentación
```

## Variables de Entorno

El archivo `.env` contiene las siguientes configuraciones:

```env
# MySQL
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=mi_base_datos
MYSQL_USER=usuario
MYSQL_PASSWORD=password

# Puertos
MYSQL_PORT=3307
PMA_PORT_EXPOSED=8080
```

## Uso

1. Clona o descomprime el proyecto
2. Navega hasta la carpeta del proyecto:
   ```bash
   cd "quick-mysql-docker-stack-main"
   ```
3. Inicia los contenedores:
   ```bash
   docker-compose up -d
   ```
4. Ver los logs de los contenedores:
   ```bash
   # Ver todos los logs
   docker-compose logs

   # Ver logs en tiempo real
   docker-compose logs -f

   # Ver logs de un servicio específico
   docker-compose logs mysql
   docker-compose logs phpmyadmin
   ```
5. Verificar el estado de los contenedores:
   ```bash
   docker-compose ps
   ```
6. Reiniciar los servicios:
   ```bash
   # Reiniciar todos los servicios
   docker-compose restart

   # Reiniciar un servicio específico
   docker-compose restart mysql
   docker-compose restart phpmyadmin
   ```
7. Detener los contenedores:
   ```bash
   # Detener los servicios
   docker-compose stop

   # Detener y eliminar los contenedores
   docker-compose down

   # Detener y eliminar contenedores, redes y volúmenes
   docker-compose down -v
   ```
8. Ejecutar comandos dentro del contenedor MySQL:
   ```bash
   # Acceder a la consola de MySQL
   docker-compose exec mysql mysql -uroot -proot

   # Hacer backup de una base de datos
   docker-compose exec mysql mysqldump -uroot -proot mi_base_datos > backup.sql
   ```

## Acceso a los Servicios

### MySQL
- **Host**: localhost
- **Puerto**: 3307
- **Usuario Root**:
  - Usuario: root
  - Contraseña: root
- **Usuario Adicional**:
  - Usuario: usuario
  - Contraseña: password
- **Base de datos**: mi_base_datos

### phpMyAdmin
- **URL**: http://localhost:8080
- **Usuario**: root
- **Contraseña**: root

## Persistencia de Datos

Los datos de MySQL se mantienen persistentes a través de un volumen Docker llamado `mysql_data`.

## Solución de Problemas

1. Si el puerto 3307 está en uso, puedes modificar `MYSQL_PORT` en el archivo `.env`
2. Si el puerto 8080 está en uso, puedes modificar `PMA_PORT_EXPOSED` en el archivo `.env`
3. Para reiniciar los servicios:
   ```bash
   docker-compose restart
   ```

## Seguridad

Por defecto, este es un entorno de desarrollo. Para producción, se recomienda:
- Cambiar todas las contraseñas en el archivo `.env`
- Utilizar secretos de Docker para las credenciales
- Configurar reglas de firewall apropiadas 
