---
description: Além dos parâmetros de consulta básicos, os parâmetros de consulta opcionais permitem que o servidor de manifesto funcione com clientes e situações diferentes.
title: Parâmetros de consulta opcionais por cliente e situação
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Parâmetros de consulta opcionais por cliente e situação {#optional-query-parameters-by-client-and-situation}

Além dos parâmetros de consulta básicos, os parâmetros de consulta opcionais permitem que o servidor de manifesto funcione com clientes e situações diferentes.

## Inserção de anúncio com o Akamai Ad Scaler {#section_120FEC75C34D4F4587B77D842166D68A}

Na rede de entrega de conteúdo (CDN) da Akamai, o servidor Akamai Edge funciona como um intermediário entre o cliente e o servidor manifest. Se também usar o Ad Scaler, os parâmetros de consulta `ptassetid` e `live` fornecerão as informações necessárias ao Akamai Edge.

O parâmetro `ptassetid` é a ID do editor para seu ativo. O Akamai usa esse URL, em vez do URL codificado em base64 fornecido como parte do URL da solicitação, para identificar a lista de reprodução a ser fornecida ao servidor de manifesto para inserção de anúncio.

O parâmetro `live` faz a distinção entre conteúdo ao vivo e vídeo sob demanda (VOD). O servidor manifest precisa dessas informações para oferecer suporte à interface simplificada com o Akamai.

Este é um exemplo de URL que mostra os parâmetros que pertencem ao Akamai:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Inserção de anúncio do TVSDK no Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

Um reprodutor baseado no Primetime TVSDK no Xbox não precisa fornecer parâmetros de consulta adicionais além dos básicos.

## Inserção de anúncio do TVSDK no iOS com Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

Um reprodutor com base no Primetime TVSDK no iOS usando o navegador Safari deve especificar os parâmetros `ptplayer` e `live` além dos parâmetros de consulta básicos.

O servidor manifest reconhece o valor `ptplayer` `ios-mobileweb` e elimina o precedente do manifesto anexado retornado.

O parâmetro `live` informa ao servidor de manifesto se deve retornar conteúdo em tempo real ou VOD.

Este é um exemplo de URL que mostra os parâmetros que pertencem ao iOS com o Safari:

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Inserção de anúncio usando um formato de sinalização de anúncio personalizado {#section_82AF880AAABE4BD4B593D906434D4D89}

O Adobe fornece nomes para formatos de sinalização de anúncio que não são compatíveis diretamente no pacote Primetime. Para usar esse formato, forneça seu nome fornecido pelo Adobe como o valor do parâmetro `ptcueformat`.

Este é um exemplo de URL especificando um formato de sinalização de anúncio personalizado:

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Inserção de anúncio usando dicas de anúncio para criar uma linha do tempo FreeWheel para VOD {#section_E0D830F5EEE24639819B975B90F6999F}

Para que o conteúdo de VOD que contém dicas de anúncio seja analisado e incluído em uma solicitação de anúncio FreeWheel, defina o valor do parâmetro `ptcueformat` como `DPIsimple`.

Este é um exemplo de URL que especifica o uso de uma linha do tempo FreeWheel para VOD:

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Inserção de anúncio usando uma linha do tempo personalizada para VOD {#section_F398F7659164463FA886A4CC787C7B5A}

Para solicitar que o servidor de manifesto insira anúncios no conteúdo VOD de acordo com a linha do tempo fornecida, defina o valor do parâmetro `pttimeline` como uma string especificando a linha do tempo. Consulte [Formato de linha do tempo VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

Este é um exemplo de URL que usa uma linha do tempo personalizada para VOD:

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

Especifica uma quebra inicial de um minuto que contém até dois anúncios, seguido por um segmento de conteúdo de dois minutos, seguido por uma quebra de 30 segundos que contém até dois anúncios, seguido por um segmento de conteúdo de cinco minutos.

A compilação de anúncios para uma linha do tempo do conteúdo personalizado para o conteúdo VOD se comporta da seguinte maneira:

* O anúncio aparece no limite de quebra mais próximo após o tempo de posicionamento do anúncio especificado pelo servidor de anúncios.

* Os segmentos têm pelo menos dois segundos de duração.

## Autorizar segmentos TS {#section_BF855A4399DC42CB8C0586113A416BBC}

O Adobe suporta esse recurso somente para o Akamai CDN. O HTTP live streaming (HLS) fornece segmentos de fluxo de transporte (TS) usando uma lista de reprodução M3U8 em nível de fluxo. Várias listas de reprodução em nível de fluxo são fornecidas ao cliente em uma lista de reprodução variante M3U8. O cliente escolhe um fluxo de lista de reprodução da lista de variantes e, em seguida, baixa os segmentos TS dessa lista de reprodução em nível de fluxo um por um. Em operação normal, o conteúdo solicitado pode exigir autorização de cookie, que o servidor de manifesto lida de forma invisível em segundo plano. Ele extrai o cookie do conteúdo bruto e anexa um token apropriado ao URL a ser usado na solicitação do fluxo da lista de reprodução selecionada.

Quando os parâmetros de consulta de URL do Bootstrap incluem `pttoken=true`, o editor requer que um cookie seja usado na solicitação de cada segmento TS, em vez de apenas uma vez para todo o fluxo. O servidor manifest anexa esse cookie como um parâmetro de consulta para cada URL de segmento TS na lista de reprodução de fluxo que ele envia de volta.
