---
description: nulo
seo-description: nulo
seo-title: Requisitos de software
title: Requisitos de software
uuid: 9faa229b-1abf-4b55-b293-247777bcb1db
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Requisitos de software {#software-requirements}

* Tomcat 6
* JDK 1.8

## Entrega de código/Conteúdo do pacote{#code-delivery-package-contents}

O pacote do Adobe Primetime DRM On Premise Individualization Server contém o seguinte:

* [!DNL flashaccess.war] - O servidor de individualização
* [!DNL flashaccess-kgs.war] - Servidor opcional de geração de chave
* [!DNL /shared] - Contém:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - Arquivo de propriedades de amostra

* [!DNL thirdparty/] - Inclui suporte a Crypto-J como bibliotecas nativas:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Um utilitário para criptografar senhas de credenciais do servidor
* [!DNL ROOT] - contém um [!DNL crossdomain.xml] arquivo

* Arquivos de cache ECI - Pré-baixados
* [!DNL addIndivCert.py] - Um script para atualizar a raiz de confiança do License Server para suportar individualizações locais
* [!DNL CreateMetadata.jar] - Um utilitário para a criação de metadados DRM locais
* [!DNL client_sample/] - Uma pasta com um trecho de código de cliente
* Notas de versão - Para quaisquer adições de última hora à documentação

## Obter certificados do servidor de individualização{#obtain-individualization-server-certificates}

Para usar o On Premise Individualization Server, primeiro você deve obter duas credenciais digitais (certificados):

* *Credencial* de transporte de personalização - emitida pela Adobe
* *Credencial* CA de individualização - emitida pela Symantec (VeriSign)

Para obter esses certificados, envie uma solicitação por meio do tíquete Zendesk para: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Observe que essas credenciais estão além das credenciais necessárias para operar um Servidor de Licenças DRM Primetime.