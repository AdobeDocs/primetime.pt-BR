---
title: Requisitos de software
description: Requisitos de software
copied-description: true
exl-id: aa2ae6ac-7c2a-4cc3-a3a4-b7f92e478d23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Requisitos de software {#software-requirements}

* Tomcat 6
* JDK 1.8

## Entrega de código/Conteúdo do pacote{#code-delivery-package-contents}

O pacote Adobe Primetime DRM On Premises Individualization Server contém o seguinte:

* [!DNL flashaccess.war] - O servidor de personalização
* [!DNL flashaccess-kgs.war] - O servidor de geração de chaves opcional
* [!DNL /shared] - Contém:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - Arquivo de propriedades de exemplo

* [!DNL thirdparty/] - Inclui suporte a Crypto-J como bibliotecas nativas:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Um utilitário para criptografar senhas de credenciais do servidor
* [!DNL ROOT] - contém um [!DNL crossdomain.xml] arquivo

* Arquivos de cache da ECI - Pré-baixados
* [!DNL addIndivCert.py] - Um script para atualizar a raiz de confiança de um License Server para dar suporte a individualizações no local
* [!DNL CreateMetadata.jar] - Um utilitário para criar Metadados DRM no Local
* [!DNL client_sample/] - Uma pasta com um trecho de código de cliente
* Notas de versão - Para adições de última hora à documentação

## Obter Certificados do Servidor de Individualização{#obtain-individualization-server-certificates}

Para usar o On Premises Individualization Server, primeiro obtenha duas credenciais digitais (certificados):

* *Credencial de transporte de individualização* - emitido por Adobe
* *Credencial da CA de individualização* - emitido pela Symantec (VeriSign)

Para obter esses certificados, envie uma solicitação por meio do ticket do Zendesk para: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Observe que essas credenciais são adicionais às credenciais necessárias para operar um servidor de licença PRIMETIME DRM.
