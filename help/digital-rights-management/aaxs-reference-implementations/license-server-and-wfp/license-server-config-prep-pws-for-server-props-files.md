---
title: Preparando senhas para os arquivos de propriedades do Servidor
description: Preparando senhas para os arquivos de propriedades do Servidor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Preparando senhas para os arquivos de propriedades do Servidor {#preparing-passwords-for-the-server-properties-files}

Para garantir a segurança da senha da sua credencial, uma ferramenta é fornecida para criptografar a senha antes que ela seja inserida na [!DNL flashaccess-refimpl.properties] ou [!DNL flashaccess-refimpl-packager.properties] arquivo.

Para executar a ferramenta usando o script ANT fornecido:

* Ir para *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* Assegure a `sdkdir` propriedade no [!DNL build-refimpl.xml] aponta para o diretório que contém o SDK de acesso do Adobe
* Execute o seguinte comando usando ANT:

  ```
      ant -f build-refimpl.xml
  ```

* Quando solicitado, digite a senha da sua credencial

Para executar a ferramenta usando Java:

* Ir para *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* No prompt de comando, digite o comando:

* No Windows:

  ```
  java -classpath path_to_adobe-flashaccess-sdk.jar;.  
  com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
  ```

* No Linux:

  ```
      java -classpath path_to_adobe-flashaccess-sdk.jar;.  
      com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
  ```

O utilitário gera a senha criptografada, que você deve copiar para o arquivo .properties.

>[!NOTE]
>
>As senhas codificadas usando o utilitário de codificação de senhas fornecido com a implementação de referência não funcionarão com o Adobe Access Server para transmissão protegida.
