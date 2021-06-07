# RDS 

## Snapshots

Automated snapshots cannot be shared. Only manual snapshots

### Copia a otra región

> - Hasta 5 snapshot copy request por region / account.
> - Dependiendo de la data y las regiones puede tomar horas en completar.
> - Puede haber muchos requests, entonces se encolan pero no hay inidicador de este encolamiento. 


### Copia de Snapshots compartidos

> Si esta encriptado sólo se puede copiar a la misma región, si no está encriptado se puede copiar a diferentes regiones.

### Encriptación

> - La copia de un snapshot encriptado debe estar encriptada tambien.
> - Si la copia es en la misma region, puede usar la misma CMK. Pero si es en otra región se debe especificar una CMK de la región de destino.
> - Una copia de un snapshot no encriptado se puede copiar (para encriptar bases de datos)

### Copia de Snapshots incrementales

> - Son más rápidos porque copian sólo los cambios.
> - Condiciones:
>   - Se ha copiado un snapshot a la region de destino previamente.
>   - La mas reciente copia de snapshot existe en la region de destino
>   - Las copias no estan encriptadas, o  estan encriptadas con la misma CMK. 
>   - Para snapshots compartidos, los incrementales solo están soportados para snapshots no encriptados.


### Options Groups y Parameter Groups

No se copian, deben existir en la región de destino (recomendado con los mismos settings)


## Actualización de Motor

> - Crear read Replica, opcionalmente y recomendable habilitar Multi-AZ y Backups para esta read replica.
> - Actualizar la read replica al engine version.
> - Create read replica from read replica.
> - Promote read replica to standalone DB.


## IAM DB Access

Permite establecer accesos a través de IAM Roles en vez de contraseñas.
Funciona con Aurora (MySQL PostgreSQL) y RDS MySQL


## Aurora Global Database

- Global Read, Local Latenci
- Scalable Secondary
- PostgreSQL y MySQL
- Fast Replication Lower RPO, RTO


## Aurora Multi Master
- En el cluster hay varios writers y se replican todos contra todos (Mesh)
- Todas en la misma region
- No se puede habilitar cross-region replicas
- No tiene integración con otros sevicios de AWS como Lambda, S3, IAM
- No se puede habilitar el clonado, backtrack


## Aurora Replicas (cluster)

- Hasta 15 Replicas
- Automatic Failover
- Se distribuyen en distintas AZ
- Replica Lag < 100ms

Para crear un reader => add Reader (en la consola)

## Aurora Read Replicas

- Usa Binglog replication
- Hasta 5 RR
- Puede ser en otra región
