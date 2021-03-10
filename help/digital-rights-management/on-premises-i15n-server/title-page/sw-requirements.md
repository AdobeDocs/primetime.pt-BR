---
title: Requisitos de software
description: Requisitos de software
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Requisitos de software {#software-requirements}

* Tomcat 6
* JDK 1.8

## Entrega de código/Conteúdo do pacote{#code-delivery-package-contents}

O pacote Adobe Primetime DRM On Premise Individualization Server contém o seguinte:

* [!DNL flashaccess.war] - O servidor de individualização
* [!DNL flashaccess-kgs.war] - Servidor opcional de geração de chave
* [!DNL /shared] - Contém:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - Arquivo de propriedades de exemplo

* [!DNL thirdparty/] - Inclui suporte a Crypto-J como bibliotecas nativas:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Um utilitário para criptografar senhas de credenciais do servidor
* [!DNL ROOT] - contém um  [!DNL crossdomain.xml] arquivo

* Arquivos de cache da ECI - Pré-baixados
* [!DNL addIndivCert.py] - Um script para atualizar a raiz de confiança do License Server para suportar individualizações locais
* [!DNL CreateMetadata.jar] - Um utilitário para criar metadados de DRM nas instalações
* [!DNL client_sample/] - Uma pasta com um trecho de código de cliente
* Notas de versão - Para quaisquer adições de último minuto à documentação

## Obter certificados do servidor de individualização{#obtain-individualization-server-certificates}

Para usar o On Premise Individualization Server, primeiro você deve obter duas credenciais digitais (certificados):

* *Credencial de Transporte de Individualização*  - emitida pelo Adobe
* *Credencial da CA de individualização*  - emitida pela Symantec (VeriSign)

Para obter esses certificados, envie uma solicitação por meio do tíquete do Zendesk para: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Observe que essas credenciais estão além das credenciais necessárias para operar um Servidor de Licenças de DRM do Primetime.