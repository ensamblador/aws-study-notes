# Auto Scaling Group

## Life Cicle Hooks

EC2_INSTANCE_LAUNCHING
- Pending:Wait
- Pending:Proceed

EC2_INSTANCE_TERMINATING
- Terminating:Wait
- Terminating:Proceed

Es posible agregar un LCH en Terminating:Wait para ejecutar acciones antes de terminar la instancia. Se debe crear un Cloudwatch Event Rule y ejecutar un Documento de Automation.