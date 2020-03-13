---
description: Substitua uma linha do tempo VOD enviando uma nova solicitação de inserção de publicidade para o servidor manifest por um parâmetro de consulta de linha do tempo devidamente definido.
seo-description: Substitua uma linha do tempo VOD enviando uma nova solicitação de inserção de publicidade para o servidor manifest por um parâmetro de consulta de linha do tempo devidamente definido.
seo-title: Substituir uma linha do tempo VOD
title: Substituir uma linha do tempo VOD
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Substituir uma linha do tempo VOD {#replace-a-vod-timeline}

Substitua uma linha do tempo VOD enviando uma nova solicitação de inserção de publicidade para o servidor manifest por um parâmetro de consulta de linha do tempo devidamente definido.

1. Prepare uma solicitação de inserção de anúncio da maneira habitual.
1. Defina o parâmetro de `ptcueformat` consulta como DPIScte35.
1. Defina o parâmetro de `enableC3` consulta como true ou false, conforme apropriado.
1. Crie um `pttimeline` parâmetro usando o formato de linha do tempo VOD:
   1. Especifique cada bloco de conteúdo (capítulo) com `duration = 0` e `number_of_lots = 1`.
   1. Especifique cada bloco de publicidade como de costume, mas defina `lots = 0` para remover uma quebra. Defina `duration = 0` para usar a duração do intervalo do anúncio (do arquivo M3U8).

## Exemplo: Substituição de uma linha do tempo VOD

Este exemplo supõe que o conteúdo VOD esteja em `Original.m3u8` uma linha do tempo de `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

A seguinte solicitação de servidor manifest substitui as quebras `Original.m3u8` por uma pré-rolagem de 30 segundos, seguida de duas quebras de duração de dois minutos cada.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

A solicitação de servidor manifest a seguir remove as quebras em `Original.m3u8` e adiciona uma pré-rolagem de 30 segundos e uma pós-rolagem de 30 segundos.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
