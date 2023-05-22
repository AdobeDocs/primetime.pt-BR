---
title: Ativação dos serviços de direitos do Primetime para um programador no Xbox 360 e no Xbox One Clientless
description: Ativação dos serviços de direitos do Primetime para um programador no Xbox 360 e no Xbox One Clientless
exl-id: ff7254de-9ea4-4c27-a186-d1c2eea12222
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Ativação dos serviços de direitos do Primetime para um programador no Xbox 360 e no Xbox One Clientless {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.




1. O Programador cria um tíquete Zendesk para habilitar a solução cliente de autenticação do Xbox 360/One para Primetime, fornecendo as seguintes informações:

   1. Plataforma: por exemplo, Xbox 360, Xbox One

   1. ID do solicitante: por exemplo, netgeo, CNN etc.

1. O Adobe criará Certificados X509 e configurará a chave privada e a senha no final.

1. O Adobe fornecerá o certificado Público (de certificado X509) ao Programador no tíquete ou por email.

1. O programador precisaria então instalar esse certificado público no portal GDNP para o aplicativo registrado no Microsoft.

1. O Programador irá então solicitar o JWT (Java Web Token) ou o STS Token para XboxOne ou 360, respectivamente, a partir do serviço Microsoft Xbox Live, que seria criptografado usando o certificado público X509 fornecido na etapa 3.

1. Esses são os tokens que contêm o deviceId exclusivo para dispositivos Xbox. Inclua o token (JWT ou STS) no cabeçalho de Autorização usando um parâmetro &quot;x&quot;, conforme abaixo:

   1. Para o Xbox 360, o token XSTS deve ser codificado em Base64 antes de enviar para a autenticação de TV paga do Primetime.
   1. Para o Xbox One, o JWT já está corretamente codificado, então nenhuma codificação extra deve ocorrer. 

1. Todas as chamadas de API do dispositivo Xbox devem conter o cabeçalho de autorização com o token mencionado acima no parâmetro x.

 

>[!NOTE]
>
>O Xbox, em particular, tem alguns requisitos exclusivos relacionados à assinatura digital. A ID de dispositivo do console XBox está incluída no token XSTS.  Para o Xbox 360, esta é uma asserção SAML criptografada; para o Xbox One, esta é uma JWT criptografada. O aplicativo do console XBox envia o token XSTS inteiro para a autenticação de TV paga do Primetime. A autenticação de TV paga do Primetime descriptografa o token usando sua chave pública, analisa o token e extrai o deviceId dele.

>[!NOTE]
>
>Devido ao grande comprimento do token XSTS, o console XBox tem uma limitação técnica: não pode enviar o token como um GET HTTP para as APIs de autenticação de TV paga do Primetime. Para lidar com isso, a autenticação de TV paga do Primetime permite enviar o token XSTS como parte da &quot;Autorização&quot; do cabeçalho HTTP ao chamar as APIs. O token XSTS deve ser criptografado usando a chave pública do certificado X.509 emitido para o Programador na autenticação de TV paga do Primetime. A autenticação de TV por assinatura do Primetime armazena a chave privada associada e a usa para descriptografar o token XSTS e extrair o deviceId dele.
