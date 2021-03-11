---
description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão de Internet de um visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.
title: Formato AC-3 5.1
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Formato AC-3 5.1{#ac-format}

O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão de Internet de um visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.

O Primetime não pode proteger contra falhas como uma interrupção de ISP ou uma desconexão de cabo. No entanto, o streaming do Primetime oferece proteção contra failover para proteger a reprodução de determinadas falhas de servidor remoto ou falhas operacionais, o que melhora a experiência dos visualizadores. O TVSDK implementa a proteção contra failover para minimizar as interrupções da reprodução e obter uma reprodução contínua apesar dos problemas de transmissão. O reprodutor de vídeo muda automaticamente para um conjunto de mídia de backup quando representações inteiras ou fragmentos não estão disponíveis.

O Audio Codec 3 (AC-3, também conhecido como Dolby Digital®) 5.1, permite que os provedores de conteúdo compactem o tamanho de arquivos de áudio multicanal sem prejudicar a qualidade do som. O AC-3 é um formato 5.1, o que significa que ele fornece cinco canais de largura de banda total para uma experiência do usuário mais rica.

Para obter mais informações, consulte [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

>[!IMPORTANT]
>
>O TVSDK versão 1.4 é compatível com o formato AC-3 5.1 somente no Amazon FireTV.

O TVSDK é compatível com os seguintes recursos do AC-3 5.1:

* Áudio surround AC-3
* Fluxos mistos/não mistos para o tipo de áudio surround
* Capacidade de consultar o dispositivo para ver se o codec de áudio surround está disponível no dispositivo.

   Os resultados determinam qual tipo de codec de áudio preferencial é selecionado. O manifesto com o tipo de codec de áudio que o dispositivo não vai usar é descartado. Por exemplo, se o formato AC-3 tiver sido selecionado, os perfis com o formato Advanced Audio Coding (AAC) não serão considerados.
* Modo de passagem

   No modo de passagem, em vez de decodificar a mídia do formato AC-3 5.1 para um formato PCM (multicanal pulse-code Modules), o TVSDK é modificado ou não modificado (dependendo do dispositivo) a mídia Dolby do decodificador. Essa mídia é enviada para o dispositivo de áudio (alto-falante ou receptor) para que o dispositivo de áudio possa decodificar e reproduzir o fluxo surround Dolby.

O TVSDK é compatível com os recursos AC-3 5.1 somente no dispositivo Amazon Fire TV de primeira geração.

Os seguintes recursos do AC-3 5.1 não são compatíveis:

* Áudio AAC multicanal
* ABR em diferentes codecs (AAC - AC3)

## Selecionar mídia compatível {#section_E1DFA1F472EA4BDE846C71A3343E275A}

Este é um fluxo de trabalho típico que ocorre quando o TVSDK encontra um manifesto com mídia AC-3 e AAC:

1. Consultas TVSDK que codec o dispositivo pode suportar.
1. O codec com a qualidade mais alta é selecionado.

   A ordem de qualidade é AC-3 > AAC.
1. O TVSDK ignora perfis com outros tipos de codec de áudio.

>[!TIP]
>
>O aplicativo não pode obter informações sobre perfis ignorados.

## Determinar o modo de saída {#section_64145D9824594C36AADBF0482C528767}

Ao processar mídia AC-3, se um dispositivo Android estiver conectado ao sistema de alto-falantes, a decisão de reproduzir o conteúdo no modo surround ou estéreo dependerá de como o dispositivo está configurado.

|  | Som surround | Altifalante estéreo |
|---|---|---|
| Configuração do dispositivo Dolby on (ou auto) | Configuração do dispositivo Dolby on (ou auto) | Modo estéreo |
| Dolby de configuração do dispositivo desativado | Modo estéreo | Modo estéreo |

