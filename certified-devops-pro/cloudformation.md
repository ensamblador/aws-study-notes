# Cloudformation

## UpdatePolicy:
- AutoScalingReplacingUpdate: WillReplace: Boolean

    Indica como se tratará las actualizaciones que requieran remplazo, willreplace: True indica que se debe crear otro ASG. (Facilita el rollback)

- AutoScalingRollingUpdate:

    Indica como se tratan los rolling updates, MaxBatchSize, MinInstance in service etc.

    