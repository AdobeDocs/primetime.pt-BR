---
description: Além dos parâmetros básicos do query, os parâmetros opcionais do query permitem que o servidor manifest funcione com diferentes clientes e situações.
seo-description: Além dos parâmetros básicos do query, os parâmetros opcionais do query permitem que o servidor manifest funcione com diferentes clientes e situações.
seo-title: Parâmetros opcionais do query por cliente e situação
title: Parâmetros opcionais do query por cliente e situação
uuid: e3fae41e-9f7d-4f01-9a01-52a1d5f5dad5
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Parâmetros de query opcionais por cliente e situação {#optional-query-parameters-by-client-and-situation}

Além dos parâmetros básicos do query, os parâmetros opcionais do query permitem que o servidor manifest funcione com diferentes clientes e situações.

## Inserção de anúncio com Akamai Ad Scaler {#section_120FEC75C34D4F4587B77D842166D68A}

Na rede de delivery de conteúdo Akamai (CDN), o servidor do Akamai Edge funciona como um intermediário entre o cliente e o servidor manifest. Se você também usar o Ad Scaler, os parâmetros de query `ptassetid` e `live` fornecerão as informações necessárias ao Akamai Edge.

O parâmetro `ptassetid` é a ID do editor para seu ativo. O Akamai usa esse URL, em vez do URL codificado em base64 fornecido como parte do URL da solicitação, para identificar a lista de reprodução a ser fornecida ao servidor manifest para inserção de anúncios.

O parâmetro `live` faz a distinção entre conteúdo ao vivo e vídeo sob demanda (VOD). O servidor manifest precisa dessas informações para suportar sua interface simplificada com o Akamai.

Este é um exemplo de URL que mostra os parâmetros que pertencem ao Akamai:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Inserção de anúncio do TVSDK no Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

Um player baseado no Primetime TVSDK no Xbox não precisa fornecer parâmetros de query adicionais além dos básicos.

## Inserção de anúncios do TVSDK no iOS com o Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

Um player com base no Primetime TVSDK no iOS usando o navegador Safari deve especificar os parâmetros `ptplayer` e `live` além dos parâmetros básicos do query.

O servidor manifest reconhece o valor `ptplayer` `ios-mobileweb` e elimina a pré-rolagem do manifesto com ponto publicitário retornado.

O parâmetro `live` informa ao servidor manifest se deve retornar conteúdo em tempo real ou VOD.

Este é um exemplo de URL que mostra os parâmetros que pertencem ao iOS com o Safari:

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Inserção de anúncio usando um formato de sinalização de anúncio personalizado {#section_82AF880AAABE4BD4B593D906434D4D89}

O Adobe fornece nomes para formatos de sinalização de anúncios que não são suportados diretamente no pacote Primetime. Para usar esse formato, forneça seu nome fornecido pelo Adobe como o valor do parâmetro `ptcueformat`.

Este é um exemplo de URL que especifica um formato de anúncio personalizado:

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Inserção de anúncio usando dicas de anúncio para criar uma linha do tempo FreeWheel para VOD {#section_E0D830F5EEE24639819B975B90F6999F}

Para que o conteúdo VOD que contém dicas de anúncio seja analisado e incluído em uma solicitação de anúncio FreeWheel, defina o valor do parâmetro `ptcueformat` como `DPIsimple`.

Este é um exemplo de URL que especifica o uso de uma linha do tempo FreeWheel para VOD:

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Inserção de anúncio usando uma linha do tempo personalizada para VOD {#section_F398F7659164463FA886A4CC787C7B5A}

Para solicitar que o servidor manifest insira publicidades no conteúdo VOD de acordo com a linha do tempo fornecida, defina o valor do parâmetro `pttimeline` como uma string que especifica a linha do tempo. Consulte [Formato de linha do tempo VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

Este é um exemplo de URL que usa uma linha do tempo personalizada para VOD:

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

Ela especifica uma quebra inicial de um minuto contendo até dois anúncios, seguida por um segmento de conteúdo de dois minutos, seguido por uma quebra de 30 segundos contendo até dois anúncios, seguida por um segmento de conteúdo de cinco minutos.

A costura de anúncios para uma linha do tempo de conteúdo personalizado para conteúdo VOD comporta-se da seguinte maneira:

* O anúncio é exibido no limite de quebra mais próximo após o tempo de posicionamento do anúncio especificado pelo servidor de anúncios.

* Os segmentos têm pelo menos dois segundos de duração.

## Autorizando segmentos TS {#section_BF855A4399DC42CB8C0586113A416BBC}

O Adobe suporta este recurso somente para o Akamai CDN. O HTTP live streaming (HLS) oferece segmentos de transmissão (TS) usando uma lista de reprodução M3U8 de nível de fluxo. Várias listas de reprodução de nível de fluxo são fornecidas ao cliente em uma lista de reprodução variante M3U8. O cliente escolhe um fluxo da lista de reprodução da lista variante e, em seguida, baixa os segmentos TS na lista de reprodução de nível de fluxo um por um. Em operação normal, o conteúdo solicitado pode exigir autorização de cookie, que o servidor manifest lida de forma invisível em segundo plano. Ele extrai o cookie do conteúdo bruto e anexa um token apropriado ao URL a ser usado para solicitar o fluxo da lista de reprodução selecionada.

Quando os parâmetros do query de URL do Bootstrap incluem `pttoken=true`, o editor requer um cookie para ser usado na solicitação de cada segmento TS, em vez de apenas uma vez para o fluxo inteiro. O servidor manifest anexa esse cookie como um parâmetro de query a cada URL de segmento TS na lista de reprodução de fluxo que ele envia.
