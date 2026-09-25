# V02 — User Management

## Escenario

El cliente necesita configurar accesos para su equipo en el servidor.
Tres roles diferentes, cada uno con permisos distintos sobre
los archivos del proyecto.

## Usuarios configurados

| Usuario | Grupo principal | Grupos secundarios | Sudo | Rol |
|---------|----------------|-------------------|------|-----|
| dev | dev | developers | No | Desarrollador |
| cloud | cloud | developers | No | Cloud Engineer |
| admin | admin | admins, sudo | Si | Administrador |

## Estructura de directorios creada
/srv/project/  
├── src/ → grupo developers, SGID activado  
├── config/ → grupo developers  
├── logs/ → solo dueño puede escribir  
└── backups/ → grupo developers  


## Permisos aplicados

| Directorio | Permisos | Significado |
|------------|----------|-------------|
| /srv/project/ | 775 + chown devops:developers | Grupo puede leer y escribir |
| /srv/project/src/ | 775 + SGID | Archivos heredan grupo developers |
| /srv/project/logs/ | 755 | Solo el dueño escribe |

## Comandos clave aprendidos

| Comando | Descripción |
|---------|-------------|
| `useradd -m -s /bin/bash -c "comentario" user` | Crear usuario modo producción |
| `getent passwd usuario` | Info completa del usuario |
| `getent group grupo` | Info completa del grupo |
| `id usuario` | UID, GID y grupos del usuario |
| `usermod -aG grupo1,grupo2 usuario` | Asignar múltiples grupos |
| `chown -R usuario:grupo directorio` | Cambiar dueño recursivo |
| `chmod -R 775 directorio` | Permisos recursivos |
| `chmod g+s directorio` | Activar SGID |
| `awk -F: '$3 >= 1000' /etc/passwd` | Listar usuarios reales |

## Diferencia entre adduser y useradd

`adduser` es interactivo y amigable, ideal para aprender.
`useradd` es el comando de bajo nivel, más rápido y usado
en scripts de automatización en producción.

## Restricción SSH aplicada

Solo los usuarios `devops` y `admin` pueden conectarse
por SSH. Configurado en `/etc/ssh/sshd_config` con `AllowUsers`.
Esto evita que usuarios de solo trabajo tengan acceso remoto.

## Lo que aprendí

El SGID en directorios resuelve uno de los problemas más
comunes en equipos: que los archivos creados por diferentes
usuarios tengan permisos inconsistentes. En lugar de arreglar
permisos manualmente, el bit SGID lo hace automáticamente.

La restricción de SSH por usuario es una de las primeras
cosas que se configura en servidores de producción.

## Evidencia

### Grupos y usuarios creados
![Grupos](./screenshots/01-groups-created.png)
![Usuarios](./screenshots/02-users-created.png)
![IDs completos](./screenshots/03-user-ids.png)

### Estructura de directorios y permisos
![Estructura](./screenshots/04-project-structure.png)
![Test de permisos](./screenshots/05-permissions-test.png)
![SGID en acción](./screenshots/06-sgid.png)

### Seguridad SSH
![Restricción SSH](./screenshots/07-ssh-restriction.png)

### Administración
![Usuarios reales](./screenshots/08-real-users.png)
![Limpieza](./screenshots/09-cleanup.png)
