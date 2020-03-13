---
description: A TVSDK Primetime Reference é um aplicativo Android criado em torno das estruturas TVSDK e AVE.
seo-description: A TVSDK Primetime Reference é um aplicativo Android criado em torno das estruturas TVSDK e AVE.
seo-title: Criar a implementação de referência do Primetime
title: Criar a implementação de referência do Primetime
uuid: ab12660a-1563-49a4-82d9-1ab13f8a92be
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Criar a implementação de referência do Primetime {#build-the-primetime-reference-implementation}

A TVSDK Primetime Reference é um aplicativo Android criado em torno das estruturas TVSDK e AVE.

Para configurar e criar o projeto de Referência do Primetime no Eclipse:

1. Baixe o arquivo zip Android TVSDK e descompacte-o em um diretório em um local que você lembrará.
1. Inicie o Eclipse.
1. Selecione **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Selecione **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Clique em **[!UICONTROL Next]**.
1. Use o **[!UICONTROL Browse]** botão para preencher o **[!UICONTROL Root Directory]** campo com o diretório sob [!DNL samples/PrimetimeReference/src] o qual você descompactou o arquivo zip Android TVSDK.
1. Selecione os seguintes projetos a serem importados: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Clique em **[!UICONTROL Finish]**.
1. Selecione **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para criar o projeto.

   Essa etapa não é necessária se o projeto estiver configurado para ser construído automaticamente.
1. Se você quiser incluir o projeto de testes na área de trabalho, associe o projeto de testes ao projeto PrimetimeReference:
   1. Repita as etapas 3. até 6.
   1. Selecione o seguinte projeto a ser importado: `PrimetimeReference\tests`.
   1. Clique em **[!UICONTROL Finish]**.

      O projeto de testes tem uma dependência do projeto CatalogActivity, portanto, é necessário associar o projeto de testes ao projeto CatalogActivity.
   1. Clique com o botão direito do mouse **[!UICONTROL tests]** e escolha **[!UICONTROL Properties]**.
   1. Selecione a **[!UICONTROL Projects]** guia em Java Build Path.
   1. Clique em **[!UICONTROL Add...]**
   1. Selecione CatalogActivity.
   1. Clique em **[!UICONTROL OK]** para adicionar o projeto.
   1. Clique **[!UICONTROL OK]** para sair da página Propriedades.
   1. Selecione **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para criar o projeto.

      Essa etapa não é necessária se o projeto estiver configurado para ser construído automaticamente.
