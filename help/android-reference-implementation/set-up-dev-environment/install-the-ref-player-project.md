---
description: O TVSDK Primetime Reference é um aplicativo Android criado em torno das estruturas TVSDK e AVE.
title: Criar a implementação de referência do Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Criar a implementação de referência do Primetime {#build-the-primetime-reference-implementation}

O TVSDK Primetime Reference é um aplicativo Android criado em torno das estruturas TVSDK e AVE.

Para configurar e criar o projeto de referência do Primetime no Eclipse:

1. Baixe o arquivo zip TVSDK Android e descompacte-o em um diretório em um local que você se lembrará.
1. Inicie o Eclipse.
1. Selecionar **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Selecionar **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Clique em **[!UICONTROL Next]**.
1. Use o **[!UICONTROL Browse]** botão para preencher a **[!UICONTROL Root Directory]** com o diretório em [!DNL samples/PrimetimeReference/src] ao qual você descompactou o arquivo zip TVSDK Android.
1. Selecione os seguintes projetos para importar: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Clique em **[!UICONTROL Finish]**.
1. Selecionar  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para construir o projeto.

   Esta etapa não será necessária se o projeto estiver configurado para build automaticamente.
1. Se você quiser incluir o projeto de testes no espaço de trabalho, associe o projeto de testes ao projeto PrimetimeReference:
   1. Repita as etapas 3. até 6.
   1. Selecione o seguinte projeto para importar: `PrimetimeReference\tests`.
   1. Clique em **[!UICONTROL Finish]**.

      O projeto de testes tem uma dependência no projeto CatalogActivity, portanto, é necessário associar o projeto de testes ao projeto CatalogActivity.
   1. Clique com o botão direito do mouse **[!UICONTROL tests]** e escolha **[!UICONTROL Properties]**.
   1. Selecione o **[!UICONTROL Projects]** em Caminho de compilação Java.
   1. Clique em **[!UICONTROL Add...]**
   1. Selecione CatalogActivity.
   1. Clique em **[!UICONTROL OK]** para adicionar o projeto.
   1. Clique em **[!UICONTROL OK]** para sair da página Propriedades.
   1. Selecionar  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para construir o projeto.

      Esta etapa não será necessária se o projeto estiver configurado para build automaticamente.
