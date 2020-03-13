---
description: Para mídia ao vivo e vídeo sob demanda (VOD), o TVSDK inicia a reprodução baixando a lista de reprodução associada à taxa de bits de resolução média e baixando os segmentos de mídia definidos pela lista de reprodução. Ele seleciona rapidamente a lista de reprodução de taxa de bits de alta resolução e sua mídia associada e continua o processo de download.
seo-description: Para mídia ao vivo e vídeo sob demanda (VOD), o TVSDK inicia a reprodução baixando a lista de reprodução associada à taxa de bits de resolução média e baixando os segmentos de mídia definidos pela lista de reprodução. Ele seleciona rapidamente a lista de reprodução de taxa de bits de alta resolução e sua mídia associada e continua o processo de download.
seo-title: Reprodução e failover de mídia
title: Reprodução e failover de mídia
uuid: e0072eeb-8ad1-436f-bf4a-fee6885a25bd
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Reprodução e failover de mídia {#media-playback-and-failover}

Para mídia ao vivo e vídeo sob demanda (VOD), o TVSDK inicia a reprodução baixando a lista de reprodução associada à taxa de bits de resolução média e baixando os segmentos de mídia definidos pela lista de reprodução. Ele seleciona rapidamente a lista de reprodução de taxa de bits de alta resolução e sua mídia associada e continua o processo de download.

## Failover de lista de reprodução ausente {#section_4EA0AEFA7FB84FCEA699DFB10B135368}

Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo manifest de nível superior não for baixado, o TVSDK tentará recuperar. Se não puder ser recuperado, seu aplicativo determinará a próxima etapa.

Se a lista de reprodução associada à taxa de bits de resolução média estiver ausente, o TVSDK pesquisará uma lista de reprodução variante na mesma resolução. Se encontrar a mesma resolução, o TVSDK começará a baixar a lista de reprodução variante e os segmentos da posição correspondente. Se o player não encontrar a mesma lista de reprodução de resolução, ele tentará percorrer outras listas de reprodução de taxa de bits e suas variantes. Uma taxa de bits imediatamente menor é a primeira escolha, depois sua variante e assim por diante. Se todas as listas de reprodução de taxa de bits inferior e suas variantes estiverem esgotadas na tentativa de encontrar uma lista de reprodução válida, o TVSDK irá para a taxa de bits superior e contará a partir daí. Se não for possível encontrar uma lista de reprodução válida, o processo falhará e o player será movido para o estado ERROR.

Seu aplicativo pode determinar como lidar com essa situação. Por exemplo, você pode querer fechar a atividade do player e direcionar o usuário para a atividade do catálogo. O evento de interesse é o `STATUS_CHANGED` evento e o retorno de chamada correspondente é o `onStatusChanged` método. Este é o código que monitora se o player altera seu status interno para `ERROR`:

```java
... 
case ERROR: 
getActivity().finish(); // this is where we close the current activity (the Player activity) 
break; 
...
```

## Failover de segmento ausente {#section_D8DF377CCB644D7FB936796DA0CC5A4B}

Quando um segmento está ausente, por exemplo, quando um segmento específico falha no download, o TVSDK tenta se recuperar por meio de várias tentativas de failover. Se não conseguir recuperar, isso emite um erro.

Se um segmento estiver ausente no servidor porque, por exemplo, o arquivo manifest não está presente, o segmento não pode ser baixado e assim por diante, o TVSDK tenta fazer failover tentando as seguintes opções:

1. Tente um failover para o mesmo segmento, na mesma taxa de bits, em um arquivo de variante.
1. Alterne para uma taxa de bits alternativa (switch ABR) no mesmo arquivo.
1. Faça o ciclo de cada taxa de bits disponível em cada variante disponível.
1. Ignore o segmento e emita um aviso.

Quando o TVSDK não pode obter um segmento alternativo, ele aciona uma notificação de `CONTENT_ERROR` erro. Esta notificação contém uma notificação interna com o `DOWNLOAD_ERROR` código. Se o fluxo com o problema for uma faixa de áudio alternativa, o TVSDK gera a notificação de `AUDIO_TRACK_ERROR` erro.

Se o mecanismo de vídeo não conseguir obter segmentos continuamente, ele limita o segmento contínuo para 5, após o qual a reprodução é interrompida e o TVSDK emite um erro `NATIVE_ERROR` com o código 5.

>[!Rrestrições]
>
>Estas são algumas restrições que você deve estar ciente:
>* Os parâmetros de controle da taxa de bits adaptável (ABR) não são considerados quando ocorre um failover.
>
>  
Isso ocorre porque o mecanismo de failover foi projetado para usar qualquer uma das listas de reprodução disponíveis no momento, independentemente do perfil de taxa de bits, como fluxos de backup.
>* Durante uma operação de failover, pode haver um switch de perfil.
>
>  
Se ocorrer um erro durante o download de um dos segmentos da lista de reprodução, os parâmetros de controle ABR, como a taxa de bits mínima/máxima permitida, serão ignorados.