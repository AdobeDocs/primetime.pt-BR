---
description: Para mídia ao vivo e de vídeo sob demanda (VOD), o TVSDK inicia a reprodução baixando a lista de reprodução associada à taxa de bits de resolução média e baixa os segmentos de mídia definidos por essa lista de reprodução. Ele seleciona rapidamente a lista de reprodução de alta resolução de taxa de bits e sua mídia associada e continua o processo de download.
title: Reprodução e failover de mídia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Reprodução e failover de mídia{#media-playback-and-failover}

Para mídia ao vivo e de vídeo sob demanda (VOD), o TVSDK inicia a reprodução baixando a lista de reprodução associada à taxa de bits de resolução média e baixa os segmentos de mídia definidos por essa lista de reprodução. Ele seleciona rapidamente a lista de reprodução de alta resolução de taxa de bits e sua mídia associada e continua o processo de download.

## Failover de lista de reprodução ausente {#section_E6B6A15930894F56A0A8501577B35E7F}

Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo de manifesto de nível superior não for baixado, o TVSDK tentará se recuperar. Se não puder ser recuperado, seu aplicativo determinará a próxima etapa.

Se a lista de reprodução associada à taxa de bits de resolução média estiver ausente, o TVSDK procurará uma lista de reprodução variante na mesma resolução. Se encontrar a mesma resolução, ele inicia o download da lista de reprodução da variante e dos segmentos da posição correspondente. Se o TVSDK não encontrar a mesma lista de reprodução de resolução, ele tentará percorrer outras listas de reprodução de taxa de bits e suas variantes. Uma taxa de bits imediatamente mais baixa é a primeira escolha, depois sua variante e assim por diante. Se todas as listas de reprodução de taxa de bits mais baixa e suas variantes se esgotarem na tentativa de encontrar uma lista de reprodução válida, o TVSDK irá para a taxa de bits superior e contará a partir daí. Se uma lista de reprodução válida não puder ser encontrada, o processo falhará e o reprodutor será movido para o estado ERRO.

Seu aplicativo pode determinar como lidar com essa situação. Por exemplo, você pode querer fechar a atividade do reprodutor e direcionar o usuário para a atividade de catálogo. O evento de interesse é o `STATUS_CHANGED` e o retorno de chamada correspondente é o `onStatusChange` método. Este é o código que monitora se o player altera seu estado interno para ERROR:

Para obter mais informações, consulte `PSDKDemo` arquivo. Ouvintes de eventos são anexados à ocorrência de MediaPlayer.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

Se a rede do lado do cliente estiver inativa, você poderá usar esse código para verificar.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

A API fornecerá o URL usado para verificar se a rede do lado do cliente está inativa. Este deve ser um url válido, que retorna o código de resposta http 200 em solicitações http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Se setNetworkDownVerificationUrl não estiver definido, o TVSDK usará o url MainManifest por padrão para descobrir se a rede está inativa.

## Failover de segmento ausente {#section_ED8CF666289042D39E9914D42BDD9BA4}

Quando um segmento está ausente, por exemplo, quando um determinado segmento não é baixado, o TVSDK tenta se recuperar por meio de várias tentativas de failover. Se não conseguir se recuperar, emitirá um erro.

Se um segmento estiver ausente no servidor porque, por exemplo, o arquivo de manifesto não está presente, o segmento não pode ser baixado e assim por diante, o TVSDK tentará fazer failover tentando as seguintes opções:

1. Tente um failover para o mesmo segmento, na mesma taxa de bits, em um arquivo variante.
1. Alterne para uma taxa de bits alternativa (switch ABR) no mesmo arquivo.
1. Percorra cada taxa de bits disponível em cada variante disponível.
1. Ignore o segmento e emita um aviso.

Quando o TVSDK não pode obter um segmento alternativo, ele aciona um `CONTENT_ERROR` notificação de erro. Esta notificação contém uma notificação interna com o código `DOWNLOAD_ERROR` código. Se o fluxo com o problema for uma faixa de áudio alternativa, o TVSDK gerará a variável `AUDIO_TRACK_ERROR` notificação de erro.

Se o mecanismo de vídeo não puder obter segmentos continuamente, ele limitará os segmentos contínuos a 5, após os quais a reprodução será interrompida e o TVSDK emitirá um `NATIVE_ERROR` com o código 5.

>[!NOTE]
>
>Os parâmetros de controle da taxa de bits adaptável (ABR) não são considerados quando ocorre um failover. Isso ocorre porque o mecanismo de failover foi projetado para usar qualquer uma das listas de reprodução disponíveis no momento, independentemente do perfil de taxa de bits, como fluxos de backup.
>
>Durante uma operação de failover, pode haver uma troca de perfil. Se ocorrer um erro durante o download de um dos segmentos da lista de reprodução, os parâmetros de controle ABR, como a taxa de bits mínima/máxima permitida, são ignorados.
