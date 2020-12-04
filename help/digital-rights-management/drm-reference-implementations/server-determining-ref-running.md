---
description: nulo
seo-description: nulo
seo-title: Determinando se o Servidor de Licenças de Implementação de Referência é executado corretamente
title: Determinando se o Servidor de Licenças de Implementação de Referência é executado corretamente
uuid: afd82d6d-a11c-48ff-b48c-8f81d4b406a0
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Determinando se o Servidor de Licenças de Implementação de Referência é executado corretamente {#determining-if-reference-implementation-license-server-runs-properly}

Existem várias maneiras de determinar se o Servidor de Licenças de Implementação de Referência foi iniciado corretamente. Você pode visualização os registros [!DNL catalina.log] podem não ser suficientes, já que o servidor de licenças registra em seus próprios arquivos de log. Siga as etapas abaixo para garantir que a implementação de referência tenha sido iniciada corretamente.

* Verifique seu arquivo [!DNL AdobeFlashAccess.log]. É aqui que a Implementação de referência grava informações de log. O local desse arquivo de log é indicado pelo arquivo [!DNL log4j.xml] e pode ser modificado para apontar para qualquer local desejado. Por padrão, o arquivo de log copiado para o diretório de trabalho onde você executa o catalina.

* Vá para o seguinte URL: [!DNL https:// flashaccess/license/v4]*servidor:porta do servidor*. Você deve ver o texto &quot;O License Server está configurado corretamente&quot;.

Outra maneira de testar se o servidor é executado corretamente é empacotar um segmento do conteúdo de teste, configurar um player de vídeo de amostra e reproduzi-lo.

O procedimento a seguir descreve esse processo:

1. Vá para a pasta [!DNL \Reference Implementation\Command Line Tools].

   Consulte [Instalar as ferramentas de linha de comando](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) sobre como instalar as ferramentas de linha de comando.

1. Digite o seguinte comando para criar uma política de DRM anônima simples:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Consulte [Uso da linha de comando](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) sobre como criar políticas DRM com o Gerenciador de políticas DRM.

1. Defina a propriedade `encrypt.license.serverurl` no arquivo [!DNL flashaccesstools.properties] como a URL do servidor de licenças.

   Por exemplo, [!DNL https:// localhost:8080/]. O arquivo [!DNL flashaccesstools.properties] está localizado na pasta [!DNL \Reference Implementation\Command Line Tools].

1. Digite o seguinte comando para empacotar um segmento do conteúdo:

```
       java -jar libs\AdobePackager.jar  
       <i class="+ topic ph hi-d="" i "="">
         test_input_FLV  
        <i class="+ topic ph hi-d="" i "="">
       output_file  
               -p policy_test.pol 
       </i class="+ topic> 
       </i class="+ topic>
```

1. Copie os dois arquivos gerados para a pasta [!DNL webapps\ROOT\Content] no servidor Tomcat.
1. Vá para o diretório [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] e copie o conteúdo para a pasta [!DNL webapps\ROOT\SVP\] no servidor Tomcat.

1. Instale o Flash Player versão 10.1 ou posterior.
1. Abra um navegador da Web e vá para o seguinte URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Vá para o seguinte URL e clique em **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. Se o vídeo não for reproduzido, verifique se algum código de erro é exibido no painel de registro do Amostra do player de vídeo ou adicionado ao arquivo [!DNL AdobeFlashAccess.log].

   Agora você pode pesquisar a localização do arquivo de log [!DNL AdobeFlashAccess.log] no arquivo log4j.xml e modificá-lo. Por padrão, o arquivo de log é copiado no diretório de trabalho onde você executa o catalina.

