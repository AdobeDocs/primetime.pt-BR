---
description: Para mídia dinâmica e VOD, a reprodução de start TVSDK do navegador é feita por download da lista de reprodução associada à taxa de bits de resolução média e, em seguida, por download dos segmentos da mídia de taxa de bits de resolução média definida pela lista de reprodução.
seo-description: Para mídia dinâmica e VOD, a reprodução de start TVSDK do navegador é feita por download da lista de reprodução associada à taxa de bits de resolução média e, em seguida, por download dos segmentos da mídia de taxa de bits de resolução média definida pela lista de reprodução.
seo-title: Reprodução de mídia
title: Reprodução de mídia
uuid: 454f84fe-8077-4f37-8e62-1d6ba0fcde27
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Reprodução de mídia {#media-playback}

Para mídia dinâmica e VOD, a reprodução de start TVSDK do navegador é feita por download da lista de reprodução associada à taxa de bits de resolução média e, em seguida, por download dos segmentos da mídia de taxa de bits de resolução média definida pela lista de reprodução.

O TVSDK do navegador seleciona rapidamente a lista de reprodução de taxa de bits de alta resolução e sua mídia associada e continua o processo de download.

## Failover de lista de reprodução ausente {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo manifest de nível superior não for baixado, o TVSDK do navegador tentará recuperar. Se não puder ser recuperado, seu aplicativo determinará a próxima etapa.

Se a lista de reprodução associada à taxa de bits de resolução média estiver ausente, o TVSDK do navegador procurará uma lista de reprodução variante na mesma resolução. Se encontrar a mesma resolução, ele start o download da lista de reprodução variante e dos segmentos da posição correspondente. Se o TVSDK do navegador não encontrar a mesma lista de reprodução de resolução, ele tentará percorrer outras listas de reprodução de taxa de bits e suas variantes. Uma taxa de bits imediatamente menor é a primeira escolha, depois sua variante e assim por diante. Se todas as listas de reprodução de taxa de bits inferior e suas variantes estiverem esgotadas na tentativa de encontrar uma lista de reprodução válida, o TVSDK do navegador irá para a taxa de bits superior e contará a partir daí. Se não for possível encontrar uma lista de reprodução válida, o processo falhará e o player será movido para o estado ERROR.

Seu aplicativo pode determinar como lidar com essa situação. Por exemplo, talvez você queira fechar a atividade do player e direcionar o usuário para a atividade do catálogo. O evento de interesse é o evento de status ou estado alterado e o retorno de chamada correspondente é o método on status changed. Este é um código que monitora se o player altera seu estado interno para ERRO:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
