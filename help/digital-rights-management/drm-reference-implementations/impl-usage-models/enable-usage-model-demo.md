---
seo-title: Ativar a demonstração do modelo de uso
title: Ativar a demonstração do modelo de uso
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Habilitar a demonstração do modelo de uso{#enable-the-usage-model-demo}

1. Especifique a propriedade personalizada `RI_UsageModelDemo=true` no momento do empacotamento.

   Se você estiver empacotando conteúdo usando a ferramenta de linha de comando Media Packager, digite:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Se você não ativar o modo de demonstração opcional no momento do empacotamento, o servidor de licenças emitirá uma licença com base na primeira política DRM válida que ele processa.

