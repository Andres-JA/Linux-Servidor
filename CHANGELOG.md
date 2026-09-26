# Changelog

Todos los cambios relevantes de este proyecto se registran en este archivo.

El formato sigue [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/)
y el proyecto se versiona con [Versionado Semántico](https://semver.org/lang/es/).

## [No publicado]

Pendiente de iniciar la V03 — Filesystem.

## [V02] — User Management

### Agregado

- Escenario de negocio con tres roles: desarrollador, cloud engineer y administrador
- Grupos `developers` y `admins` creados con `groupadd`
- Usuarios `dev`, `cloud` y `admin` creados con `useradd -m -s /bin/bash -c`
- Asignación de grupos secundarios con `usermod -aG`
- Estructura `/srv/project/` con `src/`, `config/`, `logs/` y `backups/`
- Permisos `775` sobre el proyecto y `755` sobre `logs/`
- Bit SGID en `src/` con `chmod g+s`
- Prueba de herencia de grupo creando archivos con dos usuarios distintos
- Verificación de privilegios sudo: `dev` sin acceso y `admin` con acceso
- Restricción de acceso SSH con `AllowUsers devops admin` en `/etc/ssh/sshd_config`
- Confirmación de que el servicio SSH sigue activo tras el cambio
- Evidencia visual en `user-management/screenshots/` (7 capturas, renombradas
  con nomenclatura `NN-descripcion.jpeg`)

### Documentación

- README de V02 con tablas de usuarios, permisos y comandos clave
- Comparación entre `adduser` y `useradd` y criterio de uso de cada uno
- Sección "Lo que aprendí" sobre SGID y restricción de acceso remoto

### Notas

- El bit SGID en `src/` garantiza que los archivos hereden el grupo
  `developers` sin importar qué usuario los cree, evitando tener que
  corregir permisos manualmente
- `logs/` queda en `755` para que solo su dueño escriba y el grupo
  únicamente pueda leer los registros

## [V01] — Server Setup

### Agregado

- Instalación de Ubuntu Server 26.04 LTS en VirtualBox
- Configuración inicial: usuario `devops`, hostname `linux-server`
  y actualización de paquetes
- OpenSSH habilitado durante la instalación
- Conexión SSH exitosa desde el PC local
- Documentación completa con evidencia visual

### Solucionado

- El adaptador de red en modo NAT no asignaba IP al servidor.
  Cambiado a modo Bridge en la configuración de VirtualBox

### Documentación

- README de V01 con el entorno, las tareas completadas y los comandos aprendidos
