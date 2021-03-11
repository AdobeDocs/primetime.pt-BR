---
title: Configurar o caminho e o caminho de classe
description: Configurar o caminho e o caminho de classe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# Configurar o caminho e o caminho de classe{#configure-the-path-and-classpath}

O [!DNL flashaccess.war] contém [!DNL jsafeWithNative.jar], que é a biblioteca Crypto-J. O último requer uma biblioteca nativa adicional para executar operações de criptografia.

1. Adicione a biblioteca nativa [!DNL jsafe] ao seu caminho.

   * **Linux /  [!DNL libjsafe.so]  -** O diretório que contém  [!DNL libjsafe.so] deve estar no Caminho (as bibliotecas Crypto-J nativas também estão disponíveis para outras plataformas). Por exemplo, defina [!DNL libjsafe.so] em `LD_LIBRARY_PATH`.

   * **Windows /  [!DNL jsafe.dll]  -** A contrapartida no Windows para  [!DNL libjsafe.so] é a apropriada  [!DNL jsafe.dll].
   Essas bibliotecas estão disponíveis para você na pasta [!DNL thirdparty] da biblioteca.
1. Coloque um dos arquivos jar [!DNL adobe-flashaccess-certs] no classpath.

       Este arquivo JAR não está incluído no arquivo WAR; você deve adicioná-lo explicitamente ao classpath.
   
   * Servidores de desenvolvimento - devem usar somente [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Servidores de produção - deve usar somente [!DNL adobe-flashaccess- certs.jar]

A distribuição inclui uma pasta [!DNL shared] que inclui o arquivo jar e um arquivo [!DNL AdobeInitial.properties] pré-configurado. O Adobe recomenda adicionar esses itens ao `common.loader` por meio do arquivo [!DNL catalina.properties]. Por exemplo:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


