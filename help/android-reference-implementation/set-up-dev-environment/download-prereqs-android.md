---
title: Baixe e configure o software de pré-requisito
description: O processo de instalação é simples. Se você já tiver o JDK instalado em seu sistema, ignore esta etapa, mas saiba que seu JDK, Eclipse IDE e o SO precisam ser compatíveis.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Baixe e configure o software de pré-requisito {#download-and-configure-prerequisite-software}

1. Baixe o JDK em [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/).

   O processo de instalação é simples. Se você já tiver o JDK instalado em seu sistema, ignore esta etapa, mas saiba que seu JDK, Eclipse IDE e o SO precisam ser compatíveis.
1. Baixe o Eclipse IDE para desenvolvedores Java em [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads).

   Depois de descompactar o pacote, você pode executar o Eclipse diretamente. Não há instalador.
1. Baixe o pacote ADT do Android SDK em [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html).

   Esse pacote inclui o Eclipse. Se você já tiver o Eclipse instalado em seu sistema, poderá baixar as Ferramentas do SDK para sua plataforma na seção [!UICONTROL Use An Existing IDE].

   Descompacte e instale em um local que você lembrará. Você precisará fazer referência a isso em uma etapa posterior.
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

         Esse processo leva algum tempo.

1. Configure o Eclipse.
   1. Inicie o Eclipse.

      No Windows, se o Eclipse não iniciar e o problema reportado for que o Eclipse não consegue localizar um arquivo Java necessário, tente o seguinte:

      * adicione `-vm C:\[path to your JDK bin]\javaw.exe` ao arquivo [!DNL eclipse.ini].
   1. Selecione **[!UICONTROL Help]** > **[!UICONTROL Install New Software]** .
   1. Clique em **[!UICONTROL Add...]**.
   1. Insira `Android` para o nome.
   1. Insira `https://dl-ssl.google.com/android/eclipse/` para o link **[!UICONTROL Work with]**.
   1. Clique em **[!UICONTROL OK]**.

      Você deve ver uma caixa de diálogo semelhante a esta:

      ![](assets/available_software.jpg)

   1. Selecione os pacotes resultantes (em Ferramentas do desenvolvedor e Plug-ins do NDK) e clique em **[!UICONTROL Next]**.

      Isso baixa as Ferramentas de desenvolvimento do Android (ADT).
   1. Depois que o download for concluído, reinicie o Eclipse.

   O Android SDK agora está instalado. 1. Configure o Eclipse para encontrar o Android SDK e usá-lo como um recurso.
   1. Abra o Eclipse.
   1. Selecione **[!UICONTROL Window]** > **[!UICONTROL Preferences]** no Windows;  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** no Mac OS X.
   1. Selecione a guia **[!UICONTROL Android]**.
   1. Navegue até o local do Android SDK.
   1. Clique em **[!UICONTROL Apply]**.

      ![Resultado da etapa](assets/ss2.jpg)


