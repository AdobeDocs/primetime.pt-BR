---
description: O formato Audio Codec 3 (AC-3, também conhecido como Dolby Digital®) 5.1 permite que os provedores de conteúdo compactem o tamanho de arquivos de áudio multicanal sem prejudicar a qualidade do som. O AC-3 é um formato 5.1, o que significa que fornece cinco canais de largura de banda total para uma experiência mais avançada do usuário.
seo-description: O formato Audio Codec 3 (AC-3, também conhecido como Dolby Digital®) 5.1 permite que os provedores de conteúdo compactem o tamanho de arquivos de áudio multicanal sem prejudicar a qualidade do som. O AC-3 é um formato 5.1, o que significa que fornece cinco canais de largura de banda total para uma experiência mais avançada do usuário.
seo-title: Formato AC-3 5.1
title: Formato AC-3 5.1
uuid: 11dab0ac-5aed-4909-b9fb-807781f88480
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Formato AC-3 5.1 {#ac-format}

O formato Audio Codec 3 (AC-3, também conhecido como Dolby Digital®) 5.1 permite que os provedores de conteúdo compactem o tamanho de arquivos de áudio multicanal sem prejudicar a qualidade do som. O AC-3 é um formato 5.1, o que significa que fornece cinco canais de largura de banda total para uma experiência mais avançada do usuário.

Para obter mais informações, consulte [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

O TVSDK suporta os seguintes recursos AC-3 5.1:

* Áudio surround AC-3
* Fluxos mistos/não mistos para o tipo de áudio surround
* Capacidade de query do dispositivo para verificar se o codec de áudio surround está disponível no dispositivo.

   Os resultados determinam qual tipo de codec de áudio preferencial é selecionado. O manifesto com o tipo de codec de áudio que o dispositivo não usará será descartado. Por exemplo, se o formato AC-3 tiver sido selecionado, perfis com o formato AAC (Advanced Audio Coding) não serão considerados.
* Modo de passagem

   No modo de passagem, em vez de decodificar a mídia do formato AC-3 5.1 para um formato PCM (multicanal Pulse-code Modules), o TVSDK é modificado ou não modificado (dependendo do dispositivo) pela mídia Dolby do Decoder. Essa mídia é enviada ao dispositivo de áudio (alto-falante ou receptor) para que o dispositivo de áudio possa decodificar e reproduzir o fluxo surround Dolby.

>[!IMPORTANT]
>
>O TVSDK suporta os recursos AC-3 5.1 somente no dispositivo Amazon Fire TV da primeira geração.

Os seguintes recursos AC-3 5.1 não são suportados:

* Áudio AAC multicanal
* ABR em diferentes codecs (AAC - AC3)

## Selecione a mídia compatível {#section_0D7E717BE18B418D817EE017EF2375D1}

Este é o fluxo de trabalho típico que ocorre quando o TVSDK encontra um manifesto com as mídias AC-3 e AAC:

1. Query TVSDK que codec o dispositivo pode suportar.
1. O codec com qualidade superior é selecionado.

   Esta é a ordem na qual a qualidade é selecionada:

   1. AC-3
   1. AAC

1. O TVSDK ignora perfis com outros tipos de codec de áudio.

>[!TIP]
>
>O aplicativo não pode obter informações sobre perfis ignorados.

## Determine o modo de saída {#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

Durante o processamento de mídia AC-3, se um dispositivo Android estiver conectado ao sistema do alto-falante, a decisão de reproduzir o conteúdo no modo surround ou estéreo depende de como o dispositivo está configurado.

|  | Som surround | Alto-falante estéreo |
|---|---|---|
| Dolby de configuração do dispositivo ativado (ou automático) | Dolby de configuração do dispositivo ativado (ou automático) | Modo estéreo |
| Dolby de configuração do dispositivo desativado | Modo estéreo | Modo estéreo |

