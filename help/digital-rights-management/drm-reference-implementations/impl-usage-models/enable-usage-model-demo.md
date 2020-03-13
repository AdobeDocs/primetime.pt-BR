---
seo-title: Ativar a demonstração do modelo de uso
title: Ativar a demonstração do modelo de uso
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Ativar a demonstração do modelo de uso{#enable-the-usage-model-demo}

1. Especifique a propriedade personalizada `RI_UsageModelDemo=true` no horário de empacotamento.

   Se você estiver empacotando conteúdo usando a ferramenta de linha de comando Media Packager, digite:

   ```
   java -jar AdobeMediaPackager.jar [
   
<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true

```
>[!NOTE] {class="- topic/note "}
>
>If you do not activate the optional demo mode at packaging time, the license server issues a license based on the first valid DRM policy it processes.

