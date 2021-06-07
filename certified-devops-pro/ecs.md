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


## Uso de secrets

### Secrets Manager

Es posible usar secret manager pasando como valor en el campo Secrets

```json 
{
  "containerDefinitions": [{
    "secrets": [{
      "name": "environment_variable_name",
      "valueFrom": "arn:aws:secretsmanager:region:aws_account_id:secret:appauthexample-AbCdEf:username1::"
    }]
  }]
}
```

### Parameter Store

```json
{
  "containerDefinitions": [{
    "secrets": [{
      "name": "environment_variable_name",
      "valueFrom": "arn:aws:ssm:region:aws_account_id:parameter/parameter_name"
    }]
  }]
}
```
    


### Container Agent

* Instalado automaticamente en ECS-Optimized AMI
* Se puede instalar en otras AMI
* Viene instalado y administrado por AWS en caso de Fargate Launch Type


### Cloudwatch Logs

