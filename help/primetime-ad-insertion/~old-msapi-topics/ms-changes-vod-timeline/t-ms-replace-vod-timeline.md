---
description: Substitua uma linha do tempo VOD enviando uma nova solicitação de inserção de anúncio ao servidor manifest com um parâmetro de consulta de linha do tempo definido apropriadamente.
title: Substituir uma linha do tempo de VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Substituir uma linha do tempo VOD {#replace-a-vod-timeline}

Substitua uma linha do tempo VOD enviando uma nova solicitação de inserção de anúncio ao servidor manifest com um parâmetro de consulta de linha do tempo definido apropriadamente.

1. Prepare uma solicitação de inserção de anúncio da maneira normal.
1. Defina o parâmetro de consulta `ptcueformat` como DPIScte35.
1. Defina o parâmetro de consulta `enableC3` como true ou false, conforme apropriado.
1. Crie um parâmetro `pttimeline` usando o formato de linha do tempo VOD:
   1. Especifique cada bloco de conteúdo (capítulo) com `duration = 0` e `number_of_lots = 1`.
   1. Especifique cada bloco de anúncio como de costume, mas defina `lots = 0` para remover uma quebra. Defina `duration = 0` para usar a duração do ad break (a partir do arquivo M3U8).

## Exemplo: Substituição de uma linha do tempo de VOD

Este exemplo supõe que o conteúdo de VOD está em `Original.m3u8` com uma linha do tempo de `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

A solicitação de servidor manifest a seguir substitui as quebras em `Original.m3u8` por um precedente de 30 segundos, seguido por duas quebras de duração de dois minutos cada.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

A solicitação de servidor de manifesto a seguir remove as quebras em `Original.m3u8` e adiciona um precedente de 30 segundos e um pós-rolagem de 30 segundos.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
