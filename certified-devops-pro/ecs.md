# ECS

ECS puedes ser target directo de Cloudwatch event rule a nivel de Task.

## ECS Agent

Viene instalado en AMI Optimizadas para ECS, se puede instalar en EC2 (AL, Ubuntu, Windows).

**Soportado Solo en instancias EC2**


## Deployment Types

|Deployment| Proveedor | Opcion
|--|--|--
|Rolling Update|ECS| _minimumHealthPercent, maximumPercent_
|Blue/Green <br> Necesita 2 target Groups. No soportado con Classic Load Balancer)|CodeDeploy|_Canary_: trafico se cambia en 2 incrementos <br> _Linear_ Trafico se cambia en incrementos lineales <br> _all-at-once_: Todo el tráfico se cambia de una.
|External| Cualquiera | Utilizando API ECS.


## Actualizacion de Docker Container en las tareas actuales:

Para actualizar las tareas en curso se utiliza _"Force New Deployment"_ para que las tareas vuelvan a descargar la última versión del contenedor.

Otra alternativa es reiniciar el container agent:


**`sudo systemctl restart ecs`**