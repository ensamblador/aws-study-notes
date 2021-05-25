# Application discovery service

- Import CSV
- Agentless
- Agent Windows / Linux
    - requiere Access Key / Secret Key de usuario IAM
    - Managed Policy ApplicationDiscoveryAgentAccess


# EC2 VM Import / Export

Puede importar una imagen de S3 y crear ina AMI o una instancia.

OVA, VMDX (VMWare), VHDX (Hyper-v), RAW


_aws cli comandos para exportar OVA, VMWare o Hyper-V_ 👇
```bash
aws ec2 start-export-task
aws ec2 export-image
```
