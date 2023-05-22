---
title: Habilitar a demonstração do modelo de uso
description: Habilitar a demonstração do modelo de uso
copied-description: true
exl-id: 5d546f1a-ebf6-4c93-9a73-fa812cd71086
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# Habilitar a demonstração do modelo de uso{#enable-the-usage-model-demo}

1. Especificar a propriedade personalizada `RI_UsageModelDemo=true` no momento da embalagem.

   Se você estiver empacotando conteúdo com a ferramenta de linha de comando do Media Packager, digite:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Se você não ativar o modo de demonstração opcional no momento do empacotamento, o servidor de licença emitirá uma licença com base na primeira política DRM válida que ele processar.
