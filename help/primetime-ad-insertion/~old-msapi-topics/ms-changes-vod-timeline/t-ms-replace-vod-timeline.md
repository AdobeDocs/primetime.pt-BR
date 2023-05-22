---
description: Substitua uma linha do tempo de VOD enviando uma nova solicitação de inserção de anúncio ao servidor de manifesto com um parâmetro de consulta de linha do tempo definido adequadamente.
title: Substituir uma linha do tempo de VOD
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Substituir uma linha do tempo de VOD {#replace-a-vod-timeline}

Substitua uma linha do tempo de VOD enviando uma nova solicitação de inserção de anúncio ao servidor de manifesto com um parâmetro de consulta de linha do tempo definido adequadamente.

1. Prepare uma solicitação de inserção de anúncio da maneira usual.
1. Defina o `ptcueformat` para DPIScte35.
1. Defina o `enableC3` parâmetro de consulta para verdadeiro ou falso, conforme apropriado.
1. Criar um `pttimeline` usando o formato de linha do tempo de VOD:
   1. Especifique cada bloco de conteúdo (capítulo) com `duration = 0` e `number_of_lots = 1`.
   1. Especifique cada bloco de publicidade como de costume, mas defina `lots = 0` para remover uma interrupção. Definir `duration = 0` para usar a duração do ad break (do arquivo M3U8).

## Exemplo: Substituição de uma linha de tempo de VOD

Este exemplo supõe que o conteúdo de VOD esteja em `Original.m3u8` com uma linha do tempo de `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

A seguinte solicitação do servidor de manifesto substitui as interrupções em `Original.m3u8` com um pré-lançamento de 30 segundos, seguido de duas interrupções de duração de dois minutos cada.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

A solicitação do servidor de manifesto a seguir remove as interrupções no `Original.m3u8` e adiciona um pré-rolagem de 30 segundos e um pós-rolagem de 30 segundos.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
