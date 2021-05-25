# Lambda

## Versions

Weigthed alias permite enviar cierta cantidad de tráfico a un Alias y el resto al otro. Útil para Canary.

## Lambda@edge

Codigo de Node.js o Python  que se ejecuta en cloudfront en lo siguientes eventos.

Solo Se pueden agregar triggers a la función en us-east-1 (virginia)

- Viewer request
- Origin request
- Origin response
- Viewer response

0,60 USD por millón de solicitudes + 0,00005001 USD por cada GB-segundo utilizado

## Cloudfront Functions

Cuando se agrega una cloudfrony function a la cloudfront distribution, CF intercepta el request y la respuesta em las ubicaciones edge y se las pasa a la funcion

* Cuando recibe el request (viewer request)
* Cuando recibe el response (viewer response)

Codigo de Javascript ECMAScript 5.1 y 6.

Se crean en la consola de Cloudfront.

0,10 USD por millón de invocaciones

Comparativa https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/edge-functions.html
