# 🚀 Implementando Infraestrutura Automatizada com AWS CloudFormation

## 📘 Descrição do Projeto
Este repositório contém o desafio da **Digital Innovation One (DIO)**: *Implementando Infraestrutura Automatizada com AWS CloudFormation*.

O objetivo é aplicar os conceitos de **Infraestrutura como Código (IaC)** utilizando o serviço **AWS CloudFormation**, criando uma infraestrutura completa na nuvem de forma automatizada e reprodutível.

---

## 🎯 Objetivos de Aprendizagem
- Entender o funcionamento do AWS CloudFormation.  
- Criar templates YAML para provisionamento automático de recursos AWS.  
- Diferenciar CloudFormation e Terraform.  
- Aplicar boas práticas de documentação técnica e versionamento com GitHub.

---

## ⚙️ Estrutura do Projeto

```
desafio-aws-cloudformation/
│
├── README.md               # Documentação principal
├── template.yaml            # Arquivo do modelo CloudFormation
├── notas.md                 # Anotações e aprendizados
└── /images/                 # Pasta para capturas de tela do projeto
```

---

## 🧱 Template CloudFormation (`template.yaml`)

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Template para criação de infraestrutura automatizada básica na AWS

Resources:
  MyVPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsSupport: true
      EnableDnsHostnames: true
      Tags:
        - Key: Name
          Value: DIO-VPC

  MySubnet:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref MyVPC
      CidrBlock: 10.0.1.0/24
      MapPublicIpOnLaunch: true
      Tags:
        - Key: Name
          Value: DIO-Subnet

  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Acesso SSH e HTTP
      VpcId: !Ref MyVPC
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
      Tags:
        - Key: Name
          Value: DIO-SG

  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-08c40ec9ead489470
      InstanceType: t2.micro
      KeyName: my-key-pair
      SubnetId: !Ref MySubnet
      SecurityGroupIds:
        - !Ref MySecurityGroup
      Tags:
        - Key: Name
          Value: DIO-Instance

  MyS3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: dio-cloudformation-bucket-${AWS::AccountId}
      VersioningConfiguration:
        Status: Enabled
      Tags:
        - Key: Name
          Value: DIO-Bucket
```

---

## 🧾 Passo a Passo de Execução

1. Acesse o **AWS Console** → **CloudFormation**.  
2. Clique em **Create Stack → With new resources (standard)**.  
3. Faça upload do arquivo `template.yaml`.  
4. Nomeie a stack (exemplo: `DIO-Automation-Stack`).  
5. Aguarde a criação e confirme a infraestrutura criada.

---

## 💡 Comparativo CloudFormation vs Terraform

| Recurso | CloudFormation | Terraform |
|----------|----------------|------------|
| Escopo | Exclusivo da AWS | Multi-cloud |
| Linguagem | YAML/JSON | HCL |
| Armazenamento de estado | AWS Service integrado | Arquivo local/remoto |
| Integração | Nativa com AWS | Requer provedores externos |

---

## 💬 Aprendizados e Insights
- CloudFormation é uma ferramenta essencial para quem deseja dominar automação de infraestrutura na AWS.  
- Com ele, é possível garantir versionamento e reprodutibilidade dos ambientes.  
- É uma abordagem alinhada ao conceito **DevOps** e **Infraestrutura como Código (IaC)**.

---

## 🔗 Links Úteis
- [Documentação AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)  
- [GitHub Markdown Guide](https://guides.github.com/features/mastering-markdown/)  
- [DIO - Digital Innovation One](https://www.dio.me)

---

## 👨‍💻 Autor
Desenvolvido por **[Seu Nome Aqui]**  
Desafio da **Digital Innovation One (DIO)** — *Implementando Infraestrutura Automatizada com AWS CloudFormation*.
