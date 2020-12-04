---
seo-title: Arquivos de propriedades do servidor
title: Arquivos de propriedades do servidor
uuid: 3d3a0ee3-009f-4d62-9587-7e487ecdcafd
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Arquivos de propriedades do servidor {#server-properties-files}

O servidor requer dois arquivos de configuração, um para o servidor de licenças e outro para o empacotador. Ambos os arquivos devem ser colocados no classpath. Os arquivos de propriedades contêm o local das credenciais emitidas pelo Adobe. Essas credenciais podem ser especificadas como um arquivo e senha .pfx ou fornecendo um alias e senha para uma credencial armazenada em um HSM.

Consulte os arquivos de propriedade para obter detalhes sobre os valores específicos e o uso de cada parâmetro. Arquivos de propriedades de amostra podem ser encontrados no diretório &quot;resources&quot; da implementação de referência (Referência Implementation\Server\resources).

Para garantir a segurança da senha de sua credencial, uma ferramenta é fornecida (ScrambleUtil.class) para criptografar a senha antes de ela ser inserida no arquivo flashaccess-refimpl.properties ou flashaccess-refimpl-packager.properties.

Para preparar corretamente a senha da sua credencial:

1. Vá para [!DNL Reference Implementation\Server\refimpl\scrambler].
1. No prompt de comando, digite o comando:

   ```
   java -classpath  
   <i class="+ topic ph hi-d="" i "="">
   path_to_adobe-flashaccess-sdk.jar.; 
        com.adobe.flashaccess.refimpl.util.ScrambleUtil " 
   <i class="+ topic ph hi-d="" i "="">
   your_pfx_password" 
   </i class="+ topic> 
   </i class="+ topic>
   ```

>[!NOTE]
>
>O exemplo anterior usa um ponto-e-vírgula (;) como delimitador. Para plataformas diferentes do Microsoft Windows, use dois pontos (:) como delimitador.

O utilitário gera a senha criptografada, que você deve copiar para o arquivo [!DNL .properties].
