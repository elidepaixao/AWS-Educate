# ☁️ AWS Educate: Introdução a Cloud Computing 101

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![EC2](https://img.shields.io/badge/Amazon%20EC2-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![S3](https://img.shields.io/badge/Amazon%20S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white)

Este repositório documenta meus estudos e anotações do laboratório de **Introdução à Cloud Computing 101** da AWS. O material cobre conceitos fundamentais de nuvem, modelos de serviço, modelos de implantação e um guia prático de demonstração do Amazon S3.

---

## 📖 O que é Computação em Nuvem?

**Definição:** Computação em nuvem é a entrega de recursos de TI **sob demanda** pela internet com definição de preço com pagamento conforme o uso.

### ⏳ Breve Histórico (AWS)
* **2002:** A AWS inicia a nuvem pública.
* **2006:** Lançamento do Amazon EC2 para o público.
* **2008:** Criação de data centers.
* **2015:** ISO publica os primeiros padrões para nuvem.

### 🖥️ Modelo Cliente-Servidor
* **Cliente:** Navegador web ou aplicação desktop com o qual um usuário interage para fazer solicitações a servidores de computador.
* **Servidor:** Exemplo: **Amazon EC2**, que atua como um servidor virtual na nuvem.

### ✨ Benefícios da Computação em Nuvem
1. **Trocar despesas iniciais por despesas variáveis:** Pagar apenas pelos recursos de computação que você consome. Não precisa investir em data centers físicos.
2. **Parar de gastar dinheiro:** Com a execução e manutenção de data centers.
3. **Parar de tentar adivinhar a capacidade:** Não precisa prever a capacidade de infraestrutura antes de implantar uma aplicação.
4. **Aumentar a velocidade e agilidade:** Pode acessar novos recursos em poucos minutos.
5. **Ter alcance global em minutos.**

---

## 🏗️ Modelos de Computação em Nuvem

* **IaaS (Infraestrutura como Serviço):** Engloba os componentes básicos de TI na nuvem. Recursos disponibilizados: rede, computadores (virtuais ou em hardware dedicado) e espaço de armazenamento de dados. 
  * *Exemplos da Amazon:* EC2, S3, RDS e Route 53.
* **PaaS (Plataforma como Serviço):** Elimina a necessidade de as organizações gerenciarem a infraestrutura subjacente (hardware e SO). Elas podem se concentrar na implementação e gerenciamento de aplicações. 
  * *Exemplo da Amazon:* AWS Elastic Beanstalk (implementa e dimensiona aplicações web rapidamente).
* **SaaS (Software como Serviço):** Produto de software completo que o provedor de serviços executa. 
  * *Exemplos:* Microsoft 365, Slack, Zoom, Salesforce, SAP, Google Drive, Shopify, Wix, Canva, Figma...

## 🌍 Modelos de Implementação
* **Nuvem:** Migra as aplicações ou cria novas 100% na nuvem.
* **Híbrida:** Integra recursos baseados na nuvem a aplicações de TI legadas.
* **On-premises:** Implementação de nuvem privada (infraestrutura local).

---

## 🪣 Laboratório: Demonstração do Amazon S3

Passo a passo prático para criação de buckets, adição de objetos e compartilhamento no **Amazon S3**.

### 1. Criar Bucket S3
No console da AWS, digite `S3` e siga os passos:
1. Clique em **Create bucket**.
2. **Bucket name:** precisa ser único globalmente.
3. **AWS Region:** escolha uma região.
4. **ACLs disabled:** garante a segurança dos objetos.
5. **Block Public Access:** selecione `Block all` (garante o bloqueio do acesso público ao bucket num primeiro momento).
6. **Bucket Versioning:** Disable.
7. **Default encryption:** Disable.
8. Clique em **CREATE BUCKET**.

### 2. Enviando Arquivos para o Bucket
1. Clique no nome do bucket criado no primeiro passo.
2. Clique no botão **UPLOAD** -> `Add Files` (ou `Add folder`, ou simplesmente arraste e solte os arquivos).

### 3. Compartilhar Arquivos (Configurando Permissões)
Para compartilhar os arquivos carregados, é necessário editar as permissões de segurança:

1. Clique no Nome do bucket -> Aba **Permissions**.
2. Vá em **Block public access** -> `Edit` -> `Disable` (Desmarque a opção de bloqueio total).
3. Vá em **Edit bucket policy** -> Cole o arquivo JSON abaixo (não esqueça de alterar `nomedobucket` para o nome real do seu bucket):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": [
        "arn:aws:s3:::nomedobucket/index.html",
        "arn:aws:s3:::nomedobucket/css/*",
        "arn:aws:s3:::nomedobucket/images/*"
      ]
    }
  ]
}
```

4. Clique em **SAVE CHANGES**.
5. Volte nos arquivos anexados, clique neles, copie a URL e cole no navegador: *o arquivo estará disponível publicamente!*

---
---

## 💻 Laboratório: Demonstração do Amazon EC2

**Iniciar uma Instância EC2:**
Uma instância é um servidor virtual na nuvem AWS. O objetivo deste laboratório é configurar uma instância de servidor Linux.

### 1. Acessando o EC2 e Escolhendo a Imagem (AMI)
No console da AWS, digite `EC2` e siga os passos:
1. Vá no **EC2 Dashboard** -> clique em **Launch instance**.
2. **Name and tags:** Escolha um nome para a sua instância e clique em `Add additional tags` se necessário.
3. **Application and OS Images (AMI):** Selecione **Amazon Linux** (AWS).
4. Certifique-se de que a opção **Free tier eligible** (elegível para o nível gratuito) esteja selecionada.

### 2. Tipo de Instância e Par de Chaves (Key Pair)
1. **Instance type:** Escolha `t2.micro` (Free tier eligible). 
   * *Nota: É o tipo de instância que define a memória, CPU, armazenamento e capacidade de rede.* Deixe a máquina virtual de hardware padrão (HVM).
2. **Key pair (login):** Clique em **Create new key pair**.
3. **Key pair name:** Escolha um nome (pode ser o mesmo nome do EC2).
4. **Key pair type:** `RSA`
5. **Private key file format:** `.pem` (OpenSSH).
6. Clique em **Create key pair**.
   * ⚠️ *O arquivo de chave privada é baixado automaticamente no navegador. Salve em um local seguro! O EC2 armazena a chave pública na instância e você armazena a chave privada.*

### 3. Configurações de Rede (Network Settings)
Uma VPC padrão é criada em cada região. Uma Nuvem Privada Virtual (VPC) permite definir uma rede virtual.
1. Em **Network settings**, clique em **Edit**.
2. **VPC - required info:** Selecione sua própria VPC, que estará na lista para definir onde a instância EC2 será executada.
3. **Subnet:** Selecione a sub-rede desejada.
4. **Auto-assign public IP:** O campo de IP público não é ativado automaticamente. Altere para **Enable** (Ativar), já que a instância será executada em um servidor web público.

### 4. Firewall e Security Groups
1. Selecione **Create security group**.
2. Altere o nome para o nome da instância utilizada e preencha a **Description - required** (nomeie).
3. **Regras de SSH:** 
   * A opção padrão é `Allow SSH traffic from -> Anywhere`. Vamos mudar a origem de acesso SSH para **My IP**. Apenas este endereço IP terá acesso pela porta 22.
4. **Regras de HTTP/HTTPS:**
   * Marque a caixa ☑️ **Allow HTTPS traffic from the internet**.
   * Marque a caixa ☑️ **Allow HTTP traffic from the internet**.
   * *Configuração manual:* `Security group rule` -> `Add Security Group` -> Type: `HTTP` -> Source type: `Anywhere`.

### 5. Configurar o Armazenamento (Storage)
1. Configure o volume raiz (Root volume) como: `1x [ 10 ] GiB [ gp2 ]`.
2. Se necessário, você pode clicar em `Add new volume`.

### 6. Lançamento da Instância
1. Revise tudo no painel **Summary** (à direita).
2. Clique no botão **Launch instance**.
3. Clique em **View all instances**.
4. Acompanhe o **Instance state**: para estar pronta para uso, o status deve mudar para `"Running"`.

---
