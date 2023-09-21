---
title: Configurar o caminho e o classpath
description: Configurar o caminho e o classpath
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Configurar o caminho e o classpath{#configure-the-path-and-classpath}

A variável [!DNL flashaccess.war] contém [!DNL jsafeWithNative.jar], que é a biblioteca Crypto-J. Este último requer uma biblioteca nativa adicional para executar operações de criptografia.

1. Adicionar o nativo [!DNL jsafe] para o seu caminho.

   * **Linux / [!DNL libjsafe.so] -** O diretório que contém [!DNL libjsafe.so] deve estar no Caminho (as bibliotecas Crypto-J nativas também estão disponíveis para outras plataformas). Por exemplo, defina [!DNL libjsafe.so] em `LD_LIBRARY_PATH`.

   * **Windows / [!DNL jsafe.dll] -** O equivalente no Windows para [!DNL libjsafe.so] é o apropriado [!DNL jsafe.dll].

   Essas bibliotecas estão disponíveis no [!DNL thirdparty] pasta da biblioteca.
1. Coloque um dos [!DNL adobe-flashaccess-certs] arquivos jar no classpath.

       Esse arquivo JAR não está incluído no arquivo WAR; você deve adicioná-lo explicitamente ao classpath.
   
   * Servidores de desenvolvimento - devem usar somente [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Servidores de produção - devem usar somente [!DNL adobe-flashaccess- certs.jar]

A distribuição inclui um [!DNL shared] pasta que inclui o arquivo jar e um arquivo pré-configurado [!DNL AdobeInitial.properties] arquivo. A Adobe recomenda adicionar esses itens à `common.loader` por meio da [!DNL catalina.properties] arquivo. Por exemplo:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
