---
description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. Entretanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.
seo-description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. Entretanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.
seo-title: Formato AC-3 5.1
title: Formato AC-3 5.1
uuid: d5e77bb5-ed51-4f9f-b34f-e9082f5ee4de
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# Formato AC-3 5.1{#ac-format}

O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. Entretanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.

O Primetime não pode proteger contra falhas como uma interrupção ISP ou uma desconexão de cabo. No entanto, o streaming Primetime oferece proteção contra failover para proteger a reprodução contra determinadas falhas de servidor remoto ou operacionais, o que proporciona uma melhor experiência para os visualizadores. O TVSDK implementa a proteção contra failover para minimizar as interrupções de reprodução e obter uma reprodução contínua, apesar de problemas de transmissão. O player de vídeo muda automaticamente para um conjunto de mídia de backup quando execuções inteiras ou fragmentos não estão disponíveis.

O formato Audio Codec 3 (AC-3, também conhecido como Dolby Digital®) 5.1 permite que os provedores de conteúdo compactem o tamanho de arquivos de áudio multicanal sem prejudicar a qualidade do som. O AC-3 é um formato 5.1, o que significa que fornece cinco canais de largura de banda total para uma experiência mais avançada do usuário.

Para obter mais informações, consulte [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

>[!IMPORTANT]
>
>O TVSDK versão 1.4 suporta o formato AC-3 5.1 somente na Amazon FireTV.

O TVSDK suporta os seguintes recursos AC-3 5.1:

* Áudio surround AC-3
* Fluxos mistos/não mistos para o tipo de áudio surround
* Capacidade de query do dispositivo para verificar se o codec de áudio surround está disponível no dispositivo.

   Os resultados determinam qual tipo de codec de áudio preferencial é selecionado. O manifesto com o tipo de codec de áudio que o dispositivo não usará será descartado. Por exemplo, se o formato AC-3 tiver sido selecionado, perfis com o formato AAC (Advanced Audio Coding) não serão considerados.
* Modo de passagem

   No modo de passagem, em vez de decodificar a mídia do formato AC-3 5.1 para um formato PCM (multicanal Pulse-code Modules), o TVSDK é modificado ou não modificado (dependendo do dispositivo) pela mídia Dolby do Decoder. Essa mídia é enviada ao dispositivo de áudio (alto-falante ou receptor) para que o dispositivo de áudio possa decodificar e reproduzir o fluxo surround Dolby.

O TVSDK suporta os recursos AC-3 5.1 somente no dispositivo Amazon Fire TV da primeira geração.

Os seguintes recursos AC-3 5.1 não são suportados:

* Áudio AAC multicanal
* ABR em diferentes codecs (AAC - AC3)

## Selecionar mídia compatível {#section_E1DFA1F472EA4BDE846C71A3343E275A}

Este é o fluxo de trabalho típico que ocorre quando o TVSDK encontra um manifesto com as mídias AC-3 e AAC:

1. Query TVSDK que codec o dispositivo pode suportar.
1. O codec com qualidade superior é selecionado.

   A ordem de qualidade é AC-3 > AAC.
1. O TVSDK ignora perfis com outros tipos de codec de áudio.

>[!TIP]
>
>O aplicativo não pode obter informações sobre perfis ignorados.

## Determinando o modo de saída {#section_64145D9824594C36AADBF0482C528767}

Durante o processamento de mídia AC-3, se um dispositivo Android estiver conectado ao sistema do alto-falante, a decisão de reproduzir o conteúdo no modo surround ou estéreo depende de como o dispositivo está configurado.

|  | Som surround | Alto-falante estéreo |
|---|---|---|
| Dolby de configuração do dispositivo ativado (ou automático) | Dolby de configuração do dispositivo ativado (ou automático) | Modo estéreo |
| Dolby de configuração do dispositivo desativado | Modo estéreo | Modo estéreo |

