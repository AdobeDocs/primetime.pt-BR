---
title: Determinando se o Servidor de licenças de implementação de referência está sendo executado corretamente
description: Determinando se o Servidor de licenças de implementação de referência está sendo executado corretamente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Determinando se o Servidor de licenças de implementação de referência está sendo executado corretamente {#determining-if-reference-implementation-license-server-is-running-properly}

Há várias maneiras de determinar se o servidor foi iniciado corretamente. Exibir o [!DNL catalina.log] os registros podem não ser suficientes, pois o servidor de licenças registra seus próprios arquivos de registro. Siga as etapas abaixo para garantir que sua Implementação de referência tenha sido iniciada corretamente.

* Verifique o seu [!DNL AdobeFlashAccess.log] arquivo. É aqui que a implementação de referência grava informações de log. O local desse arquivo de log é indicado pelo seu [!DNL log4j.xml] e podem ser modificadas para apontar para qualquer local desejado. Por padrão, o arquivo de log será enviado para o diretório de trabalho no qual você executou o catalina.

* Navegue até o seguinte URL: `https:///flashaccess/license/v4<your server:server port>`. Você deve ver o texto &quot;O License Server está configurado corretamente&quot;.

Outra maneira de testar se o servidor está sendo executado corretamente é criar um pacote de conteúdo de teste, configurar um player de vídeo de exemplo e reproduzi-lo. O procedimento a seguir descreve esse processo:

1. Navegue até a [!DNL \Reference Implementation\Command Line Tools] pasta. Para obter informações sobre como instalar as ferramentas de linha de comando, consulte [Instalação das ferramentas de linha de comando](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Crie uma política anônima simples usando o seguinte comando:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Para obter mais informações sobre como criar políticas usando o Gerenciador de políticas, consulte [Uso da linha de comando](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Defina o `encrypt.license.serverurl` propriedade na [!DNL flashaccesstools.properties] para o URL do servidor de licenças (por exemplo, `https:// localhost:8080/`). A variável [!DNL flashaccesstools.properties] O arquivo está localizado sob o [!DNL \Reference Implementation\Command Line Tools] pasta.

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

1. Copie os 2 arquivos gerados para o Tomcat [!DNL webapps\ROOT\Content] pasta.
1. Navegue até `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` e copiar o conteúdo para o Tomcat `webapps\ROOT\SVP\` pasta.
1. Instale o Flash Player 10.1 ou posterior.
1. Abra o navegador da Web e navegue até o seguinte URL:

   `https:// localhost:8080/SVP/player.html`
1. Navegue até o URL a seguir e clique no botão Reproduzir:

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Se não for possível reproduzir o vídeo, verifique se algum código de erro foi gravado no painel de registro do reprodutor de vídeo de amostra ou na variável `AdobeFlashAccess.log` arquivo. A localização do `AdobeFlashAccess.log` O arquivo de log é indicado pelo arquivo log4j.xml e pode ser modificado para apontar para qualquer local desejado. Por padrão, o arquivo de log é gravado no diretório de trabalho em que você executou o catalina.
