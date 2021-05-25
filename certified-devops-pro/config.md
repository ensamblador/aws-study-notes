# Config

## Rules
- Managed By Config
- Lambda

### Trigger
- Configuration changes (All, resource, Tags)
- Periodic (1,3,6,12,24H)



## Remeditation

<div style='border:1px solid gray; padding:10px'>
AWS System Manager Automation
</div>

## Notificaciones 

Se puede establecer configuration change, compliance change, etc. En Cloudwatch events
Tambien se puede desde config notificar a un SNS Topic a nivel de cuenta (no a nivel de regla)

### Configuration Timeline

    Todos los cambios

### Compliance Timeline

    Todos los cambios de compliance

## Algunas reglas
- Restricted SSH: Verifica si los SG Permiten el acceso sin restricciones
- Restricted-common-ports: Verifica sin los SG permiten el acceso sin restricciones en los puertos más comunes.
- approved-amis-by-id, approved-amis-by-tag: SI las AMI que usa EC2 están aprobadas.
