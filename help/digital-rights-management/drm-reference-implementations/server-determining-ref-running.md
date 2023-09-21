---
title: Determinar se o Servidor de licenças de implementação de referência é executado corretamente
description: Determinar se o Servidor de licenças de implementação de referência é executado corretamente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Determinar se o Servidor de licenças de implementação de referência é executado corretamente {#determining-if-reference-implementation-license-server-runs-properly}

Há várias maneiras de determinar se o Servidor de licenças de implementação de referência foi iniciado corretamente. É possível exibir a [!DNL catalina.log] os registros podem não ser suficientes, pois o servidor de licenças registra seus próprios arquivos de registro. Siga as etapas abaixo para garantir que sua Implementação de referência tenha sido iniciada corretamente.

* Verifique o seu [!DNL AdobeFlashAccess.log] arquivo. É aqui que a implementação de referência grava informações de log. O local desse arquivo de log é indicado pelo seu [!DNL log4j.xml] e podem ser modificadas para apontar para qualquer local desejado. Por padrão, o arquivo de log é copiado para o diretório de trabalho no qual você executa o catalina.

* Vá para o seguinte URL: [!DNL https:// flashaccess/license/v4]*seu servidor:porta do servidor*. Você deve ver o texto &quot;O License Server está configurado corretamente&quot;.

Outra maneira de testar se o servidor é executado corretamente é empacotar um segmento do conteúdo de teste, configurar um player de vídeo de amostra e reproduzi-lo.

O procedimento a seguir descreve esse processo:

1. Vá para a [!DNL \Reference Implementation\Command Line Tools] pasta.

   Consulte [Instalação das ferramentas de linha de comando](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) sobre como instalar as ferramentas de linha de comando.

1. Digite o seguinte comando para criar uma política DRM anônima simples:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Consulte [Uso da linha de comando](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) sobre como criar políticas DRM com o Gerenciador de políticas DRM.

1. Defina o `encrypt.license.serverurl` propriedade na [!DNL flashaccesstools.properties] para o URL do servidor de licenças.

   Por exemplo, [!DNL https:// localhost:8080/]. A variável [!DNL flashaccesstools.properties] O arquivo está localizado na [!DNL \Reference Implementation\Command Line Tools] pasta.

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

1. Copie os dois arquivos gerados para o [!DNL webapps\ROOT\Content] no servidor Tomcat.
1. Vá para a [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] e copie o conteúdo para o [!DNL webapps\ROOT\SVP\] no servidor Tomcat.

1. Instale o Flash Player versão 10.1 ou posterior.
1. Abra um navegador da Web e vá para o seguinte URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Vá para o seguinte URL e clique em **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. Se não for possível reproduzir o vídeo, verifique se algum código de erro é exibido no painel de registro do reprodutor de vídeo de amostra ou adicionado à [!DNL AdobeFlashAccess.log] arquivo.

   Agora você pode pesquisar a localização do [!DNL AdobeFlashAccess.log] arquivo de log no arquivo log4j.xml e modifique-o. Por padrão, o arquivo de log é copiado para o diretório de trabalho no qual você executa o catalina.
