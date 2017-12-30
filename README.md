# Docker-wrapper-template

Template para generar wrappers que ejecuten fácilmente una imagen docker.
La finalidad es proporcionar una capa de abstracción extra para solamente
enfocarse en la configuración base para arrancar una imagen docker por única
vez.

Además se agregan funcionalidades para agrupar procesos de una misma imagen
docker en sus diferentes versiones.
Estas funcionalidades son:
  * Iniciar un nuevo proceso.
  * Detener un procesos existente.
  * Eliminar un proceso existente.
  * Conocer el estado de un proceso.
  * Listar todos los procesos de una imagen en particular.
  * etc.

## Instalación

1. Clonar el repositorio en ~/.docker-wrappers
```bash
$ git clone git@github.com:lucasdc6/Docker-wrapper-template.git
~/.docker-wrappers
```

2. Agregar el directorio ~/.docker-wrappers/bin para contar con todos los ejecutables.
Además agregar el directorio raíz donde se clonó el repositorio.
```bash
$ echo 'export DOCKERWRAPPERS_ROOT=~/.docker-wrappers' >> ~/.bash_profile
$ echo 'export PATH="$HOME/.docker-wrappers/bin:$PATH"' >> ~/.bash_profile
```

En ubuntu Ubuntu modificar ~/.bashrc

En Zsh modificar ~/.zshrc

3. Reiniciar la terminar para efectuar los cambios.

## Uso del template

Para usar el template, únicamente hace falta redefinir (al menos) la función
"new_container", la cual es la función encargada de definir cómo va a ejecutarse
la imagen docker. Por ejemplo, la función más básica podría ser algo como:

```bash
function new_container {
  docker run --rm -it $IMAGE_NAME
}
```

Además existen otras 3 funciones las cuales se pueden definir para extender la
documentación:

  * extra_option: Para extender nuevas opciones agregadas.
  * extra_default_value: Para extender nuevos valores por defecto agregados.
  * extra_help: Para agregar cualquier otro extracto de ayuda.

Los tres casos se pueden ver utilizados en el script "phpmyadmin".

Ademas se recomienda definir valores por defecto para al menos las 4 siguientes
variables de ambiente:
  * DOCKERNAME
  * NAME
  * PORT
  * VERSION

Los valores de cada variables se describen en la sección "Variables de ambiente"

Por ultimo es necesario realizar el llamado al template de la siguiente mantera:

```bash
source $DOCKERWRAPPERS_ROOT/.docker_wrapper_template
```

Es muy importante realizar el llamado al template **al final** del script para
evitar posibles colisiones con valores de varialbes seteadas en el template.

## Variables de ambiente.

Se cuenta con las siguientes variables de ambiente definidas en el archivo
.docker_wapper_template:

  * PROG: Nombre del script.
  * NAME: Nombre de la imagen docker utilizada (sin tag).
  * PORT: Puerto de la máquina **host** por el cual se comunica la imagen docker.
  * VERSION: Tag de la imagen docker utilizado.
  * DOCKERNAME: Nombre completo del repositorio utilizado para la imagne docker.
  * OPTION: Opción seleccionada dentro del script (new por ejemplo).
