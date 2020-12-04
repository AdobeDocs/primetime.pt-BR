---
description: nulo
seo-description: nulo
seo-title: Determinando se o Servidor de Licença de Implementação de Referência está sendo executado corretamente
title: Determinando se o Servidor de Licença de Implementação de Referência está sendo executado corretamente
uuid: 84d32c94-7594-464e-a883-5338b52de2bf
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Determinando se o Servidor de Licenças de Implementação de Referência está sendo executado corretamente {#determining-if-reference-implementation-license-server-is-running-properly}

Existem várias maneiras de determinar se o servidor foi iniciado corretamente. A visualização dos registros [!DNL catalina.log] pode não ser suficiente, uma vez que o servidor de licenças registra nos seus próprios ficheiros de registro. Siga as etapas abaixo para garantir que a implementação de referência tenha sido iniciada corretamente.

* Verifique seu arquivo [!DNL AdobeFlashAccess.log]. É aqui que a Implementação de referência grava informações de log. O local desse arquivo de log é indicado pelo arquivo [!DNL log4j.xml] e pode ser modificado para apontar para qualquer local desejado. Por padrão, o arquivo de log será enviado para o diretório de trabalho onde você executou o catalina.

* Navegue até o seguinte URL: `https:///flashaccess/license/v4<your server:server port>`. Você deve ver o texto &quot;O License Server está configurado corretamente&quot;.

Outra maneira de testar se o servidor está sendo executado corretamente é empacotar um conteúdo de teste, configurar um player de vídeo de amostra e reproduzi-lo. O procedimento a seguir descreve esse processo:

1. Navegue até a pasta [!DNL \Reference Implementation\Command Line Tools]. Para obter informações sobre como instalar as ferramentas de linha de comando, consulte [Instalar as ferramentas de linha de comando](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Crie uma política anônima simples usando o seguinte comando:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Para obter mais informações sobre como criar políticas usando o Gerenciador de Políticas, consulte [Uso da linha de comando](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Defina a propriedade `encrypt.license.serverurl` no arquivo [!DNL flashaccesstools.properties] como a URL do servidor de licenças (por exemplo, `https:// localhost:8080/`). O arquivo [!DNL flashaccesstools.properties] está localizado na pasta [!DNL \Reference Implementation\Command Line Tools].

1. Empacote um conteúdo usando o seguinte comando:

   ```java
       java -jar libs\AdobePackager.jar  
   <i class="+ topic ph hi-d="" i "="">
   test_input_FLV  
   <i class="+ topic ph hi-d="" i "="">
   output_file  
               -p policy_test.pol 
   </i class="+ topic> 
   </i class="+ topic>
   ```

1. Copie os 2 arquivos gerados para a pasta Tomcat [!DNL webapps\ROOT\Content].
1. Navegue até `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` e copie o conteúdo para a pasta Tomcat `webapps\ROOT\SVP\`.
1. Instale o Flash Player 10.1 ou posterior.
1. Abra o navegador da Web e navegue até o seguinte URL:

   `https:// localhost:8080/SVP/player.html`
1. Navegue até o seguinte URL e clique no botão Reproduzir:

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Se o vídeo não for reproduzido, verifique se algum código de erro foi gravado no painel de registro do Amostra do player de vídeo ou no arquivo `AdobeFlashAccess.log`. O local do arquivo de log `AdobeFlashAccess.log` é indicado pelo arquivo log4j.xml e pode ser modificado para apontar para qualquer local desejado. Por padrão, o arquivo de log é gravado no diretório de trabalho onde você executou o catalina.
