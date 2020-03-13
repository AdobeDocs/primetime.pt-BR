---
seo-title: Configurar o caminho e o caminho de classe
title: Configurar o caminho e o caminho de classe
uuid: cf10fafa-125e-450c-83ae-60b990dab6b5
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# Configurar o caminho e o caminho de classe{#configure-the-path-and-classpath}

O [!DNL flashaccess.war] contém [!DNL jsafeWithNative.jar], que é a biblioteca Crypto-J. O último requer uma biblioteca nativa adicional para executar operações de criptografia.

1. Adicione a biblioteca nativa ao seu [!DNL jsafe] caminho.

   * **Linux /[!DNL libjsafe.so]-** O diretório que contém [!DNL libjsafe.so] deve estar no Caminho (as bibliotecas nativas do Crypto-J também estão disponíveis para outras plataformas). Por exemplo, defina [!DNL libjsafe.so] em `LD_LIBRARY_PATH`.

   * **Windows /[!DNL jsafe.dll]-** O equivalente do Windows para [!DNL libjsafe.so] é o apropriado [!DNL jsafe.dll].
   Essas bibliotecas estão disponíveis para você na pasta da [!DNL thirdparty] biblioteca.
1. Coloque um dos arquivos [!DNL adobe-flashaccess-certs] jar no classpath.

       Este ficheiro JAR não está incluído no ficheiro WAR; você deve adicioná-lo explicitamente ao classpath.
   
   * Servidores de desenvolvimento - devem usar apenas [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Servidores de produção - deve usar somente [!DNL adobe-flashaccess- certs.jar]

A distribuição inclui uma [!DNL shared] pasta que inclui o arquivo jar e um [!DNL AdobeInitial.properties] arquivo pré-configurado. A Adobe recomenda que você adicione esses itens ao arquivo `common.loader` por meio do [!DNL catalina.properties] arquivo. Por exemplo:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


