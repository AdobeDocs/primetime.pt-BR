---
seo-title: Baixar e configurar software de pré-requisito
title: Baixar e configurar software de pré-requisito
description: O processo de instalação é simples. Se você já tiver o JDK instalado no sistema, ignore essa etapa, mas saiba que seu JDK, Eclipse IDE e o SO precisam ser compatíveis.
seo-description: O processo de instalação é simples. Se você já tiver o JDK instalado no sistema, ignore essa etapa, mas saiba que seu JDK, Eclipse IDE e o SO precisam ser compatíveis.
uuid: ca29144f-8088-4c8d-93cf-aa59007da034
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---


# Baixe e configure o software de pré-requisito {#download-and-configure-prerequisite-software}

1. Baixe o JDK de [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/).

   O processo de instalação é simples. Se você já tiver o JDK instalado no sistema, ignore essa etapa, mas saiba que seu JDK, Eclipse IDE e o SO precisam ser compatíveis.
1. Baixe o Eclipse IDE para desenvolvedores Java de [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads).

   Depois de descompactar o pacote, você pode executar o Eclipse diretamente. Não há instalador.
1. Baixe o pacote ADT do Android SDK de [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html).

   Este pacote inclui o Eclipse. Se você já tiver o Eclipse instalado em seu sistema, poderá baixar as Ferramentas do SDK para sua plataforma na seção [!UICONTROL Use An Existing IDE].

   Desempacotar e instalar em um local que você lembrará. Você precisará fazer referência a isso em uma etapa posterior.
1. Configure o Android SDK.
   1. Abra um terminal (no Mac OS X) ou um prompt de comando (no Windows).
   1. Navegue até o diretório onde você baixou/descompactou o Android SDK.
   1. Vá para a pasta de ferramentas, que contém um arquivo chamado [!DNL android].
   1. Execute os seguintes comandos:

      * Para Mac OS X/Unix:

         ```
         chmod +x android 
         android update sdk --no-ui
         ```

      * Para Windows:

         ```
         android update sdk --no-ui
         ```

         Esse processo leva um tempo.

1. Configure o Eclipse.
   1. Eclipse do start.

      No Windows, se o Eclipse não for start e o problema reportado for que o Eclipse não consegue localizar um arquivo Java necessário, tente o seguinte:

      * adicione `-vm C:\[path to your JDK bin]\javaw.exe` ao arquivo [!DNL eclipse.ini].
   1. Selecione **[!UICONTROL Help]** > **[!UICONTROL Install New Software]**.
   1. Clique em **[!UICONTROL Add...]**.
   1. Digite `Android` como nome.
   1. Digite `https://dl-ssl.google.com/android/eclipse/` para o link **[!UICONTROL Work with]**.
   1. Clique em **[!UICONTROL OK]**.

      Você deve ver uma caixa de diálogo semelhante a esta:

      ![](assets/available_software.jpg)

   1. Selecione os pacotes resultantes (em Ferramentas do desenvolvedor e Plug-ins NDK) e clique em **[!UICONTROL Next]**.

      Isso baixa as Ferramentas de desenvolvimento do Android (ADT).
   1. Depois que o download for concluído, reinicie o Eclipse.

   O Android SDK agora está instalado. 1. Configure o Eclipse para que ele possa encontrar o Android SDK e usá-lo como um recurso.
   1. Abra o Eclipse.
   1. Selecione **[!UICONTROL Window]** > **[!UICONTROL Preferences]** no Windows;  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** no Mac OS X.
   1. Selecione a guia **[!UICONTROL Android]**.
   1. Navegue até o local do Android SDK.
   1. Clique em **[!UICONTROL Apply]**.

      ![Resultado da etapa](assets/ss2.jpg)


