# CODE-GIRLS-DIO-4
3° DESAFIO DO BOOTCAMP CODE GIRLS DIO

Aprendizados que tive com CloudFormation
## Objetivo
Consolidar conhecimentos em CloudFormation com prática real.

## Tecnologias Utilizadas
- AWS CloudFormation
- AWS EC2
- AWS S3
- YAML / JSON

##  O que aprendi
- Escrever templates em YAML
- Criar infraestrutura como código 
- Testar e validar stacks no CloudFormation

## Exemplo de template da prática
Bucket S3

    AWSTemplateFormatVersion: '2010-09-09'
    Description: Template para criar um bucket S3 com versionamento ativado
    
    Resources:
      MeuBucketS3:
        Type: AWS::S3::Bucket
        Properties:
          BucketName: !Sub 'meu-bucket-dio-${AWS::AccountId}-${AWS::Region}'
          VersioningConfiguration:
            Status: Enabled
    
    Outputs:
      NomeDoBucket:
        Description: Nome do bucket S3 criado
        Value: !Ref MeuBucketS3
