---
title: Habilite a demonstração do modelo de uso
description: Habilite a demonstração do modelo de uso
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Habilite a demonstração do modelo de uso{#enable-the-usage-model-demo}

1. Especifique a propriedade personalizada `RI_UsageModelDemo=true` no momento do empacotamento.

   Se estiver empacotando conteúdo usando a ferramenta de linha de comando do Media Packager, insira:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Se você não ativar o modo de demonstração opcional no momento do empacotamento, o servidor de licença emitirá uma licença com base na primeira política de DRM válida que ele processa.

