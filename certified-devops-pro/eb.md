# Elastic Beanstalk


## Language support

- Languages: Go / Java / PHP / Nodejs /Python  / Ruby 
- Containers: Docker
- Application Servers: Tomcat / Passenger / Puma

## Environments

Aplicaciones corren en los envs, cada env puede tener varias versiones de la misma app.

Versiones se almancenan en s3.

Limite de 1000 app versions total.

Logs se almacenan en s3. O logs en tiempo real a cloudwatch o x-ray.

SNS para notificaciones y manejo de eventos.

Auto Heal: descansa en ELB y ASG.

Persisten Store: Las instancias no tienen persistencia de data, se debe configurar la aplicación para almacenar datos persistentes fuera del env (ej S3, EFS, DynamoDB, RDS)

## Deployments
- Blue/Green: Swap-URL, hay que Desacoplar BBDD, ojo con el TTL.
- All at Once
- Rolling
- Rolling with additional batch
- Immutable

## Folder Structure

    |--App
        |--.ebextensions
            |-- *.config
        |--.elasticbeanstalk
            |-- saved_configs
            |-- config.yaml
        |app-files  

**_ebextensions_**: JSON o YAML files, Comandos shell o de aplicacióm. Se ejecutan en orden alfabético.<br>

**_saved_config_**: configuración del environment, si se requiere reutilizar la configuración.

### Source Code Bundle

- puede incluir un cron.yaml para programar periódicamente
- No debe exeder 512 MB
- zip o war file
- no incluir directorios superiores (parent)

### .ebextensions config file structure
- packages: yum, rubygems, python, rpm (el orden dentro de un package manager no está garantizado)
- groups
- users
- sources : para descargar un archivo y descomprimirlo
- files
- commands: comandos que se ejecutan antes de que la aplicacion y el servidor estén configurados. Corren como root, en orden alfabético.
- services: servicios que se deben correr
- container_commands (leader_only:BOOL): corren antes de que se despliegue la aplicación pero después de la extracción y configuración.

### dockerrun.aws.json

Archivo asociado a eb, se define como se corren los contenedores en la instancia EC2 que corre docker engine. Las secciones son versio, volumes y container definition (es como el task definition pero en eb)

Usar V2 para multicontainer.

## Configuration Precedence

1. aplicados en la consola o en la cli/sdk
2. saved configurations (eb create --cfg configfile)
3. .ebextensions
4. default values

## eb cli
- eb init
    - eb create
        - eb logs
        - eb status
        - eb events
    - eb deploy


## RDS Decoupling

Hay que Conectarse de Forma externa, una manera es:
1. Tomar un snapshot de la RDS y habilitar deletion protection+
2. Configurar un nuevo env y conectarse a la RDS
3. Desasociar el SG del Env original
4. Borrar el env original.


## Managed Updates

- No downtimes or reduced Capacity
- Configurable maintenance window


## [Aplication Version Lifecycle](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/applications-lifecycle.html)

Dado que las versiones de las aplicaciones no pueden ser más de 1000, es posible configurar una política de ciclo de vida de aplicación para borrar las versiones después de un cierto umbral o después de cierta antigüedad.
