---
description: Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo de manifesto de nível superior não for baixado, o TVSDK tentará se recuperar. Se não for possível recuperar, o aplicativo determinará a próxima etapa.
title: Failover de lista de reprodução ausente
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Failover de lista de reprodução ausente{#missing-playlist-failover}

Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo de manifesto de nível superior não for baixado, o TVSDK tentará se recuperar. Se não for possível recuperar, o aplicativo determinará a próxima etapa.

Se a lista de reprodução associada à taxa de bits de resolução média estiver ausente, o TVSDK procurará uma lista de reprodução variante na mesma resolução. Se encontrar a mesma resolução, ele inicia o download da lista de reprodução da variante e dos segmentos da posição correspondente. Se o TVSDK não encontrar a mesma lista de reprodução de resolução, ele tentará percorrer outras listas de reprodução de taxa de bits e suas variantes. Uma taxa de bits imediatamente mais baixa é a primeira escolha, depois sua variante e assim por diante. Se todas as listas de reprodução de taxa de bits mais baixa e suas variantes se esgotarem na tentativa de encontrar uma lista de reprodução válida, o TVSDK irá para a taxa de bits superior e contará a partir daí. Se uma lista de reprodução válida não puder ser encontrada, o processo falhará e o reprodutor será movido para o estado ERRO.

Seu aplicativo pode determinar como lidar com essa situação. Por exemplo, você pode querer fechar a atividade do reprodutor e direcionar o usuário para a atividade de catálogo. O evento de interesse é o `STATE_CHANGED` e o retorno de chamada correspondente é o `onStateChanged` método. Este é o código que monitora se o player altera seu estado interno para ERROR:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Para obter mais informações, consulte [!DNL PlayerFragment.java] arquivo no SDK:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
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
