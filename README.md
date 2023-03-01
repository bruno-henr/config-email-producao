# rockeseat-config-email-producao
Apenas um readme com os passos necessarios para configurar um email em producao utilizando AWS SES

1º config
Utilizar SES da AWS para disparar emails
- Possuir um dominio (ex.: google domais)
- Possuir email (ex.: zoho)

Devera ser passado para o SES da aws o seu dominio e email que irao passar uma uma validacao, depois você deve buscar em detalhes do dominio inserido na AWs e setar em DNS no painel do seu dominio

2º config

Ainda dentro do painel da AWS, pesquise por "IAM" -> usuarios -> adicionar permissao -> anexar politicas existentes de forma direta -> *pesquisar por SeS  e adicionar a FullAccess marcando a caixa -> proximo -> adicionar.

# Exemplo de codigo:

import { injectable } from "tsyringe";
import { IMailProvider } from "../interface/MailProvider"; // interface
import nodemailer, { Transporter } from "nodemailer";
import aws from "aws-sdk";

@injectable()
export class SesMailProvider implements IMailProvider {
  private client: Transporter;
  constructor() {
    this.client = nodemailer.createTransport({
      SES: new aws.SES({
        apiVersion: "2010-12-01",
        region: "us-east-1",
      }),
    });
  }

  async sendMail(to: string, subject: string, body: string): Promise<void> {
    await this.client.sendMail({
      to,
      from: "rentx <noreplay@rentx.com.br>",
      subject,
      text: body,
      html: body,
    });
  }
}
