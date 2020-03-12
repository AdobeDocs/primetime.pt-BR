---
description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. Entretanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.
seo-description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. Entretanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.
seo-title: Reprodução e failover
title: Reprodução e failover
uuid: 5d75e55d-9c01-4a36-9bdf-891289821c6b
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Reprodução e failover {#playback-and-failover}

O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. Entretanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.

O Primetime não pode proteger contra falhas como uma interrupção ISP ou uma desconexão de cabo. No entanto, o streaming Primetime oferece proteção contra failover para proteger a reprodução contra determinadas falhas de servidor remoto ou operacionais, o que proporciona uma melhor experiência para os visualizadores. O TVSDK do navegador implementa a proteção contra failover para minimizar as interrupções de reprodução e obter uma reprodução contínua, apesar de problemas de transmissão. O player de vídeo muda automaticamente para um conjunto de mídia de backup quando execuções inteiras ou fragmentos não estão disponíveis.

## Reprodução de mídia {#media-playback}

Para mídia dinâmica e VOD, o TVSDK do navegador inicia a reprodução baixando a lista de reprodução associada à taxa de bits de resolução média e baixando os segmentos da mídia de taxa de bits de resolução média definida pela lista de reprodução.

O TVSDK do navegador seleciona rapidamente a lista de reprodução de taxa de bits de alta resolução e sua mídia associada e continua o processo de download.

## Failover de lista de reprodução ausente {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo manifest de nível superior não for baixado, o TVSDK do navegador tentará recuperar. Se não puder ser recuperado, seu aplicativo determinará a próxima etapa.

Se a lista de reprodução associada à taxa de bits de resolução média estiver ausente, o TVSDK do navegador procurará uma lista de reprodução variante na mesma resolução. Se encontrar a mesma resolução, o download da lista de reprodução variante e dos segmentos da posição correspondente será iniciado. Se o TVSDK do navegador não encontrar a mesma lista de reprodução de resolução, ele tentará percorrer outras listas de reprodução de taxa de bits e suas variantes. Uma taxa de bits imediatamente menor é a primeira escolha, depois sua variante e assim por diante. Se todas as listas de reprodução de taxa de bits inferior e suas variantes estiverem esgotadas na tentativa de encontrar uma lista de reprodução válida, o TVSDK do navegador irá para a taxa de bits superior e contará a partir daí. Se não for possível encontrar uma lista de reprodução válida, o processo falhará e o player será movido para o estado ERROR.

Seu aplicativo pode determinar como lidar com essa situação. Por exemplo, você pode querer fechar a atividade do player e direcionar o usuário para a atividade do catálogo. O evento de interesse é o evento de status ou estado alterado, e o retorno de chamada correspondente é o método on status changed. Este é um código que monitora se o player altera seu estado interno para ERRO:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
