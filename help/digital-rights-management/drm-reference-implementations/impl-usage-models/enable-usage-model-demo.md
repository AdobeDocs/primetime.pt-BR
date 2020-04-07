---
seo-title: Ativar a demonstração do modelo de uso
title: Ativar a demonstração do modelo de uso
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 6e949c2f88deef88f0d0ac95b18c006da1c89d2f

---


# Ativar a demonstração do modelo de uso{#enable-the-usage-model-demo}

1. Especifique a propriedade personalizada `RI_UsageModelDemo=true` no horário de empacotamento.

   Se você estiver empacotando conteúdo usando a ferramenta de linha de comando Media Packager, digite:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Se você não ativar o modo de demonstração opcional no momento do empacotamento, o servidor de licenças emitirá uma licença com base na primeira política DRM válida que ele processa.

