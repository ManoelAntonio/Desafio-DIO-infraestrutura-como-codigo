# Desafio-DIO-infraestrutura-como-codigo
Infraestrutura como código: Script de criação de estrutura de usuários, diretórios e permissões

Para criar uma infraestrutura como código para automatizar a criação de usuários, diretórios e permissões, podemos usar ferramentas
como o Terraform ou o CloudFormation da AWS.
Essas ferramentas permitem que você defina sua infraestrutura como código e gerencie sua infraestrutura como um aplicativo.

Aqui está um exemplo de como criar uma infraestrutura de usuários, diretórios e permissões com o Terraform:

#01-Definir as variáveis: Defina as variáveis necessárias para o script. Por exemplo, o nome do usuário, nome do grupo, nome do diretório e permissões.

(go)

  variable "user_name" {
  type = string
}

variable "group_name" {
  type = string
}

variable "dir_name" {
  type = string
}

variable "dir_permission" {
  type = string
}


#02-Criar um recurso de grupo: Crie um recurso de grupo com o nome do grupo especificado.

(csharp)

  resource "aws_security_group" "group_name" {
  name_prefix = var.group_name
}



#03-Criar um recurso de usuário: Crie um recurso de usuário com o nome do usuário especificado e adicione-o ao grupo criado anteriormente.

(Java)

  resource "aws_iam_user" "user_name" {
  name = var.user_name
}

resource "aws_iam_user_group_membership" "user_group" {
  user = aws_iam_user.user_name.name
  groups = [aws_security_group.group_name.name]
}



#04-Criar um recurso de diretório: Crie um recurso de diretório com o nome do diretório especificado e atribua as permissões especificadas.

(Java)

  resource "aws_s3_bucket" "dir_name" {
  bucket = var.dir_name

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Sid = "PublicRead"
        Effect = "Allow"
        Principal = "*"
        Action = ["s3:GetObject"]
        Resource = ["arn:aws:s3:::${var.dir_name}/*"]
      },
    ]
  })

  acl = var.dir_permission
}


#05-Executar o script: Após definir todas as variáveis e recursos, execute o script para criar a infraestrutura.

(csharp)

  terraform init
terraform apply


Com este exemplo, você pode criar facilmente uma infraestrutura de usuários, diretórios e permissões usando o Terraform.
A infraestrutura pode ser atualizada e gerenciada como código, o que facilita o gerenciamento e a manutenção.












