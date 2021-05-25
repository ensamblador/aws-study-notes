# Auto Scaling Group

## Life Cicle Hooks

EC2_INSTANCE_LAUNCHING
- Pending:Wait
- Pending:Proceed

EC2_INSTANCE_TERMINATING
- Terminating:Wait
- Terminating:Proceed

Es posible agregar un LCH en Terminating:Wait para ejecutar acciones antes de terminar la instancia. Se debe crear un Cloudwatch Event Rule y ejecutar un Documento de Automation.

## Balance entre SPOT y Ondemand

Launch templates permiten definir un porcentaje entre Spot y Ondemand como también varias familias y tamaños.

## Set Instance Health

`aws autoscaling set-instance-health` permite informar la salud de la instancia al asg

## Notificaciones

asg puede notificar a un SNS topic:
- Launch
- Terminate
- Failed

## Cómo aislar una instancia defectuosa?
1. Disable health checks from ELB en el asg config
2. Put instance in stand ny para removerla temporalmente del asg.