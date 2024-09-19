# Crear una copia (fork) del repositorio principal del manual de WordPress en Español a tu cuenta de GitHub


# CREAR UN FORK
Crearemos el fork pinchando en el último botón que aparece en la parte superior derecha, está rodeado en rojo para que puedas localizarlo más fácilmente.

![Crear un Fork]( https://raw.githubusercontent.com/WordPress/spain-handbook/master/assets/Fork-crear.jpg)

Después de realizarlo, la ventana cambiará y si nos fijamos en la ruta que se muestra en la parte de arriba a la izquierda ya aparecerá nuestro nombre de usuario, desde este momento cualquier cambio que hagamos en este repositorio, no afectará al repositorio original hasta que no hagamos un Pull request (solicitud de revisión) y éste no sea verificado y aprobado.

![Estamos en nuestro Fork](https://raw.githubusercontent.com/WordPress/spain-handbook/master/assets/Fork-estamos-en-fork.jpg)

## Sincronizar nuestra copia con el repositorio original

### Fetch upstream {#fetch}

**Si nuestro *fork* deja de estar actualizado**

Cuando se trabaja en un _fork_, se trabaja paralelamente al repositorio principal (wordpress/spain-handbook) en tu cuenta de github (micuenta/spain-handbook). 

Por tanto es posible que, mientras estés trabajando, otros contribuidores estén haciendo lo mismo en sus respectivos forks y hayan mandado los cambios al repositorio principal. Esos cambios no se aplicarán en tu fork mientras no sincronices tu repositorio con el principal.

De hecho, verás un mensaje como el siguiente:

`This branch is 3 commits behind WPES:master`

Significa que se han realizado 3 modificaciones desde que hicimos nuestra copia (*fork*).

En este caso, si el archivo principal se ha adelantado a nuestra versión, tenemos dos opciones: Contribute o Update branch.
Si no hemos realizado aun cambios en nuestro fork, para trabajar en la versión aceptada más actualizada del archivo principal (main), podemos pulsar en *Sync fork*, que nos dará a su vez la opción: _Update branch_.
![Actualizamos Rama](https://raw.githubusercontent.com/WordPress/spain-handbook/master/assets/Fork-actualizar-rama.jpg)

Si ya hemos editado nuestro archivo, pulsaremos Contribute, aparecerá una pequeña ventana que indica que el archivo no está actualizado y nos invita a hacer un Pull request para fusionar nuestra edición con el archivo principal (main).
![Solicitamos Pull Request](https://raw.githubusercontent.com/WordPress/spain-handbook/master/assets/Fork-contribute-send-PR.jpg)

*Compare* nos permite comparar las distintas versiones que se han creado.
En cualquier caso, si hubiera algún conflicto entre ambas versiones, el sistema nos avisará y nos invitará a hacer antes un *Pull request*.


