# Systems Manager

## Enrolar instancias en un entorno híbrido

1. Crear un Service Role con las politicas necesarias
2. Crear e instalar un certificado TLS en los servidores on-premises y VMWare
3. Crear una managed instance (mi-) activation.
    1. En la consola se indica el rol 
    1. Cuando Se activan se recive un activation code y un activation ID
    2. Instalar el agente, Se usan estos datos en la instalación del SSM Agent
