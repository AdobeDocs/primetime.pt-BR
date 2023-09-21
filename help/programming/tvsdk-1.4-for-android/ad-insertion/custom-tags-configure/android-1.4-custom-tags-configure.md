---
description: Os fluxos de mídia podem conter metadados adicionais na forma de tags no arquivo de lista de reprodução/manifesto e esse arquivo indica a inserção de publicidade. Você pode especificar nomes de tag personalizados e ser notificado quando determinadas tags aparecerem no arquivo de manifesto.
title: Tags personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Visão geral {#custom-tags-overview}

Os fluxos de mídia podem conter metadados adicionais na forma de tags no arquivo de lista de reprodução/manifesto e esse arquivo indica a inserção de publicidade. Você pode especificar nomes de tag personalizados e ser notificado quando determinadas tags aparecerem no arquivo de manifesto.

## Tags de conteúdo HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Esse recurso não está disponível para o Safari em computadores Apple, pois o TVSDK usa a tag de vídeo, em vez do Flash ou do MSE, para reproduzir conteúdo HLS.

O TVSDK oferece suporte pronto para uso para tags de publicidade #EXT específicas. Seu aplicativo pode usar tags personalizadas para aprimorar o fluxo de trabalho de publicidade ou para suportar cenários de blecaute. Para ser compatível com fluxos de trabalho avançados, o TVSDK permite especificar e assinar tags adicionais no manifesto. Você pode ser notificado quando essas tags aparecerem no arquivo de manifesto.

>[!TIP]
>
>Você pode assinar tags personalizadas para VOD e fluxos ao vivo/lineares.

>[!NOTE]
>
>**Limitação**
>
>Quando o HLS é reproduzido usando o `Video` no Safari, e não usando o Flash Fallback, esse recurso não estará disponível no Safari.

## Uso de tags HLS personalizadas {#section_AD032318AEF5418393D2B1DF36B0BABB}

Este é um exemplo de um ativo de VOD personalizado:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

Seu aplicativo pode configurar os seguintes cenários:

* Uma notificação quando `#EXT-X-ASSET` tags ou qualquer outro conjunto de nomes de tag personalizados que você tenha assinado existem no arquivo.
* Inserir anúncios quando um `#EXT-X-AD` tag, ou qualquer outro nome de tag personalizado, é encontrado no fluxo.

É possível assinar qualquer uma das seguintes tags como tags personalizadas: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. Você foi notificado com uma `TimedMetadata` durante a análise de arquivos manifest.

Há algumas tags de publicidade, como `EXT-X-CUE`, no qual você já se inscreveu. Essas tags de publicidade também são usadas pelo gerador de oportunidades padrão. Você pode especificar quais tags de anúncio são usadas pelo gerador de oportunidades padrão, definindo o `adTags` propriedade.
