# CloudWatch

## Event Bridge

Es cloudwatch events + custom event buses + third party events.

Se pueden crear event rules para aws health y generar un trigger.

### Event buses

add pemission: 
- AWS ACCOUNT
- AWS ORGANIZATION

Para filtrar eventos de una cuenta:

`{"accountId": ["11111111111"]}`

#### Partner event bus

Se debe crear 1 event bus por SaaS partner.



### API Calls

Para que cloudwatch pueda detectar API Calls, primero se debe habilitar cloudtrail. Incluidos los eventos de data como


## Cloudwatch Logs

### Puede crear un subscription filter
- Elasticsearch
- Lambda
- Kinesis Firehose (cross account)
- Kinesis Stream (cross account)




### Puede crear un metric filter

Puede crear una métrica a partir de un filtro (ejemplo error 404)

### Puede Exportar a s3

## Cloudwatch metrics

`put-metric-data --storage-resolution` indica la resolución de la data (1s, 60s, etc)
`statistical-values`indica los valores agregados inmediatamente (no los calcula cw)

# Dashboards

Puede tener un dashboard único y ver todas las regiones ahí.

