---
seo-title: Criar CRL da CA de individualização
title: Criar CRL da CA de individualização
uuid: f722f3d1-517f-43e3-b892-f9287527fbe6
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Criar CRL da CA de individualização{#create-individualization-ca-crl}

Este ponto de distribuição da Lista de Revogação de Certificado (CRL) está incluído em cada certificado de máquina emitido pelo servidor de individualização. Durante a validação do certificado da máquina no servidor de licenças, essa CRL será baixada do ponto de distribuição listado no certificado (ou lida do cache, se já tiver sido baixada) e verificada a certeza de que o certificado não foi revogado.

>[!NOTE]
>
>Para definir o URL do ponto de distribuição CRL, é necessário definir o campo [!DNL AdobeInitial.properties] `cert.machine.crldp`. Este ponto de distribuição está *e não* marcado pelo Primetime DRM para validade. Você deve verificar se este URL é válido. Os erros resultantes de um URL inválido não serão exibidos até que os erros de validação apareçam do servidor de licenças.

Os contornos abaixo são simplificados, exemplos de instruções para usar o OpenSSL para criar CRLs que seu servidor de licenças pode consumir. A Adobe recomenda que você execute essas etapas de modo seguro e ambiente, depois que uma credencial CA de produção de individualização for obtida.

1. Altere o diretório de trabalho para o diretório [!DNL create_crl] incluído nesta distribuição.
1. Copie sua CA de individualização [!DNL pfx] para o mesmo diretório [!DNL create_crl].

   As etapas subsequentes pressupõem que a AC de individualização pfx seja chamada de [!DNL i15n.pfx]. Ajuste conforme apropriado para sua configuração.
1. Extraia a chave privada do arquivo CA de personalização [!DNL pfx].

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Converta a chave privada para o formato [!DNL pksc8].

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Gerar a CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   Este exemplo cria uma CRL com um período de validade padrão de 1 mês. Use as opções `-crldays` e `-crlhours` para substituir os valores padrão.

   Gerar uma CRL usa os arquivos [!DNL index] e [!DNL crlnumber] apontados em [!DNL openssl.conf]. Por padrão, o local [!DNL demoCA] no diretório de trabalho é usado. Os arquivos de amostra [!DNL index] e [!DNL crlnumber] estão incluídos no diretório [!DNL demoCA] fornecido.

1. Implante o arquivo CRL gerado na etapa anterior para um local adequado que possa ser acessado pelo servidor de licenças (por exemplo: servidor de individualização [!DNL ROOT]).
1. Reinicie o servidor de licenças, assim que a CRL estiver em vigor.
