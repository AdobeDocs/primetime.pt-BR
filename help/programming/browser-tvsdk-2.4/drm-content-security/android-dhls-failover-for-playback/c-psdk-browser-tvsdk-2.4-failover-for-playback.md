---
description: A transmissão pela Internet requer uma conexão constante e estável para reproduzir um fluxo de um servidor remoto. No entanto, a variabilidade da conexão de Internet ou da reprodução de streaming de um visualizador significa que a reprodução remota pode não ter a qualidade de mídia reproduzida localmente.
title: Reprodução e failover
exl-id: 8316dfb8-3a2e-4057-a3d7-e3d8860e5bd4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Reprodução e failover {#playback-and-failover}

A transmissão pela Internet requer uma conexão constante e estável para reproduzir um fluxo de um servidor remoto. No entanto, a variabilidade da conexão de Internet ou da reprodução de streaming de um visualizador significa que a reprodução remota pode não ter a qualidade de mídia reproduzida localmente.

O Primetime não pode proteger contra falhas como interrupção do ISP ou desconexão de cabo. No entanto, a transmissão contínua do Primetime fornece proteção contra failover para proteger a reprodução de determinadas falhas de servidor remoto ou falhas operacionais, proporcionando uma melhor experiência aos visualizadores. O TVSDK do navegador implementa a proteção contra failover para minimizar as interrupções da reprodução e obter uma reprodução contínua apesar dos problemas de transmissão. O reprodutor de vídeo alterna automaticamente para um conjunto de mídia de backup quando representações ou fragmentos inteiros não estão disponíveis.

## Reprodução de mídia {#media-playback}

Para mídia ao vivo e VOD, o TVSDK do navegador inicia a reprodução baixando a lista de reprodução associada à taxa de bits de resolução média e baixando os segmentos da mídia de taxa de bits de resolução média definida pela lista de reprodução.

O TVSDK do navegador seleciona rapidamente a lista de reprodução de alta resolução com taxa de bits e suas mídias associadas e continua o processo de download.

## Failover de lista de reprodução ausente {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo de manifesto de nível superior não for baixado, o TVSDK do navegador tentará se recuperar. Se não puder ser recuperado, seu aplicativo determinará a próxima etapa.

Se a lista de reprodução associada à taxa de bits de resolução intermediária estiver ausente, o TVSDK do navegador procurará uma lista de reprodução variante na mesma resolução. Se encontrar a mesma resolução, ele inicia o download da lista de reprodução da variante e dos segmentos da posição correspondente. Se o TVSDK do navegador não encontrar a mesma lista de reprodução de resolução, ele tentará percorrer outras listas de reprodução de taxa de bits e suas variantes. Uma taxa de bits imediatamente mais baixa é a primeira escolha, depois sua variante e assim por diante. Se todas as listas de reprodução de taxa de bits mais baixa e suas variantes se esgotarem na tentativa de encontrar uma lista de reprodução válida, o TVSDK do navegador irá para a taxa de bits superior e contará a partir daí. Se uma lista de reprodução válida não puder ser encontrada, o processo falhará e o reprodutor será movido para o estado ERRO.

Seu aplicativo pode determinar como lidar com essa situação. Por exemplo, você pode querer fechar a atividade do reprodutor e direcionar o usuário para a atividade de catálogo. O evento de interesse é o evento de status ou de alteração de estado, e a chamada de retorno correspondente é o método on status changed. Este é o código que monitora se o player altera seu estado interno para ERROR:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
