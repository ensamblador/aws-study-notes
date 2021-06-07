# CodeDeploy

Existen alternativas de **Stop Deployment** y **Stop And Rollback Deployment**


## Canary Deployments:
  - Lambda: 🟢
  - ECS: 🟢
  - ASG: 🔴
  - On-Prem: 🔴

## AppSpec.yml
  - Hooks: Son functiones Lambda
    Hook | Lambda | ECS | EC2
    --- | :---: | :---: | :--:
    ApplicationStop |  |  | ✓
    BeforeInstall |  | ✓ |✓
    AfterInstall |  | ✓ |✓
    AfterAllowTestTraffic |  | ✓ |
    BeforeAllowTrafic | ✓ | ✓ |
    AfterAllowTraffic | ✓ | ✓ |
    ApplicationStart |  |  |✓
    ValidateService |  |  |✓

## On-Prem Deployments:

    - OS: Ubuntu, Windows, RHEL (with Sudo/ Root access)
    - Port : 443
    - IAM Identity with permissions.

## Rollback Behavior with existing content

Como parte del proceso de despliegue, CodeDeploy Remueve de la instancia todos los archivos instalados en el despliegue más reciente. Si aparecen archivos que no son parte del deploy en el ambiente del destino puedes elegir como CodeDeploy reacciona:

- Fallar el displiegue
- Sobrescribir el contenido
- Retener el contenido: Detecta y se mantienen los archivos en el destino y forman parte del paquete de despliegue.








___
# CodePipeline

Acciones el mismo action group se ejecutan en paralelo.

Acciones con el mismo runOrder se ejecutan en paralelo.

## Actions


Action Type | Alternativas 
-- | --
Source | - ECR (se debe usar como accion paralela con con code commit) <br> - S3 <br> - Github, Bitbucket, Code commit
Build | - Codebuild <br> - Cloubees <br> - Jenkins <br> - Teamcity
Test | - CodeBuild <br> - AWS Device Farm <br> - Blazemeeter <br> - Ghost Inspector <br> - MicroFocus SotormRunner Load <br> - Nouvola <br> - Runscope 
Deploy | - S3 <br> - AWS AppConfig <br> - Cloudformation <br> - Cloudformation StackSets <br> - ECS <br> - Elastic Beanstalk <br> - Opsworks <br> - Service Catalog <br> - Alexa Skills Kit <br> - Code Deploy <br> - XebiaLabs 
Approvals | - SNS 
Invoke | - Lambda <br> - Step Functions 
 

___
# CodeBuild

## Buildspac.yml

-  env: Environment variables pueden ser variables de shell, parameter-store, exported-variables, secrets manager
- proxy
- batch
- phases
    - Install
    - pre_build
    - build
        (todas tienen la misma structura)
        - run-as
        - on-failure
        - commands
        - finally
    - post_build
- reports
- artifacts
- cache

## Environtment Variables:
    - Plain Text
    - Parameter
    - Secrets Manager

## Custom Image: 

Es posible usar una imagen custom, tiene que estar en ECR u otro registro.

## Docker Images de CodeBuild:
    - AmazonLinux 2 x86_64
    - AmazonLinux 2 ARM64
    - Ubuntu (18.04 y 20.04)
    - Windows Server Core 2019

## BuildSpec.yml 
### ECR
    - pre-build: commands: $(aws ecr get-login... )
    - build: commands: 
        - docker build
        - docker tag
        - docker push

___
# CodeCommit

Encrypt at rest (KMS) / in transit (TLS)

## Cross Account Access
    1. Admin Account A:
        - Create Policy, Create IAM Role for "Another AWS Account", Attach policy.
    2. Admin Account B:
        - Policy con STS:AssumeRole y resource el ARN del role de account A.
        - Asigna la Policy a los Users 
    3. Usuarios en account B:
        - aws configure --profile MyCrossAccountProfile
        - editar ./aws/config y agregar en el profile:
            - account= Account A
            - role_arn = ARN Role en Account A.


## Aproval Rules
Se pueden crear reglas de aprobación, sin estas aprobaciones no se puede hacer merge.

    1. Crear approval rule template
    2. Aplicar template a los repositorios


## Notificaciones
    FULL o BASIC
    Targets: SNS (debe estar en la misma región el topic)o ChatBot
    Eventos: 
        Comments / Approvals / Pull Requests
        Delete / Create / Update Branch


## Triggers
    Eventos: 
        PUSH / CREATE / DELETE 
        Branch o TAG
    Target: SNS o Lambda

También se pueden crear Event Rules con eventos diferents.

## IAM Stuff:
Para permisos granulares por repo, rama:

    "StringEqualsIfExists": {
        "CodeCommit:References":[
            refs/head/main,
            refs/head/prod
        ]
    } 

**AWSCodeCommitFullAccess**: Administrador
**AWSCodeCommitPowerUser**: Most Users
**AWSCodeCommitReadOnly**: Solo Lectura


# CodePipeline

Build Stage:
    - Codebuild
    - Jenkins (add jenkins provider name and server url)
    - Solano CI


# Codestar

- Crea todo (CCommit, CBuild, CPipeline, CDeploy)
- ElasticBeanstal, EC2, Lambda
- Team (owner, viewer, contributor)
- Jira Connector For ticket System
