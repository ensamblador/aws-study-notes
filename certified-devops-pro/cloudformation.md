# Cloudformation

## General:
- Cuando se pasa una AMI como *Parameter* se debe limitar a AWS::EC2::Image::Id
- Cuando una BD RDS se debe borrar o actualizar se puede pasar el DBSnapshotIdentifier = ARN del Snapshot Manual.
- `list-stacks` permite ver los stacks que se han borrado en los últimos 90 días también.
- Cloudsearch no está soportado por cloudformation.
- Passwords: NoEcho=true
- AWS::CodeCommit::Repository permite un parámetro `code` que es el codigo en s3 (zip) y el nombre de la rama para el primer commit (sólo cuando se crea)

## SSM::Parameter en Parameter section

Se puede hacer referencia al valor de un parameter en parameter store 

```yaml
Parameters:
    LatestAmiId:
        Type: 'AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
        Default: '/aws/service/ami-windows-latest/Windows_Server-2016-English-Core-Containers'
...
Resources :
  Instance :
    Type : 'AWS::EC2::Instance'
    Properties :
      ImageId : !Ref LatestAmiId

```

```
"ResolvedValue": "ami-ba9c05c0"
```

## UpdatePolicy:
- AutoScalingReplacingUpdate: WillReplace: Boolean

    Indica como se tratará las actualizaciones que requieran remplazo, willreplace: True indica que se debe crear otro ASG. (Facilita el rollback)

- AutoScalingRollingUpdate:

    Indica como se tratan los rolling updates, MaxBatchSize, MinInstance in service etc.


## Stack Policy

Previene la actualización de recursos usando una política de Stack (Json)
- Actions => Update: Modify, Replace, o Delete
- Principal, conditions, effect.
(muy similara una a IAM Policy o Resource Policy)

## Custom Resources
- Es la forma de incorporar custom resources a Cloud Formation Stack.


## Intrinsic Functions

Se puede usar en 
* Resource Properties
* outputs
* metedata attributes
* update policy attributes
* tambien para crear stack resources


## Creation Policy (EC2 y ASG)
Es posible definir una propiedad `CreationPolicy` para indicar a Cloudformation que espere ciera condición de señales desde las instancias antes de dar el recurso como creado.

```json
"AutoScalingGroup": {
  "Type": "AWS::AutoScaling::AutoScalingGroup",
  "Properties": {
    ...
  },
  "CreationPolicy": {
    "ResourceSignal": {
      "Count": "3",
      "Timeout": "PT5M"
    }
  }
}
```
después se usa `cfn-init`, `cfn-signal` para mandar esa señal

```json
"UserData": {
  "Fn::Base64": {
    "Fn::Join" [ "", [
      "/opt/aws/bin/cfn-init ",
      ...
      "/opt/aws/bin/cfn-signal -e $? ",
      "  --stack ", { "Ref": "AWS::StackName" },
      "  --resource AutoScalingGroup " ,
      "  --region ", { "Ref" : "AWS::Region" }, "n"
    ] ]
  }
}
```

## StackSets

Puedes desplegar en otras cuentas o Unidades organizativas / Regiones.

### Actualizacion de algunas regiones / accounts

- Seleccionar Override stackset parameters
- Seleccionar regiones / accounts a sobreescribir
- En los parámetros seleccionar el valor a sobreescribir


## Template Validation

- using **`aws cloudformation validate-template`** para revisar la sintaxis (pero no valida valores de parámetros son válidos)
- usar un ambiente de testing para ver si el templata falla.
