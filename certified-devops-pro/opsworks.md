# Opsworks

## General

- Puede correr instancias fuera de opsworks como instancias EC2 u on-prem (pero deben ser de las distribuciones Linux soportadas, no soporta windows on-prem)

- API **`DeploymentCommand`** se usa para especificar un comando stack o deploy.
    - Stacks:
        - execute_recipes
        - install_dependencies
        - update_custom_cookbooks
        - update_dependencies 
    - apps:
        - deploy
        - rollback
        - start
        - stop
        - restart
        - undeploy 

- Berkshelf: Dependency manager Una forma de traer custom cookbooks a opsworks y que berkshelf maneje las dependencias.


### Stacks 

Compuesto por *layers* que se arman usando *recipes* definen Network / Seguridad / Discos / logs
| OS |
|--|
| Linux and Windows|

Un stack puede correr instancias linux o windows, pero no mezclar.

- **_`Cuando se crean los stack se pueden configurar para que utilicen custom cookbooks`_**
- **_`es posible instalar docker utilizando custom cookbooks`_**

*Applications* se despliegan

### Scaling
- 24/7
- Time Based
- Load Based (Cpu, Ram, Load) [Linux] 



### Auto-healing
- Agente instalado
- Heartbeat
- Despues de ciertos segundos, failed instance y la reemplaza
- Opsworks espera 5 minutos para una instancia antes de considerarla fallida.

### Security

Puede manejar un set de permisos independientes de IAM (ej: Sudo en la instancia, admin, deploy, etc.)

### ELB (Classic)

- Se crea aparte
- 1 x Stack
- CLB
- No puede tener instancias previamente (de desregistran las actuales)

### Service Layers (ECS, RDS)

Estos servicios se agregan al stack pero existen previamente.

#### RDS

Se agregan a la App y opsworks crea un archivo de conexión en cada instancia (linux stacks). Se puede implementar un custom recipe para extraer esta información y pasarla a la instancia en un archivo.

En linux, Hay que asociar el driver package adecuado para la conexión con la BBDD

## Lifecycle Events

Event | Cuando | 
--- | :--- 
Setup | Post instance Boot, instance is offline
Configure | Instance Leaves or Enter Online (se ejecuta an todas las instancias)
Deploy | Deploy app App from repo to instances
UnDeploy | Undeploy App
Shutdown | Prior to instance Termination (cleanup)

Se pueden ejecutar custom recipes en cualquier Lifecycle event (cookbook::recipename). 

Se pueden ejecutar comandos en un lifecycle event con **Run Command**

### Data Bags

(Chef Concept) Configuraciones en json que dicen como se despliega la aplicación y otras configuraciones.


### EventBridge 
    # Para ser notificado cuando se ejecute un auto-heal
    source: aws.opsworks
    detail: initiated-by: [auto-healing]


## Otras Versions

| Opsworks Flavor | Features 
|--| --
| Opsworks For Chef Automate|  - setup automate server <br> - use community cookbooks <br> - Chef native tools <br> - you can ssh to automate server <br> - control your network (VPC)|
| Opsworks For Puppet Enterprise | - Puppet master server <br> - can ssh server <br> - control network (VPC)
