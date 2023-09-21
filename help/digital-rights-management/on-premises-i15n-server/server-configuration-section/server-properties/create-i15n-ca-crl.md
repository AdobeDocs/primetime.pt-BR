---
title: Criar CRL de CA de Individualização
description: Criar CRL de CA de Individualização
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Criar CRL de CA de Individualização{#create-individualization-ca-crl}

Este ponto de distribuição da Lista de Certificados Revogados (CRL) está incluído em cada certificado de máquina emitido pelo servidor de individualização. Durante a validação do certificado de máquina no servidor de licenças, essa CRL será baixada do ponto de distribuição listado no certificado (ou lida do cache, se já tiver sido baixada) e verificada para ter certeza de que o certificado não foi revogado.

>[!NOTE]
>
>Para definir o URL do ponto de distribuição da CRL, será necessário definir o [!DNL AdobeInitial.properties] `cert.machine.crldp` campo. Este ponto de distribuição é *não* verificado pelo Primetime DRM quanto à validade. Você deve verificar se esse URL é válido. Erros resultantes de um URL inválido não se tornarão aparentes até que erros de validação apareçam no servidor de licenças.

As instruções de exemplo para usar o OpenSSL para criar CRLs que seu servidor de licenças pode consumir são simplificadas e descritas abaixo. A Adobe recomenda executar essas etapas de maneira segura e em um ambiente, depois que uma credencial de CA de individualização de produção for obtida.

1. Altere o diretório de trabalho para o [!DNL create_crl] diretório incluído nesta distribuição.
1. Copiar sua Autoridade de Certificação de Individualização [!DNL pfx] para o mesmo [!DNL create_crl] diretório.

   As etapas subsequentes pressupõem que o pfx da CA de individualização seja nomeado como [!DNL i15n.pfx]. Ajuste conforme apropriado para sua configuração.
1. Extrair a autoridade de certificação de individualização [!DNL pfx] chave privada do arquivo.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Converter a chave privada em [!DNL pksc8] formato.

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Gere a CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   Este exemplo cria uma CRL com um período de validade padrão de 1 mês. Use o `-crldays` e `-crlhours` opções para substituir os valores padrão.

   A geração de uma CRL usa a variável [!DNL index] e [!DNL crlnumber] arquivo apontado em seu [!DNL openssl.conf]. Por padrão, a variável [!DNL demoCA] a localização no diretório de trabalho é usada. Amostra [!DNL index] e [!DNL crlnumber] os arquivos estão incluídos na variável [!DNL demoCA] diretório.

1. Implante o arquivo CRL gerado na etapa anterior em um local adequado que possa ser acessado pelo servidor de licenças (por exemplo: servidor de individualização [!DNL ROOT]).
1. Reinicie o servidor de licenças quando a CRL estiver em vigor.
