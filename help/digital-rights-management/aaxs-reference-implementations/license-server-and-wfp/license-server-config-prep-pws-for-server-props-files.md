---
seo-title: Preparando senhas para os arquivos de propriedades do Servidor
title: Preparando senhas para os arquivos de propriedades do Servidor
uuid: 2d876eb0-b1a5-4c30-ae96-0a22f6a03910
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Preparando senhas para os arquivos de propriedades do Servidor {#preparing-passwords-for-the-server-properties-files}

Para garantir a segurança da senha de sua credencial, uma ferramenta é fornecida para criptografar a senha antes de ela ser inserida no arquivo [!DNL flashaccess-refimpl.properties] ou [!DNL flashaccess-refimpl-packager.properties] .

Para executar a ferramenta usando o script ANT fornecido:

* Ir para *`<Reference Implementation Server Path>`*[!DNL \refimpl]

* Verifique se a `sdkdir` propriedade em [!DNL build-refimpl.xml] pontos do diretório que contém o SDK do Adobe Access
* Execute o seguinte comando usando ANT:

   ```
       ant -f build-refimpl.xml
   ```

* Quando solicitado, digite a senha da sua credencial

Para executar a ferramenta usando o Java:

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
>As senhas codificadas usando o utilitário de definição de senha fornecido com a implementação de referência não funcionarão com o Adobe Access Server for Protected Streaming.
