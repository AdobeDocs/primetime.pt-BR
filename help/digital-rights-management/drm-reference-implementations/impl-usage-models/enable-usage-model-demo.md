---
title: Habilitar a demonstração do modelo de uso
description: Habilitar a demonstração do modelo de uso
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
