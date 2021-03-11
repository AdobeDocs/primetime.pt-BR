---
description: A TVSDK Primetime Reference é um aplicativo Android criado com as estruturas TVSDK e AVE.
title: Criar a implementação de referência do Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---


# Criar a implementação de referência do Primetime {#build-the-primetime-reference-implementation}

A TVSDK Primetime Reference é um aplicativo Android criado com as estruturas TVSDK e AVE.

Para configurar e criar o projeto de referência do Primetime no Eclipse:

1. Baixe o arquivo zip TVSDK do Android e descompacte-o em um diretório em um local que você lembrará.
1. Inicie o Eclipse.
1. Selecione **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Selecione **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Clique em **[!UICONTROL Next]**.
1. Use o botão **[!UICONTROL Browse]** para preencher o campo **[!UICONTROL Root Directory]** com o diretório em [!DNL samples/PrimetimeReference/src] para o qual você descompactou o arquivo zip Android TVSDK.
1. Selecione os seguintes projetos a serem importados: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Clique em **[!UICONTROL Finish]**.
1. Selecione **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para criar o projeto.

   Essa etapa não é necessária se o projeto estiver configurado para ser criado automaticamente.
1. Se desejar incluir o projeto de testes no espaço de trabalho, associe o projeto de testes ao projeto PrimetimeReference:
   1. Repita as etapas 3. até 6.
   1. Selecione o projeto a seguir para importar: `PrimetimeReference\tests`.
   1. Clique em **[!UICONTROL Finish]**.

      O projeto de testes tem uma dependência no projeto CatalogActivity para que você precise associar o projeto de testes ao projeto CatalogActivity.
   1. Clique com o botão direito do mouse em **[!UICONTROL tests]** e escolha **[!UICONTROL Properties]**.
   1. Selecione a guia **[!UICONTROL Projects]** em Caminho de compilação Java.
   1. Clique em **[!UICONTROL Add...]**
   1. Selecione CatalogActivity.
   1. Clique em **[!UICONTROL OK]** para adicionar o projeto.
   1. Clique em **[!UICONTROL OK]** para sair da página Propriedades.
   1. Selecione **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para criar o projeto.

      Essa etapa não é necessária se o projeto estiver configurado para ser criado automaticamente.
