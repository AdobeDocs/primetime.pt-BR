---
title: Faça o download e configure os softwares de pré-requisito
description: O processo de instalação é simples. Se você já tiver o JDK instalado no sistema, ignore esta etapa, mas esteja ciente de que o JDK, o Eclipse IDE e o SO precisam ser compatíveis.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Faça o download e configure os softwares de pré-requisito {#download-and-configure-prerequisite-software}

1. Baixar o JDK de [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/).

   O processo de instalação é simples. Se você já tiver o JDK instalado no sistema, ignore esta etapa, mas esteja ciente de que o JDK, o Eclipse IDE e o SO precisam ser compatíveis.
1. Baixe o Eclipse IDE para desenvolvedores Java em [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads).

   Após descompactar o pacote, você pode executar o Eclipse diretamente. Não há instalador.
1. Baixe o pacote ADT do SDK do Android em [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html).

   Esse pacote inclui o Eclipse. Se você já tiver o Eclipse instalado em seu sistema, poderá baixar as Ferramentas de SDK para sua plataforma na [!UICONTROL Use An Existing IDE] seção.

   Descompacte e instale em um local que você se lembrará. Você precisará consultar isso em uma etapa posterior.
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

1. Configurar o Eclipse.
   1. Inicie o Eclipse.

      No Windows, se o Eclipse não iniciar e o problema relatado for que o Eclipse não pode encontrar um arquivo Java necessário, tente o seguinte:

      * adicionar `-vm C:\[path to your JDK bin]\javaw.exe` ao seu [!DNL eclipse.ini] arquivo.
   1. Selecionar  **[!UICONTROL Help]** > **[!UICONTROL Install New Software]** .
   1. Clique em **[!UICONTROL Add...]**.
   1. Enter `Android` para o nome.
   1. Enter `https://dl-ssl.google.com/android/eclipse/` para o **[!UICONTROL Work with]** link.
   1. Clique em **[!UICONTROL OK]**.

      Você deve ver uma caixa de diálogo semelhante a esta:

      ![](assets/available_software.jpg)

   1. Selecione os pacotes resultantes (aqueles em Ferramentas do desenvolvedor e Plug-ins NDK) e clique em **[!UICONTROL Next]**.

      Isso baixa as Ferramentas de desenvolvimento do Android (ADT).
   1. Após concluir o download, reinicie o Eclipse.

   O Android SDK agora está instalado. 1. Configure o Eclipse para que ele possa encontrar o Android SDK e usá-lo como um recurso.
   1. Abra o Eclipse.
   1. Selecionar  **[!UICONTROL Window]** > **[!UICONTROL Preferences]** no Windows;  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** no Mac OS X.
   1. Selecione o **[!UICONTROL Android]** guia.
   1. Navegue até o local do Android SDK.
   1. Clique em **[!UICONTROL Apply]**.

      ![Resultado da etapa](assets/ss2.jpg)
