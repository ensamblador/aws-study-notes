# Cloudformation

## General:
- Cuando se pasa una AMI como *Parameter* se debe limitar a AWS::EC2::Image::Id
- Cuando una BD RDS se debe borrar o actualizar se puede pasar el DBSnapshotIdentifier = ARN del Snapshot Manual.

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
