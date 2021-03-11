---
title: Criar CRL da CA de individualização
description: Criar CRL da CA de individualização
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Criar CRL da CA de individualização{#create-individualization-ca-crl}

Este ponto de distribuição da Lista de Revogação de Certificado (CRL) é incluído em cada certificado de máquina emitido pelo servidor de individualização. Durante a validação do certificado da máquina no servidor de licenças, essa CRL será baixada do ponto de distribuição listado no certificado (ou lida do cache, se já tiver sido baixada) e verificada se o certificado não foi revogado.

>[!NOTE]
>
>Para definir o URL do ponto de distribuição da CRL, é necessário definir o campo [!DNL AdobeInitial.properties] `cert.machine.crldp` . Este ponto de distribuição é *not* verificado pelo DRM Primetime para obter a validade. Você deve verificar se este URL é válido. Erros resultantes de um URL inválido não serão aparentes até que erros de validação apareçam do servidor de licenças.

Os itens descritos abaixo são simplificados, exemplos de instruções para usar o OpenSSL para criar CRLs que seu servidor de licenças pode consumir. O Adobe recomenda que você execute essas etapas com segurança e ambiente, depois que uma credencial da CA de individualização de produção for obtida.

1. Altere o diretório de trabalho para o diretório [!DNL create_crl] incluído nesta distribuição.
1. Copie sua CA de individualização [!DNL pfx] para o mesmo diretório [!DNL create_crl].

   As etapas subsequentes pressupõem que o cfx da AC de individualização seja nomeado [!DNL i15n.pfx]. Ajuste conforme apropriado para sua configuração.
1. Extraia a chave privada do arquivo CA de individualização [!DNL pfx].

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Converta a chave privada para o formato [!DNL pksc8].

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Gere a CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   Esse exemplo cria uma CRL com um período de validade padrão de 1 mês. Use as opções `-crldays` e `-crlhours` para substituir os valores padrão.

   Gerar uma CRL usa o arquivo [!DNL index] e [!DNL crlnumber] apontados em seu [!DNL openssl.conf]. Por padrão, o local [!DNL demoCA] no diretório de trabalho é usado. Arquivos [!DNL index] e [!DNL crlnumber] de amostra estão incluídos no diretório [!DNL demoCA] fornecido.

1. Implante o arquivo CRL gerado na etapa anterior em um local adequado que possa ser acessado pelo servidor de licença (por exemplo: servidor de individualização [!DNL ROOT]).
1. Reinicie o servidor de licença, assim que a CRL estiver em vigor.
