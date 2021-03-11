---
title: Preparando senhas para os arquivos de propriedades do servidor
description: Preparando senhas para os arquivos de propriedades do servidor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Preparando senhas para os arquivos de propriedades do servidor {#preparing-passwords-for-the-server-properties-files}

Para garantir a segurança da senha da credencial, uma ferramenta é fornecida para criptografar a senha antes de ela ser inserida no arquivo [!DNL flashaccess-refimpl.properties] ou [!DNL flashaccess-refimpl-packager.properties].

Para executar a ferramenta usando o script ANT fornecido:

* Vá para *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* Verifique se a propriedade `sdkdir` em [!DNL build-refimpl.xml] aponta para o diretório que contém o SDK do Adobe Access
* Execute o seguinte comando usando ANT:

   ```
       ant -f build-refimpl.xml
   ```

* Quando solicitado, digite a senha da credencial

Para executar a ferramenta usando o Java:

* Vá para *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

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

O utilitário gera a senha criptografada, que deve ser copiada para o arquivo .properties .

>[!NOTE]
>
>As senhas codificadas com o uso do utilitário de digitação de senha fornecido com a implementação de referência não funcionarão com o Adobe Access Server for Protected Streaming.
