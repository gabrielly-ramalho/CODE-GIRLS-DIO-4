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
  AWSTemplateFormatVersion: '2010-09-09'
Description: Template básico - EC2 + S3 + Security Group

Parameters:
  KeyName:
    Description: Nome da chave SSH para acessar a instância EC2
    Type: AWS::EC2::KeyPair::KeyName

  InstanceType:
    Description: Tipo da instância EC2
    Type: String
    Default: t2.micro
    AllowedValues:
      - t2.micro
      - t2.small
      - t3.micro
    ConstraintDescription: deve ser um tipo de instância EC2 válido.

Resources:
  MeuBucketS3:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Sub 'meu-bucket-dio-${AWS::AccountId}-${AWS::Region}'
      VersioningConfiguration:
        Status: Enabled

  MeuSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Permite acesso SSH (porta 22)
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
      VpcId: !Ref VpcId

  MinhaInstanciaEC2:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !Ref InstanceType
      KeyName: !Ref KeyName
      ImageId: ami-0c55b159cbfafe1f0 # Amazon Linux 2 (verifique a região)
      SecurityGroupIds:
        - !Ref MeuSecurityGroup
      Tags:
        - Key: Name
          Value: InstanciaDIO

  VpcId:
    Type: AWS::EC2::VPC::Id
    Description: ID da VPC onde os recursos serão criados

