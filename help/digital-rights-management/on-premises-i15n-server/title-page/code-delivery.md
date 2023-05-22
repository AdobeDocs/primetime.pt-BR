---
title: Entrega de código/Conteúdo do pacote
description: Entrega de código/Conteúdo do pacote
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Entrega de código/Conteúdo do pacote{#code-delivery-package-contents}

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

