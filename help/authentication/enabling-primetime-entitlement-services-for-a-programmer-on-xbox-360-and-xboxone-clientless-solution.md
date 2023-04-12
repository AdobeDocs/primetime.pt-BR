---
title: Ativando os serviços de direito do Primetime para um programador no Xbox 360 e XboxOne sem cliente
description: Ativando os serviços de direito do Primetime para um programador no Xbox 360 e XboxOne sem cliente
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Ativando os serviços de direito do Primetime para um programador no Xbox 360 e XboxOne sem cliente {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.




1. O Programador cria um tíquete do Zendesk para habilitar a solução sem cliente Xbox 360/One para autenticação Primetime, fornecendo as seguintes informações:

   1. Plataforma: Por exemplo, Xbox 360, Xbox One

   1. ID do solicitante: por exemplo, netgeo, CNN, etc.

1. O Adobe criará Certificados X509 e configurará a chave privada e a senha ao final.

1. O Adobe fornecerá o certificado Público (de certificado X509) para o Programador no tíquete ou por email.

1. O Programador precisaria instalar esse certificado público no portal GDNP para o aplicativo registrado na Microsoft.

1. O Programador solicitará o JWT (Java Web Token) ou o STS Token para XboxOne ou 360, respectivamente, do serviço Microsoft Xbox Live, que seria criptografado usando o certificado público X509 fornecido na etapa 3.

1. Esses são os tokens que contêm o deviceId exclusivo para dispositivos Xbox. Inclua o token (JWT ou STS) no cabeçalho da Autorização usando um parâmetro &quot;x&quot;, conforme abaixo:

   1. Para o Xbox 360, o token XSTS deve ser codificado em Base64 antes de enviar para a autenticação de TV paga do Primetime.
   1. Para a Xbox One, o JWT já está codificado corretamente, portanto, nenhuma codificação extra deve ocorrer. 

1. Todas as chamadas de API do dispositivo Xbox devem conter o cabeçalho de autorização com o token mencionado acima no parâmetro x .

 

>[!NOTE]
>
>A Xbox em particular tem alguns requisitos exclusivos relacionados à assinatura digital. A ID do dispositivo do console XBox é incluída no token XSTS.  Para Xbox 360, essa é uma asserção SAML criptografada; para Xbox One, este é um JWT criptografado. O aplicativo do console XBox envia o token XSTS inteiro para a autenticação do Primetime pay-TV. A autenticação da TV paga do Primetime descriptografa o token usando sua chave pública, analisa o token e extrai o deviceId dele.

>[!NOTE]
>
>Devido ao grande comprimento do token XSTS, o console XBox tem uma limitação técnica: ele não pode enviar o token como um parlamentar do HTTP GET para as APIs de autenticação do Primetime pay-TV. Para lidar com isso, a autenticação de TV paga do Primetime permite enviar o token XSTS como parte do cabeçalho HTTP &quot;Autorização&quot; ao chamar as APIs. O token XSTS deve ser criptografado usando a chave pública do certificado X.509 emitido para o Programador a partir da autenticação de TV paga do Primetime. A autenticação de TV paga do Primetime armazena a chave privada associada e a usa para descriptografar o token XSTS e extrair o deviceId dela.  


