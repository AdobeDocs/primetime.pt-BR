---
description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão de Internet de um visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.
title: Reprodução e failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Reprodução e failover {#playback-and-failover}

O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão de Internet de um visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.

O Primetime não pode proteger contra falhas como uma interrupção de ISP ou uma desconexão de cabo. No entanto, o streaming do Primetime oferece proteção contra failover para proteger a reprodução de determinadas falhas de servidor remoto ou falhas operacionais, o que melhora a experiência dos visualizadores. O TVSDK do navegador implementa a proteção contra failover para minimizar as interrupções da reprodução e obter uma reprodução contínua apesar dos problemas de transmissão. O reprodutor de vídeo muda automaticamente para um conjunto de mídia de backup quando representações inteiras ou fragmentos não estão disponíveis.

## Reprodução de mídia {#media-playback}

Para mídia ao vivo e VOD, o TVSDK do Navegador inicia a reprodução baixando a lista de reprodução associada à taxa de bits de resolução média e, em seguida, baixando segmentos da mídia de taxa de bits de resolução média que é definida pela lista de reprodução.

O TVSDK do navegador seleciona rapidamente a lista de reprodução de taxa de bits de alta resolução e sua mídia associada e continua o processo de download.

## Failover de lista de reprodução ausente {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Quando uma lista de reprodução inteira está ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo de manifesto de nível superior não é baixado, o TVSDK do navegador tenta se recuperar. Se não puder ser recuperado, o aplicativo determinará a próxima etapa.

Se a lista de reprodução associada à taxa de bits de resolução média estiver ausente, o TVSDK do navegador procurará uma lista de reprodução de variante na mesma resolução. Se encontrar a mesma resolução, ele começará a baixar a lista de reprodução da variante e os segmentos da posição correspondente. Se o TVSDK do navegador não encontrar a mesma lista de reprodução de resolução, ele tentará alternar entre outras listas de reprodução de taxa de bits e suas variantes. Uma taxa de bits imediatamente menor é a primeira escolha, depois sua variante e assim por diante. Se todas as listas de reprodução de taxa de bits mais baixas e suas variantes estiverem esgotadas na tentativa de encontrar uma lista de reprodução válida, o TVSDK do navegador irá para a taxa de bits superior e contará a partir daí. Se não for possível localizar uma lista de reprodução válida, o processo falhará e o reprodutor será movido para o estado ERROR.

Seu aplicativo pode determinar como lidar com essa situação. Por exemplo, talvez você queira fechar a atividade do reprodutor e direcionar o usuário para a atividade de catálogo. O evento de interesse é o evento de status ou estado alterado e o retorno de chamada correspondente é o método on status changed . Este é um código que monitora se o reprodutor altera seu estado interno para ERRO:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
